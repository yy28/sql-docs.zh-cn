---
title: 课程 4 预测潜在结果使用 R 模型 （SQL Server 机器学习） |Microsoft Docs
description: 本教程显示如何将 SQL Server 中嵌入的 R 脚本进行操作的存储过程带有 T-SQL 函数
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/30/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8485cd4e24e067cf6a4e6feef0c39c3c3051a166
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032534"
---
# <a name="lesson-4-run-predictions-using-r-embedded-in-a-stored-procedure"></a>第 4 课： 使用 R 运行预测嵌入在存储过程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是有关如何在 SQL Server 中使用 R 的 SQL 开发人员教程的一部分。

在此步骤中，您了解如何使用针对新观测值的模型来预测潜在的结果。 模型包装在可由其他应用程序直接调用的存储过程。 本演练演示了几种方法进行评分：

- **批处理计分模式**： 为存储过程的输入使用 SELECT 查询。 存储过程将返回与输入事例对应的观测表。

- **单个评分模式**：传递一组单独的参数值作为输出。  存储过程将返回单个行或值。

首先，让我们看看一般情况下评分的工作原理。

## <a name="basic-scoring"></a>基本评分

存储的过程**RxPredict**说明了在存储过程中包装的 RevoScaleR rxPredict 调用的基本语法。

```SQL
CREATE PROCEDURE [dbo].[RxPredict] @inquery nvarchar(max) 
AS 
BEGIN 
  
DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);  
EXEC sp_execute_external_script @language = N'R',
  @script = N' 
    mod <- unserialize(as.raw(model)); 
    print(summary(mod)) 
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE); 
    str(OutputDataSet) 
    print(OutputDataSet) 
    ', 
  @input_data_1 = @inquery, 
  @params = N'@model varbinary(max)',
  @model = @lmodel2 
  WITH RESULT SETS ((Score float));
END
GO
```

+ SELECT 语句从数据库中获取序列化的模型并将模型存储在 R 变量`mod`进行进一步的处理使用。

+ 从获取新的用例进行评分[!INCLUDE[tsql](../../includes/tsql-md.md)]中指定查询`@inquery`，存储过程的第一个参数。 读取查询数据时，行保存在默认数据帧 `InputDataSet`中。 此数据帧传递给[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)函数，在[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)，其生成评分。
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    由于数据帧可以包含单个行，你可以使用相同的代码来进行批量或单个评分。
  
+ 返回的值`rxPredict`技术支持部门**float** ，表示该驱动程序获取任何金额的小费的概率。

## <a name="batch-scoring-a-list-of-predictions"></a>批处理评分 （预测列表）

一种更常见方案是在批处理模式下生成多个观察值的预测。 在此步骤中，让我们了解批处理评分的工作原理。

1.  先获取较小的要使用的输入数据集。 此查询创建了“排名前 10”的行程列表，其中需要预测乘客计数和其他功能。
  
    ```SQL
    SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    
    FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

    LEFT OUTER JOIN

    (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime
    WHERE b.medallion IS NULL
    ```

    **示例结果**
    
    ```
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

2. 创建名为存储的过程**RxPredictBatchOutput**中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

    ```SQL
    /****** Object:  StoredProcedure [dbo].[RxPredictBatchOutput]  ******/
    CREATE PROCEDURE [dbo].[RxPredictBatchOutput] @inquery nvarchar(max)
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);
    EXEC sp_execute_external_script 
      @language = N'R',
      @script = N'
        mod <- unserialize(as.raw(model));
        print(summary(mod))
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);
        str(OutputDataSet)
        print(OutputDataSet)
      ',
      @input_data_1 = @inquery,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

3.  提供的变量中的查询文本并将其作为参数传递给存储过程：

    ```SQL
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'

    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[RxPredictBatchOutput] @inquery = @query_string;
    ```
  
存储的过程返回一的系列表示前 10 个行程的每个预测的值。 但是，顶部行程也是使用相对较短的行程距离，为其驱动程序不太可能中获得小费的单乘客行程。
  

> [!TIP]
> 
> 而不是返回的"是提示"和"无小费"的结果，可能也会返回该预测的概率分数，然后将应用到的 WHERE 子句_分数_列的值以将评分分类为"可能小费"或"不可能给小费"，使用如 0.5 或 0.7 阈值。 此步骤不包含在存储过程中，但很容易执行。

## <a name="single-row-scoring-of-multiple-inputs"></a>单行计分的多个输入

有时你想要传递多个输入值并获取单个预测基于这些值。 例如，您可以设置 Excel 工作表、 web 应用程序或 Reporting Services 报表，以调用存储的过程，并提供输入键入或选择的用户从这些应用程序。

在本部分中，您将了解如何创建单个预测使用的存储的过程采用多个输入，例如乘客计数、 行程距离等。 存储的过程创建基于以前存储的 R 模型的分数。
  
如果从外部应用程序调用存储的过程，请确保数据满足 R 模型的要求。 这可能包括确保输入的数据可以被转换为 R 数据类型或验证数据类型和数据长度。 

1. 创建一个存储的过程**RxPredictSingleRow**。
  
    ```SQL
    CREATE PROCEDURE [dbo].[RxPredictSingleRow] @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);
    EXEC sp_execute_external_script  
      @language = N'R',
      @script = N'  
        mod <- unserialize(as.raw(model));  
        print(summary(mod));  
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
        str(OutputDataSet);
        print(OutputDataSet); 
        ',  
      @input_data_1 = @inquery,  
      @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float', @model = @lmodel2, @passenger_count =@passenger_count, @trip_distance=@trip_distance, @trip_time_in_secs=@trip_time_in_secs, @pickup_latitude=@pickup_latitude, @pickup_longitude=@pickup_longitude, @dropoff_latitude=@dropoff_latitude, @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
    END
    ```

2. 通过手动提供值来进行试用。
  
    打开一个新**查询**窗口中，并调用存储过程，为每个参数提供值。 参数表示模型使用的特征列，并且需要。

    ```
    EXEC [dbo].[RxPredictSingleRow] @passenger_count = 0,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = 73.977303
    ```

    或者，使用支持此短格式[存储过程的参数](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```SQL
    EXEC [dbo].[PredictRxMultipleInputs] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. 结果表明获得小费的可能性较低 （零） 在前 10 个不得不来回往返，因为所有通过相对较短的距离都是单乘客行程。

## <a name="conclusions"></a>结论

本步骤将结束教程。 现在，您学习了如何在存储过程中嵌入 R 代码，您可以扩展这些做法，以便生成你自己的模型。 与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成使其更易于部署 R 模型以进行预测，将模型再定型合并为企业数据工作流的一部分也变得更加容易。

## <a name="previous-lesson"></a>上一课

[第 3 课： 训练和保存使用 T-SQL 的 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
