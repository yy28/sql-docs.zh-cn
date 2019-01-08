---
title: 将 SQL Server-SQL Server 机器学习预测 R 模型部署
description: 本教程演示如何部署 SQL Server 上的数据库内分析 R 模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7b14b70fc5ba8ac39535d9dd6dedbfa1bd309aa4
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645187"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>将 R 模型部署和使用 SQL Server （演练） 中
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本课中，了解如何通过从存储过程调用已训练的模型部署在生产环境中的 R 模型。 可以调用 R 或支持的任何应用程序编程语言中的存储的过程[!INCLUDE[tsql](../../includes/tsql-md.md)](如C#、 Java、 Python 等) 和使用模型对新观测值进行预测。

本文演示如何使用评分中的模型的两种最常见方法：

> [!div class="checklist"]
> * **批处理计分模式**生成多个预测
> * **单个评分模式**一次生成一个预测

## <a name="batch-scoring"></a>批处理计分

创建一个存储的过程*PredictTipBatchMode*，生成多个预测，将 SQL 查询或表作为输入传递。 结果将返回一个表，你可能会直接向表中插入或写入文件。

- 以 SQL 查询的形式获取一组输入数据
- 调用在上一课中保存的已定型逻辑回归模型
- 预测概率驱动程序获取任何非零值提示

1. 在 Management Studio 中打开新查询窗口并运行下面的 T-SQL 脚本，以创建 PredictTipBatchMode 存储过程。
  
    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipBatchMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @input nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  FROM nyc_taxi_models);
      EXEC sp_execute_external_script @language = N'R',
         @script = N'
           mod <- unserialize(as.raw(model));
           print(summary(mod))
           OutputDataSet<-rxPredict(modelObject = mod,
             data = InputDataSet,
             outData = NULL,
             predVarNames = "Score", type = "response",
             writeModelVars = FALSE, overwrite = TRUE);
           str(OutputDataSet)
           print(OutputDataSet)',
      @input_data_1 = @input,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

    + 使用 SELECT 语句调用从 SQL 表存储的模型。 从作为表中检索模型**varbinary （max)** SQL 变量中存储的数据 _\@lmodel2_，并作为参数传递*mod*到系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    + 评分是定义为 SQL 查询，以在 SQL 变量字符串存储在用作输入的数据_\@输入_。 从数据库检索数据，因为它存储在名为的数据帧*InputDataSet*，这就是默认名称的输入数据[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)过程; 可以定义如果需要通过使用参数的另一个变量名称  *_\@input_data_1_name_*。

    + 为了生成分数，存储的过程调用中的 rxPredict 函数**RevoScaleR**库。

    + 返回值*分数*，是概率，给定模型，该驱动程序获取一条提示。 （可选） 可以轻松将某种类型的筛选器应用于返回值，以将返回值分类为"提示"和"无小费"组。  例如，概率小于 0.5 意味着提示是不可能。
  
2.  若要在批处理模式下调用存储的过程，您定义作为存储过程的输入所需的查询。 下面是可以在以验证它正常工作的 SSMS 中运行的 SQL 查询。

    ```sql
    SELECT TOP 10
      a.passenger_count AS passenger_count,
      a.trip_time_in_secs AS trip_time_in_secs,
      a.trip_distance AS trip_distance,
      a.dropoff_datetime AS dropoff_datetime,
      dbo.fnCalculateDistance( pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance
      FROM 
        (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude 
        FROM nyctaxi_sample)a 
      LEFT OUTER JOIN
      ( SELECT medallion, hack_license, pickup_datetime
      FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b
      ON a.medallion=b.medallion
      AND a.hack_license=b.hack_license
      AND a.pickup_datetime=b.pickup_datetime
      WHERE b.medallion is null
    ```

3. 使用以下 R 代码以从 SQL 查询创建输入的字符串：

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. 若要从 R 运行存储的过程，调用**sqlQuery**方法**RODBC**包并使用 SQL 连接`conn`先前定义：

    ```R
    sqlQuery (conn, q);
    ```

    如果获取了 ODBC 错误，请检查语法错误以及您是否具有适当数量的引号。 
    
    如果遇到权限错误，请确保该登录名具有执行该存储的过程的能力。

