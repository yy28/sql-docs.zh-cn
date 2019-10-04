---
title: 有关在 R 中创建、训练和评分基于分区的模型的教程
description: 了解如何在使用 SQL Server 机器学习的基于分区的建模能力时, 对动态创建的分区数据进行建模、定型和使用。
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/27/2019
ms.topic: tutorial
ms.author: davidph
author: dphansen
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3395b237e08a10033819eeed74057cc7319d7f11
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952024"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>教程：在 SQL Server 中的 R 中创建基于分区的模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在 SQL Server 2019 中, 基于分区的建模是对已分区数据创建和定型模型的能力。 对于自然分成给定分类方案的分层数据 (例如地理区域、日期和时间、年龄或性别), 可以对整个数据集执行脚本, 并能够对保持不变的分区进行建模、定型和评分所有这些操作。 

基于分区的建模通过[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)上的两个新参数启用：

+ **input_data_1_partition_by_columns**，指定要按其进行分区的列。
+ **input_data_1_order_by_columns**指定排序所依据的列。 

本教程介绍如何使用经典 NYC 出租车示例数据和 R 脚本进行基于分区的建模。 分区列是支付方法。

> [!div class="checklist"]
> * 分区基于付款类型 (5)。
> * 在每个分区上创建和训练模型, 并将对象存储在数据库中。
> * 预测每个分区模型上的 tip 结果的概率, 使用为此目的而保留的示例数据。

## <a name="prerequisites"></a>先决条件
 
若要完成本教程, 您必须具备以下各项:

+ 系统资源充足。 数据集很大, 定型操作非常耗费资源。 如果可能, 请使用至少具有 8 GB RAM 的系统。 或者, 可以使用较小的数据集来解决资源约束。 有关缩减数据集的说明是内联的。 

