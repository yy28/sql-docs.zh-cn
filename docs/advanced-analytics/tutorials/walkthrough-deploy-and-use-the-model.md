---
title: "将 R 模型部署和使用在 SQL （演练） |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: f28a7aac-6d08-4781-ad28-b48d18cc16a0
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 41c2caf816ca412e4a6048713dc66f97da5155ae
ms.openlocfilehash: 5d37c9150d19c3e39ea76b48fb0453d159ca0f44
ms.contentlocale: zh-cn
ms.lasthandoff: 10/07/2017

---
# <a name="deploy-the-r-model-and-use-it-in-sql"></a>部署 R 模型，在 SQL 中使用它

在本课程中，你使用 R 模型在生产环境中，通过调用存储过程从训练的模型。 然后，你可以调用存储的过程从 R 或支持的任何应用程序编程语言[!INCLUDE[tsql](../../includes/tsql-md.md)]（如 C#、 Java、 Python 等），以使用模型来进行新的观测值的预测。

此示例演示如何使用中评分的模型的两种最常见方法：

- **批量计分模式**时你需要创建多个预测非常快，通过传递 SQL 查询或表作为输入使用。 结果将返回一个表，你可能直接向表中插入或写入到的文件。

- **单个评分模式**需要进行一次创建一个预测时使用。 将一组的单个值传递到存储过程中。 值对应于功能在模型中，用于创建预测模型，或生成另一个结果，例如概率值。 然后可以将该值返回到应用程序或用户。

## <a name="batch-scoring"></a>批处理评分

你最初运行 PowerShell 脚本时，已创建一个存储的过程作为批处理评分。 该存储过程， *PredictTipBatchMode*，执行下列任务：

- 以 SQL 查询的形式获取一组输入数据
- 调用在上一课中保存的已定型逻辑回归模型
- 预测的概率驱动程序获取任何非零提示

1. 花一些时间来查看存储过程的脚本*PredictTipBatchMode*。 它说明了如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]实施模型的几个方面。
  
    ```tsql
    CREATE PROCEDURE [dbo].[PredictTipBatchMode]
    @input nvarchar(max)
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

    + 使用 SELECT 语句调用从 SQL 表的存储的模型。 从作为表中检索模型**varbinary （max)** SQL 变量中存储的数据 _@lmodel2_ ，作为参数传递和*mod*到存储的系统过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    + 计分已定义为 SQL 查询，存储作为 SQL 变量中的字符串用作输入的数据 _@input_ 。 从数据库检索数据时，它存储在数据帧调用*InputDataSet*，这就是默认名称为输入数据传送到[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)过程; 你可以定义如果需要使用参数的其他变量名 _@input\_数据\_1\_名称_。

    + 为了生成分数，存储过程会从 `rxPredict` RevoScaleR **库调用** 函数。

    + 返回值，*分数*，是概率，给定模型，该驱动程序获取一条提示。 （可选） 你可以轻松地应用某种类型的筛选器，为返回的值，以将返回值分类为"提示"和"不提示"组。  例如，概率小于 0.5，则表示一条提示不太可能。
  
2.  若要在批处理模式下调用存储的过程，你可以定义作为存储过程的输入所需的查询。 下面是 SQL 查询中;SSMS 中用于验证其工作，可以运行它。

    ```SQL
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

3. 使用此 R 代码来创建 SQL 查询从输入的字符串：

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. 若要从 R 运行存储的过程，调用**sqlQuery**方法**RODBC**打包并使用 SQL 连接`conn`前面定义：

    ```R
    sqlQuery (conn, q);
    ```

    如果你遇到 ODBC 错误，请检查查询语法中，以及是否必须适当数量的引号引起来。 
    
    如果你收到权限错误，请确保的登录帐户具有执行存储的过程的能力。

## <a name="single-row-scoring"></a>单个行评分

当调用基于行的行的预测模型，您传递的值表示每个单独的情况下的功能集。 存储的过程然后返回单个预测或概率。 

存储的过程*PredictTipSingleMode*演示此方法。 它将作为输入多个参数表示功能值 （例如，乘客计数和行程距离）、 评分使用存储的 R 模型，这些功能和输出的提示概率。

1. 如果存储的过程*PredictTipSingleMode*未创建此初始的 PowerShell 脚本，可以运行下面的 TRANSACT-SQL 语句，立即创建。

    ```tsql
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

2. 在 SQL Server Management Studio，你可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC**过程 (或**执行**) 调用存储的过程，并将其传递所需的输入。 例如，请尝试在 Management Studio 中运行此语句：

    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    在此处传递的值分别是变量_乘客\_计数_， _trip_distance_，_行程\_时间\_中\_秒_，_拾取\_纬度_，_拾取\_经度_， _dropoff\_纬度_，和_dropoff\_经度_。

3. 若要从 R 代码运行此相同的调用，只需定义包含整个存储的过程调用，如下所示的 R 变量：

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    在此处传递的值分别是变量_乘客\_计数_，_行程\_距离_，_行程\_时间\_中\_秒_，_拾取\_纬度_，_拾取\_经度_， _dropoff\_纬度_，和_dropoff\_经度_。

4. 调用`sqlQuery`(从**RODBC**包)，并将传递连接字符串，以及包含存储的过程调用的字符串变量。

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > R 工具的 Visual Studio (RTVS) 提供极好的集成与 SQL Server 和。请参阅此文章，以使用 SQL Server 连接使用 RODBC 更多示例：[使用 SQL Server 和 R](https://docs.microsoft.com/en-us/visualstudio/rtvs/sql-server)

## <a name="summary"></a>摘要

现在，你已了解如何使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据并将保留到训练的 R 模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，它应为你创建基于此数据集的新模型相对简单。 例如，你可以尝试创建这些其他模型：

- 预测小费金额的回归模型

- 用于预测提示是大、 中或小的多类分类模型

我们还建议你查看一些其他示例和资源：

+ [数据科学方案和解决方案模板](data-science-scenarios-and-solution-templates.md)

+ [数据库内高级分析](sqldev-in-database-r-for-sql-developers.md)

+ [Microsoft R - Diving into Data Analysis](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)

+ [Additional Resources](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)

## <a name="previous-lesson"></a>上一课

[生成 R 模型并将其保存在 SQL Server](walkthrough-build-and-save-the-model.md)

## <a name="next-steps"></a>后续步骤

[SQL Server R 教程](sql-server-r-tutorials.md)

[如何创建存储的过程，请使用 sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)

