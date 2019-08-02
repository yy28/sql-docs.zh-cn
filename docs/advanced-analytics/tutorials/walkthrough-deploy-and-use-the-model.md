---
title: 部署 R 模型以便预测 SQL Server
description: 介绍如何在 SQL Server 上为数据库内分析部署 R 模型的教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: aba6990fbed5b24d63d4ab5c16e192718aeff305
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714683"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>部署 R 模型并在 SQL Server 中使用它 (演练)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本课程中, 将了解如何通过从存储过程调用训练的模型在生产环境中部署 R 模型。 可以从 R 或支持[!INCLUDE[tsql](../../includes/tsql-md.md)]的任何应用程序编程语言 (如C#、Java、Python 等) 调用存储过程, 并使用该模型对新观测值进行预测。

本文介绍使用模型的两种最常见的方法:

> [!div class="checklist"]
> * **批处理计分模式**生成多个预测
> * **单个计分模式**一次生成一个预测

## <a name="batch-scoring"></a>批处理评分

创建一个存储过程*PredictTipBatchMode*, 该存储过程将生成多个预测, 并将 SQL 查询或表作为输入传递。 返回结果表, 你可以直接将其插入到表中或写入文件。

- 以 SQL 查询的形式获取一组输入数据
- 调用在上一课中保存的已定型逻辑回归模型
- 预测驱动程序获取任何非零提示的概率

1. 在 Management Studio 中, 打开一个新的查询窗口, 然后运行以下 T-sql 脚本来创建 PredictTipBatchMode 存储过程。
  
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

    + 使用 SELECT 语句从 SQL 表调用存储的模型。 将从表中检索模型作为**varbinary (max)** 数据, 存储在 SQL 变量 _\@lmodel2_中, 并将其作为参数*mod*传递给系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    + 用作计分输入的数据定义为 sql 查询, 并作为字符串存储在 sql 变量 _\@输入_中。 从数据库检索数据，因为它存储在名为的数据帧*InputDataSet*，这就是默认名称的输入数据[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)过程; 可以定义如果需要通过使用参数的另一个变量名称 *_\@input_data_1_name_* 。

    + 为了生成分数, 存储过程会从**RevoScaleR**库调用 rxPredict 函数。

    + 返回值为*评分*, 表示该驱动程序获取提示的概率 (给定型号)。 或者, 您可以轻松地对返回值应用某种类型的筛选器, 以将返回值分类为 "tip" 和 "no tip" 组。  例如, 小于0.5 的概率表示不太可能出现提示。
  
2.  若要在批处理模式下调用存储过程, 需将查询定义为存储过程的输入。 下面是可以在 SSMS 中运行的 SQL 查询, 用于验证它是否正常工作。

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

3. 使用此 R 代码从 SQL 查询创建输入字符串:

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @input = ", input, sep="");
    ```

4. 若要从 R 运行存储过程, 请调用**RODBC**包的**sqlQuery**方法, 并使用之前定义的`conn` SQL 连接:

    ```R
    sqlQuery (conn, q);
    ```

    如果收到 ODBC 错误, 请检查语法错误以及是否有正确的引号数。 
    
    如果出现权限错误, 请确保该登录名能够执行存储过程。

## <a name="single-row-scoring"></a>单行评分

单个计分模式一次生成一个预测, 并将一组单独值作为输入传递给存储过程。 这些值对应于模型中的功能, 模型使用该模型来创建预测, 或生成其他结果, 如概率值。 然后, 可以将该值返回给应用程序或用户。

逐行调用模型进行预测时, 将传递一组表示每个单独事例的功能的值。 然后, 该存储过程返回单个预测或概率。 

存储过程*PredictTipSingleMode*演示了这种方法。 它采用多个表示功能值的参数 (例如, 乘客计数和行程距离), 使用存储的 R 模型对这些特征进行评分, 并输出刀尖概率。

1. 运行下面的 Transact-sql 语句来创建存储过程。

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

2. 在 SQL Server Management Studio 中, 可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC**过程 (或**执行**) 调用存储过程, 并向其传递所需的输入。 例如, 尝试在 Management Studio 中运行以下语句:

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    此处传递的值分别用于变量 _\_乘客 count_、 _\_\_trip_distance、行程时间\_(秒_)、 _\_分拣纬度_、_pickup\_经度_、 _下车\_纬度_和_下车\_经度_。

3. 若要从 R 代码运行相同的调用, 只需定义一个包含整个存储过程调用的 R 变量, 如下所示:

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    此处传递的值分别用于变量_乘客\_计数_、 _\_行程_ _\_\_\__ _距离、行程时间(以秒计)\_纬度_、_拾\_经度_、_下车\_纬度_和_下车\_经度_。

4. 从`sqlQuery` **RODBC**包调用, 并传递连接字符串和包含存储过程调用的字符串变量。

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > 针对 Visual Studio 的 R 工具 (RTVS) 可与 SQL Server 和 R 提供很好的集成。有关将 RODBC 与 SQL Server 连接结合使用的更多示例, 请参阅此文章:[使用 SQL Server 和 R](https://docs.microsoft.com/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>后续步骤

现在, 你已了解如何使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据并将定型 R 模型保存到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 因此, 你可以相对简单地根据此数据集创建新模型。 例如, 你可以尝试创建以下其他模型:

+ 预测小费金额的回归模型
+ 预测 tip 是大、中还是小的多类分类模型

你可能还需要浏览这些附加示例和资源:

+ [数据科学方案和解决方案模板](data-science-scenarios-and-solution-templates.md)
+ [数据库内高级分析](sqldev-in-database-r-for-sql-developers.md)
+ [Machine Learning Server 操作方法指南](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)
+ [Machine Learning Server 其他资源](https://docs.microsoft.com//machine-learning-server/resources-more)