+ 用于 T-sql 查询执行的工具, 如[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

+ [NYCTaxi_Sample](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)，可以将其[下载并还原](demo-data-nyctaxi-in-sql.md)到本地数据库引擎实例。 文件大小约为 90 MB。

+ SQL Server 2019 预览数据库引擎实例, 具有机器学习服务和 R 集成。

通过在查询工具 **`SELECT @@Version`** 中作为 t-sql 查询执行来检查版本。 输出应为 "Microsoft SQL Server 2019 (CTP 2.4)-15.0. x"。

通过返回当前与数据库引擎实例一起安装的所有 R 包的格式正确的列表, 检查 R 包的可用性:

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

## <a name="connect-to-the-database"></a>连接到数据库

启动 Management Studio 并连接到数据库引擎实例。 在对象资源管理器中，验证[NYCTaxi_Sample 数据库](demo-data-nyctaxi-in-sql.md)是否存在。 

## <a name="create-calculatedistance"></a>创建 CalculateDistance

演示数据库附带了用于计算距离的标量函数, 但我们的存储过程更适合使用表值函数。 运行以下脚本, 以创建在以后的[培训步骤](#training-step)中使用的**CalculateDistance**函数。

若要确认函数是否已创建，请在对象资源管理器中检查**NYCTaxi_Sample**数据库下的 \Programmability\Functions\Table-valued 函数。

```sql
USE NYCTaxi_sample
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[CalculateDistance] (
    @Lat1 FLOAT
    ,@Long1 FLOAT
    ,@Lat2 FLOAT
    ,@Long2 FLOAT
    )
    -- User-defined function calculates the direct distance between two geographical coordinates.
RETURNS TABLE
AS
RETURN

SELECT COALESCE(3958.75 * ATAN(SQRT(1 - POWER(t.distance, 2)) / nullif(t.distance, 0)), 0) AS direct_distance
FROM (
    VALUES (CAST((SIN(@Lat1 / 57.2958) * SIN(@Lat2 / 57.2958)) + (COS(@Lat1 / 57.2958) * COS(@Lat2 / 57.2958) * COS((@Long2 / 57.2958) - (@Long1 / 57.2958))) AS DECIMAL(28, 10)))
    ) AS t(distance)
GO
 ```

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>定义用于创建和定型每个分区模型的过程

本教程在存储过程中包装 R 脚本。 在此步骤中, 你将创建一个存储过程, 该存储过程使用 R 创建输入数据集, 生成用于预测 tip 结果的分类模型, 然后将该模型存储在数据库中。

在此脚本使用的参数输入中，你将看到**input_data_1_partition_by_columns**和**input_data_1_order_by_columns**。 请记住, 这些参数是进行分区建模所使用的机制。 参数作为输入传递给[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) ，以处理每个分区执行一次的外部脚本的分区。 

对于此存储过程, 请[使用并行度](#parallel)来加快完成时间。

运行此脚本后，应在对象资源管理器中的**NYCTaxi_Sample**数据库下的 \Programmability\Stored 过程中看到**train_rxLogIt_per_partition** 。 还应看到用于存储模型的新表： **nyctaxi_models**。

```sql
USE NYCTaxi_Sample
GO

CREATE
    OR

ALTER PROCEDURE [dbo].[train_rxLogIt_per_partition] (@input_query NVARCHAR(max))
AS
BEGIN
    DECLARE @start DATETIME2 = SYSDATETIME()
        ,@model_generation_duration FLOAT
        ,@model VARBINARY(max)
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name();

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    # Make sure InputDataSet is not empty. In parallel mode, if one thread gets zero data, an error occurs
    if (nrow(InputDataSet) > 0) {
    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    
    # build classification model to predict a tip outcome
    duration <- system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet))[3];

    # First, serialize a model to and put it into a database table
    modelbin <- as.raw(serialize(logitObj, NULL));

    # Create the data source. To reduce data size, add rowsPerRead=500000 to cut the dataset by half.
    ds <- RxOdbcData(table="ml_models", connectionString=connStr);

    # Store the model in the database
    model_name <- paste0("nyctaxi.", InputDataSet[1,]$payment_type);
    
    rxWriteObject(ds, model_name, modelbin, version = "v1",
    keyName = "model_name", valueName = "model_object", versionName = "model_version", overwrite = TRUE, serialize = FALSE);
    } 
    
    '
        ,@input_data_1 = @input_query
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@input_data_1_order_by_columns = N'passenger_count'
        ,@parallel = 1
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS NONE
END;
GO
```

<a name="parallel"></a>

### <a name="parallel-execution"></a>并行执行

请注意， [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)输入包含 `@parallel=1`，用于启用并行处理。 与以前的版本相比，在 SQL Server 2019 中，设置 @no__t 将向查询优化器提供更强的提示，使并行执行更有可能的结果。

默认情况下，查询优化器通常会在256行以上的表中执行 `@parallel=1`，但如果可以通过设置 @no__t （如此脚本中所示）来显式处理此操作。

> [!Tip]
> 对于定型 workoads，可以将 `@parallel` 与任何任意定型脚本（甚至使用非 Microsoft rx 算法的脚本）一起使用。 通常, 只有 RevoScaleR 算法 (带有 rx 前缀) 在 SQL Server 的定型方案中提供并行度。 但对于新参数, 可以并行化一个脚本来调用函数, 包括开源 R 函数, 而不是使用该功能专门设计的。 这样做的原因是，分区与特定线程关联，因此，在脚本中调用的所有操作都是在指定 @ no__t-0<a name="training-step"></a>

## <a name="run-the-procedure-and-train-the-model"></a>运行该过程并训练模型

在本部分中, 该脚本训练你在上一步中创建和保存的模型。 下面的示例演示了两种用于定型模型的方法: 使用整个数据集或部分数据。 

此步骤需要一段时间。 训练是计算密集型的, 需要花费几分钟时间才能完成。 如果系统资源 (尤其是内存) 不足以实现负载, 请使用数据的子集。 第二个示例提供语法。

```sql
--Example 1: train on entire dataset
EXEC train_rxLogIt_per_partition N'
SELECT payment_type, tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

```sql
--Example 2: Train on 20 percent of the dataset to expedite processing.
EXEC train_rxLogIt_per_partition N'
  SELECT tipped, payment_type, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample TABLESAMPLE (20 PERCENT) REPEATABLE (98074)
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

> [!NOTE]
> 如果要运行其他工作负载, 则可以将`OPTION(MAXDOP 2)`查询处理限制为仅限2个核心, 并将其追加到 SELECT 语句。

## <a name="check-results"></a>检查结果

"模型" 表中的结果应为五个不同的模型, 这些模型基于五个付款类型分段的五个分区。 模型在**ml_models**数据源中。

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>定义预测结果的过程

您可以使用相同的参数进行评分。 下面的示例包含 R 脚本, 该脚本将对当前正在处理的分区使用正确的模型进行评分。

与之前一样, 请创建存储过程来包装 R 代码。

```sql
USE NYCTaxi_Sample
GO

-- Stored procedure that scores per partition. 
-- Depending on the partition being processed, a model specific to that partition will be used
CREATE
    OR

ALTER PROCEDURE [dbo].[predict_per_partition]
AS
BEGIN
    DECLARE @predict_duration FLOAT
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name()
        ,@input_query NVARCHAR(max);

    SET @input_query = 'SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance, payment_type
                          FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)
                          CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d'

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    if (nrow(InputDataSet) > 0) {

    #Get the partition that is currently being processed
    current_partition <- InputDataSet[1,]$payment_type;

    #Create the SQL query to select the right model
    query_getModel <- paste0("select model_object from ml_models where model_name = ", "''", "nyctaxi.",InputDataSet[1,]$payment_type,"''", ";")
    

    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
        
    #Define data source to use for getting the model
    ds <- RxOdbcData(sqlQuery = query_getModel, connectionString = connStr)

    # Load the model
    modelbin <- rxReadObject(ds, deserialize = FALSE)
    # unserialize model
    logitObj <- unserialize(modelbin);

    # predict tipped or not based on model
    predictions <- rxPredict(logitObj, data = InputDataSet, overwrite = TRUE, type = "response", writeModelVars = TRUE
        , extraVarsToWrite = c("payment_type"));        
    OutputDataSet <- predictions
    
    } else {
        OutputDataSet <- data.frame(integer(), InputDataSet[,]);        
    }
    '
        ,@input_data_1 = @input_query
        ,@parallel = 1
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS((
                tipped_Pred INT
                ,payment_type VARCHAR(5)
                ,tipped INT
                ,passenger_count INT
                ,trip_distance FLOAT
                ,trip_time_in_secs INT
                ,direct_distance FLOAT
                ));
END;
GO
```

## <a name="create-a-table-to-store-predictions"></a>创建表以存储预测

```sql
CREATE TABLE prediction_results (
    tipped_Pred INT
    ,payment_type VARCHAR(5)
    ,tipped INT
    ,passenger_count INT
    ,trip_distance FLOAT
    ,trip_time_in_secs INT
    ,direct_distance FLOAT
    );

TRUNCATE TABLE prediction_results
GO
```

## <a name="run-the-procedure-and-save-predictions"></a>运行该过程并保存预测

```sql
INSERT INTO prediction_results (
    tipped_Pred
    ,payment_type
    ,tipped
    ,passenger_count
    ,trip_distance
    ,trip_time_in_secs
    ,direct_distance
    )
EXECUTE [predict_per_partition]
GO
```

## <a name="view-predictions"></a>查看预测

由于存储了预测, 因此您可以运行一个简单的查询来返回结果集。

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>后续步骤

在本教程中，你使用了[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)对已分区数据的操作进行迭代。 若要详细了解如何调用存储过程中的外部脚本和使用 RevoScaleR 函数, 请继续学习以下教程。

> [!div class="nextstepaction"]
> [R 和 SQL Server 演练](walkthrough-data-science-end-to-end-walkthrough.md)

<!--
## Old intro

**(Not for production workloads)**

One of the more common approaches for executing R or Python code on SQL data is providing script as an input parameter to the [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure. In this CTP release, SQL Server 2019 adds new parameters to `sp_execute_external_script` to process partitions with the external script executing once for every partition:

| Parameter | Usage |
|-----------|-------|
| **input_data_1_partition_by_columns** | Specifies which columns to partition by. |
| **input_data_1_order_by_columns** | Specifies which columns to order by.  |

Partitions are an organizational mechanism for stratified data that naturally segments into a given classification scheme. Common examples include partitioning by geographic region, by date and time, by age or gender, and so forth. Given the existence of partitioned data, you might want to execute script over the entire data set, with the ability to model, train, and score partitions that remain intact over all these operations. Calling `sp_execute_external_script` with the new parameters allows you to do just that.

You can run this operation in parallel by combining `partition_by` with `@parallel`. If the input query can be parallelized, set `@parallel=1` as part of your arguments to `sp_execute_external_script`. By default, the query optimizer operates under `@parallel=1` on tables having more than 256 rows.

When the scenario is training, one advantage is that any arbitrary training script, even those using non-Microsoft-rx algorithms, can be parallelized by also using the @parallel parameter. Typically, you would have to use RevoScaleR algorithms (with the rx prefix) to obtain parallelism in training scenarios in SQL Server. But with the new parameter, you can parallelize a script that calls functions not specifically engineered with that capability.
-->
