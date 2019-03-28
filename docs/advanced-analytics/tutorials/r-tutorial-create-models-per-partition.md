---
title: 创建、 定型和评分基于分区的模型在 R 中的 SQL Server 机器学习服务教程
description: 了解如何建模、 定型和使用分区时使用的 SQL Server 机器学习基于分区的建模功能动态创建的数据。
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/27/2018
ms.topic: tutorial
ms.author: davidph
author: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7ccdc67413e6714c762d165a8d087b9385a3f5a4
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512164"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>教程：在 SQL Server 上的 R 中创建基于分区的模型
[!INCLUDE[appliesto-ssvnex-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在 SQL Server 2019 基于分区的建模是创建并定型模型对已分区数据的能力。 分层数据的自然段到给定的分类方案-例如地理区域、 日期和时间、 年龄或性别的可执行脚本对整个数据集，能够建模、 定型和评分对保持不变的分区通过所有这些操作。 

通过两个新参数上启用基于分区的建模[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql):

+ **input_data_1_partition_by_columns**，它指定按分区的列。
+ **input_data_1_order_by_columns**指定哪些列进行排序。 

在本教程中，了解基于分区的建模使用经典 NYC 出租车示例数据和 R 脚本。 分区列是付款方法。

> [!div class="checklist"]
> * 分区都基于付款类型 (5)。
> * 创建和训练每个分区上的模型和数据库中存储的对象。
> * 对每个分区模型，使用保留的实现此目的的示例数据预测小费的结果的概率。

## <a name="prerequisites"></a>先决条件
 
若要完成本教程中，您必须具有：

+ 足够的系统资源。 数据集较大和培训操作占用大量资源。 如果可能，请使用具有至少 8 GB RAM 的系统。 或者，可以使用较小的数据集以解决资源限制。 减少数据集的说明将以内联方式。 

+ T-SQL 的一个工具查询执行，例如[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

+ [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)，你可[下载并还原](demo-data-nyctaxi-in-sql.md)到本地数据库引擎实例。 文件大小为约 90 MB。

+ SQL Server 2019 预览版数据库引擎实例中使用机器学习服务和 R 集成。

检查版本，通过执行**`SELECT @@Version`** 作为查询工具中的 T-SQL 查询。 输出应为"Microsoft SQL Server 2019 (CTP 2.4)-15.0.x"。

检查可用性的 R 包通过返回格式正确的数据库引擎实例与当前安装的所有 R 包列表：

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

启动 Management Studio 并连接到数据库引擎实例。 在对象资源管理器，验证是否[NYCTaxi_Sample 数据库](demo-data-nyctaxi-in-sql.md)存在。 

## <a name="create-calculatedistance"></a>创建 CalculateDistance

演示数据库附带了计算距离，但我们的存储的过程的工作原理更好地与表值函数的标量函数。 运行以下脚本来创建**CalculateDistance**函数中使用[培训步骤](#training-step)更高版本上。

若要确认该函数的创建，请检查下的 \Programmability\Functions\Table-valued 函数**NYCTaxi_Sample**在对象资源管理器中的数据库。

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

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>定义用于创建和训练每个分区模型的过程

本教程将 R 脚本包装在存储过程中。 在此步骤中，您创建使用 R 来创建输入数据集、 生成分类模型进行预测小费结果，然后将模型存储在数据库中的存储的过程。

在此脚本使用的参数输入，您将看到**input_data_1_partition_by_columns**并**input_data_1_order_by_columns**。 回想一下，这些参数的机制分区建模会发生。 作为输入传递的参数[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)到与外部脚本执行一次每个分区的处理分区。 

为此存储过程中，[使用并行性](#parallel)的速度更快完成时间。

运行此脚本后，你应该会看到**train_rxLogIt_per_partition** \Programmability\Stored 下的过程中**NYCTaxi_Sample**在对象资源管理器中的数据库。 您还应该查看有关存储模型所用的新表： **dbo.nyctaxi_models**。

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

请注意， [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)输入包括 **@parallel= 1**，可用来启用并行处理。 与早期版本中，在 SQL Server 2019，设置相比 **@parallel= 1**提供更强的提示与查询优化器，使更有可能结果的并行执行。

默认情况下，查询优化器倾向于使用您在运行 **@parallel= 1**对表具有 256 个以上的行，但如果可以处理此显式设置 **@parallel= 1**这中所示脚本。

> [!Tip]
> 可以使用培训 workoads **@parallel**任何任意训练脚本，甚至包括那些使用非 Microsoft rx 算法。 通常情况下，仅 RevoScaleR 算法 （与 rx 前缀） 产品/服务中 SQL Server 中的培训方案的并行度。 但使用新参数，您可以并行化调用函数，包括开放源代码 R 函数，不是专门设计，提供该功能的脚本。 这有效，因为分区具有关联到特定的线程，因此在每个分区模式中，在给定的线程上执行所有操作在脚本中调用。

<a name="training-step"></a>

## <a name="run-the-procedure-and-train-the-model"></a>运行过程，并为模型定型

在本部分中，脚本创建和上一步中保存的模型进行定型。 下面的示例演示用于训练模型的两种方法： 使用整个数据集或使用部分数据。 

需要此步骤，需要一些时间。 训练速度就计算很密集，采用很多分钟才能完成。 如果系统资源，尤其是内存不足，无法加载，请使用数据的子集。 第二个示例提供了语法。

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
> 如果你正在运行其他工作负荷，你可以将附加`OPTION(MAXDOP 2)`到 SELECT 语句，如果你想要限制为只需 2 个核心的查询处理。

## <a name="check-results"></a>检查结果

模型表中的结果应基于由五个付款类型划分的五个分区的五个不同的模型。 模型以**ml_models**数据源。

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>定义用于预测结果的过程

进行评分，可以使用相同的参数。 下面的示例包含 R 脚本，以将当前正在处理的分区使用正确的模型评分。

与前面一样，创建一个存储的过程以将 R 代码。

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

## <a name="create-a-table-to-store-predictions"></a>创建用于存储预测的表

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

## <a name="run-the-procedure-and-save-predictions"></a>运行过程和保存预测

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

由于存储预测，您可以运行简单查询以返回结果集。

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>后续步骤

在本教程中，您使用[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)要循环访问的分区数据的操作。 对于仔细查看存储过程中调用外部脚本并使用 RevoScaleR 函数，请继续学习以下教程。

> [!div class="nextstepaction"]
> [适用于 R 和 SQL Server 的演练](walkthrough-data-science-end-to-end-walkthrough.md)

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