## <a name="single-row-scoring"></a>单行计分

单个评分模式将生成一个预测时，将一组的单个值传递给存储过程作为输入。 值对应于该模型使用来创建预测，该模型中的功能，或生成如概率值的另一个结果。 然后可以将该值返回到应用程序或用户。

当调用基于行的行的预测模型，您传递值表示为每个单独的用例的功能的一的组。 存储的过程然后返回单个预测或概率。 

存储的过程*PredictTipSingleMode*展示这种方法。 它将作为输入多个参数表示功能值 （例如，乘客计数和行程距离），使用存储的 R 模型，这些功能进行评分并输出提示概率。

1. 运行下面的 TRANSACT-SQL 语句，以创建存储的过程。

    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipSingleMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0,
    @trip_distance float = 0,
    @trip_time_in_secs int = 0,
    @pickup_latitude float = 0,
    @pickup_longitude float = 0,
    @dropoff_latitude float = 0,
    @dropoff_longitude float = 0
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs, @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)'
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);

      EXEC sp_execute_external_script @language = N'R',  @script = N'
            mod <- unserialize(as.raw(model));
            print(summary(mod))
            OutputDataSet<-rxPredict(
              modelObject = mod,
              data = InputDataSet,
              outData = NULL,
              predVarNames = "Score",
              type = "response",
              writeModelVars = FALSE,
              overwrite = TRUE);
            str(OutputDataSet)
            print(OutputDataSet)
            ',
      @input_data_1 = @inquery,
      @params = N'
      -- passthrough columns
      @model varbinary(max) ,
      @passenger_count int ,
      @trip_distance float ,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      -- mapped variables
      @model = @lmodel2 ,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance ,
      @trip_time_in_secs=@trip_time_in_secs ,
      @pickup_latitude=@pickup_latitude ,
      @pickup_longitude=@pickup_longitude ,
      @dropoff_latitude=@dropoff_latitude ,
      @dropoff_longitude=@dropoff_longitude
      WITH RESULT SETS ((Score float));
    END
    ```

2. 在 SQL Server Management Studio，你可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC**过程 (或**EXECUTE**) 来调用存储的过程，并将其传递所需的输入。 例如，请尝试在 Management Studio 中运行此语句：

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    在此处传递的值分别是变量_乘客\_计数_， _trip_distance_，_行程\_时间\_中\_秒_， _pickup\_纬度_， _pickup\_经度_，_下车\_纬度_，并_下车\_经度_。

3. 若要从 R 代码运行此相同的调用，只需定义包含整个存储的过程调用，如下一个 R 变量：

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    在此处传递的值分别是变量_乘客\_计数_，_行程\_距离_，_行程\_时间\_中\_秒_， _pickup\_纬度_， _pickup\_经度_，_下车\_纬度_，并_下车\_经度_。

4. 调用`sqlQuery`(从**RODBC**包)，并将传递连接字符串，以及包含存储的过程调用的字符串变量。

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > R 工具的 Visual Studio (RTVS) 提供了极好的集成，与 SQL Server 和。请参阅本文了解 SQL Server 连接上使用 RODBC 的更多示例：[使用 SQL Server 和 R](https://docs.microsoft.com/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>后续步骤

现在，已了解如何使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据和持久保存已定型的 R 模型到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，它应该为你创建基于此数据集的新模型相对容易。 例如，可能会尝试创建这些附加的模型：

+ 预测小费金额的回归模型
+ 预测小费是否是大、 中或小的多类分类模型

您可能想要了解这些其他示例和资源：

+ [数据科学方案和解决方案模板](data-science-scenarios-and-solution-templates.md)
+ [数据库内高级分析](sqldev-in-database-r-for-sql-developers.md)
+ [Microsoft R - Diving into Data Analysis](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)
+ [其他资源](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)
