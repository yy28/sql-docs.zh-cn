---
title: 第4课使用 R 模型预测潜在结果
description: 介绍如何在 SQL Server 带有 T-sql 函数的存储过程中操作嵌入式 R 脚本的教程
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 159fb29bf560e755fdc605330d7d20369f55ba08
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345897"
---
# <a name="lesson-4-run-predictions-using-r-embedded-in-a-stored-procedure"></a>第 4 课：使用存储过程中嵌入的 R 运行预测
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是有关如何在 SQL Server 中使用 R 的 SQL 开发人员教程的一部分。

在此步骤中, 您将了解如何针对新的观测值使用该模型来预测潜在的结果。 模型包装在存储过程中, 该存储过程可由其他应用程序直接调用。 本演练演示了执行评分的几种方法:

- **批处理计分模式**:使用 SELECT 查询作为存储过程的输入。 存储过程将返回与输入事例对应的观测表。

- **单个计分模式**:作为输入传递一组单独的参数值。  存储过程将返回单个行或值。

首先，让我们看看一般情况下评分的工作原理。

## <a name="basic-scoring"></a>基本评分

存储过程**RxPredict**说明了在存储过程中包装 RevoScaleR RxPredict 调用的基本语法。

```sql
CREATE PROCEDURE [dbo].[RxPredict] (@model varchar(250), @inquery nvarchar(max))
AS 
BEGIN 

DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);  
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

+ SELECT 语句从数据库获取序列化模型, 并将该模型存储在 r 变量`mod`中, 以供使用 r 进行进一步处理。

+ 评分的新用例是从[!INCLUDE[tsql](../../includes/tsql-md.md)]中`@inquery`指定的查询获得的, 该存储过程的第一个参数。 读取查询数据时，行保存在默认数据帧 `InputDataSet`中。 此数据帧传递到[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)中的[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)函数, 这将生成分数。
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    由于数据帧可以包含单个行，你可以使用相同的代码来进行批量或单个评分。
  
+ `rxPredict`函数返回的值是一个**浮点**值, 它表示驱动程序获取任何量提示的概率。

## <a name="batch-scoring-a-list-of-predictions"></a>批处理评分 (预测列表)

更常见的情况是在批处理模式下为多个观察生成预测。 在此步骤中, 我们来看一下批处理评分的工作原理。

1.  首先, 获取一组较小的要使用的输入数据。 此查询创建了“排名前 10”的行程列表，其中需要预测乘客计数和其他功能。
  
    ```sql
    SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    
    FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

    LEFT OUTER JOIN

    (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime
    WHERE b.medallion IS NULL
    ```

    **示例结果**
    
    ```sql
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

2. 在中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]创建名为**RxPredictBatchOutput**的存储过程。

    ```sql
    CREATE PROCEDURE [dbo].[RxPredictBatchOutput] (@model varchar(250), @inquery nvarchar(max))
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
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

3.  提供变量中的查询文本, 并将其作为参数传递给存储过程:

    ```sql
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'
    
    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[RxPredictBatchOutput] @model = 'RxTrainLogit_model', @inquery = @query_string;
    ```
  
该存储过程将返回一系列值, 这些值表示前10次行程的预测。 但是, 最大行程的行程也是相对较短的乘客行程, 驱动程序不太可能获得提示。
  

> [!TIP]
> 
> 你还可以返回预测的概率分数, 然后将 WHERE 子句应用于_分数_列值, 以将分数归类为 "有可能提示" 或 "不太可能", 而不是仅返回 "yes-tip" 和 "no 刀尖" 结果, 并使用阈值, 例如0.5 或0.7。 此步骤不包含在存储过程中，但很容易执行。

## <a name="single-row-scoring-of-multiple-inputs"></a>多个输入的单行评分

有时, 您想要传入多个输入值并基于这些值获取单个预测。 例如, 您可以设置一个 Excel 工作表、web 应用程序或 Reporting Services 报表来调用存储过程, 并提供这些应用程序中用户键入或选择的输入。

在本部分中, 将了解如何使用存储过程创建单个预测, 该存储过程采用多个输入, 例如乘客计数、行程距离等。 该存储过程基于之前存储的 R 模型创建分数。
  
如果从外部应用程序调用存储过程, 请确保数据符合 R 模型的要求。 这可能包括确保输入的数据可以被转换为 R 数据类型或验证数据类型和数据长度。 

1. 创建存储过程**RxPredictSingleRow**。
  
    ```sql
    CREATE PROCEDURE [dbo].[RxPredictSingleRow] @model varchar(50), @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
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
  
    打开一个新的**查询**窗口, 然后调用存储过程, 并为每个参数提供值。 参数表示模型所使用的功能列, 并且是必需的。

    ```sql
    EXEC [dbo].[RxPredictSingleRow] @model = 'RxTrainLogit_model',
    @passenger_count = 1,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = -73.977303
    ```

    或者, 为[存储过程的参数](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters)使用此更短的格式:
  
    ```sql
    EXEC [dbo].[RxPredictSingleRow] 'RxTrainLogit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. 结果表明, 在这前10次行程中获得笔尖的概率很低 (零), 因为所有这些都是相对较短的距离。

## <a name="conclusions"></a>结论

本步骤将结束教程。 现在, 你已了解如何将 R 代码嵌入到存储过程中, 你可以扩展这些方法来生成自己的模型。 与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成使其更易于部署 R 模型以进行预测，将模型再定型合并为企业数据工作流的一部分也变得更加容易。

## <a name="previous-lesson"></a>上一课

[第 3 课：使用 T-sql 定型和保存 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
