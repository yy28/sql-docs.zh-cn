---
title: "第 6 课： 具有可操作性 R 模型 |Microsoft 文档"
ms.custom: 
ms.date: 08/23/2016
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
- TSQL
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0fbdebc582650b0bd524d583d936848ae42e5f6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-6-operationalize-the-r-model"></a>第 6 课： 具有可操作性 R 模型

本文是教程的有关如何在 SQL Server 中使用 R 的 SQL 开发人员的一部分。

在此步骤中，您学习*具有可操作性*模型时使用存储的过程。 此存储过程可由其他应用程序直接调用，以就新的观测进行预测。 本演练演示了两种方法执行存储过程中使用 R 模型评分：

- **批量计分模式**: SELECT 查询用作存储过程的输入。 存储过程将返回与输入事例对应的观测表。

- **单个评分模式**：传递一组单独的参数值作为输出。  存储过程将返回单个行或值。

首先，让我们看看一般情况下评分的工作原理。

## <a name="basic-scoring"></a>基本评分

存储过程 _PredictTip_ 说明了在存储过程中包装预测调用的基本语法。

```SQL
CREATE PROCEDURE [dbo].[PredictTip] @inquery nvarchar(max)  
AS  
BEGIN  
  
  DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
  FROM nyc_taxi_models);  
  EXEC sp_execute_external_script @language = N'R',  
                                  @script = N'  
mod <- unserialize(as.raw(model));  
print(summary(mod))  
OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
          predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
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

- SELECT 语句从数据库中获取序列化的模型，并将模型存储在 R 变量 `mod` 中以便使用 R 对其进行进一步处理。

- 获取新用例以获得评分[!INCLUDE[tsql](../../includes/tsql-md.md)]中指定查询`@inquery`，存储过程的第一个参数。 读取查询数据时，行保存在默认数据帧 `InputDataSet`中。 此数据帧将被传递给 R 中的 `rxPredict` 函数，该函数将生成评分。
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,            predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    由于数据帧可以包含单个行，你可以使用相同的代码来进行批量或单个评分。
  
-   返回的值`rxPredict`函数是**float**表示该驱动程序获取任意数量的提示的概率。

## <a name="batch-scoring"></a>批处理评分

现在让我们看看批量评分的工作原理。

1.  我们先获取要处理的较小输入数据集。 此查询创建了“排名前 10”的行程列表，其中需要预测乘客计数和其他功能。
  
    ```SQL
    SELECT TOP 10 a.passenger_count AS passenger_count,
        a.trip_time_in_secs AS trip_time_in_secs, 
        a.trip_distance AS trip_distance, 
        a.dropoff_datetime AS dropoff_datetime, 
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    FROM
    (
        SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,
         dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a
    LEFT OUTERJOIN
    (
    SELECT medallion, hack_license, pickup_datetime
    FROM nyctaxi_sample
    TABLESAMPLE (70 percent) REPEATABLE (98052)
    )b
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

    此查询可以用作存储的过程中，输入_PredictTipBatchMode_、 下载中提供。

2. 花点时间查看存储过程的代码_PredictTipBatchMode_中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

    ```SQL
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model
      FROM nyc_taxi_models);
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
    ```

3.  提供在变量中的查询文本，并将其作为参数传递到存储过程：

    ```SQL
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='
    select top 10 a.passenger_count as passenger_count,
        a.trip_time_in_secs as trip_time_in_secs,
        a.trip_distance as trip_distance,
        a.dropoff_datetime as dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance
    from
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
        from nyctaxi_sample
    )a  
    LEFT OUTER JOIN
    (
    SELECT medallion, hack_license, pickup_datetime
    FROM nyctaxi_sample  
    TABLESAMPLE (70 percent) REPEATABLE (98052)
    )b 
    ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime  
    WHERE b.medallion is null'

    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[PredictTip] @inquery = @query_string;
    ```
  
4. 存储的过程返回一的系列表示的前 10 个行程的每个预测的值。 但是，顶部行程也是单乘客行程相对较短的行程距离，为其驱动程序不太可能获取一条提示。
  

> [!TIP]
> 
> 你可能还会返回该预测的概率评分（而不是返回有小费/无小费的结果），然后将一个 WHERE 子句应用到 _分数_ 列的值以使用如 0.5 或 0.7 之类的阈值将评分分类为“可能会给小费”或“不可能给小费”。 此步骤不包含在存储过程中，但很容易执行。

## <a name="single-row-scoring"></a>单行评分

有时你想要从应用程序以单一值传递并基于这些值获取单个结果。 例如，你可以设置 Excel 工作表、Web 应用程序或 Reporting Services 报表，以调用存储过程和提供用户键入或选择的输入信息。

在本部分中，你将了解如何创建使用存储的过程的单个预测。

1. 花点时间查看存储过程 _PredictTipSingleMode_的代码，它作为下载的一部分提供。
  
    ```SQL
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
      SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count,  
    @trip_distance,  
    @trip_time_in_secs,  
    @pickup_latitude,  
    @pickup_longitude,  
    @dropoff_latitude,  
    @dropoff_longitude)  
        '  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
      FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
    mod <- unserialize(as.raw(model));  
    print(summary(mod))  
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
              predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
    str(OutputDataSet)  
    print(OutputDataSet)  
    ',  
    @input_data_1 = @inquery,  
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  
    @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float',  
    @model = @lmodel2,  
    @passenger_count =@passenger_count ,  
    @trip_distance=@trip_distance,  
    @trip_time_in_secs=@trip_time_in_secs,    
    @pickup_latitude=@pickup_latitude,  
    @pickup_longitude=@pickup_longitude,  
    @dropoff_latitude=@dropoff_latitude,  
    @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
    END
    ```
  
    - 此存储过程将多个单一值作为输入，例如乘客计数、行程距离等。
  
        如果从外部应用程序调用存储过程，请确保数据满足 R 模型的要求。 这可能包括确保输入的数据可以被转换为 R 数据类型或验证数据类型和数据长度。 有关详细信息，请参阅 [使用 R 数据类型](https://msdn.microsoft.com/library/mt590948.aspx)。
  
    -   存储过程根据存储的 R 模型创建评分。
  
2. 通过手动提供值来进行试用。
  
    打开一个新**查询**窗口中，并调用存储过程，为每个参数提供值。 参数表示模型使用的特征列，并且需要。

    ```
    EXEC [dbo].[PredictTipSingleMode] @passenger_count = 0,
    @trip_distance float = 2.5,
    @trip_time_in_secs int = 631,
    @pickup_latitude float = 40.763958,
    @pickup_longitude float = -73.973373,
    @dropoff_latitude float =  40.782139,
    @dropoff_longitude float = 73.977303
    ```

    或者，使用此较短形式的受支持[到存储过程的参数](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. 结果指示获取一条提示的概率是在这些前的 10 旅行，非常低，因为所有跨相对较短的距离是单乘客行程。

## <a name="conclusions"></a>结论

本步骤将结束教程。 现在，您学习了如何将 R 代码嵌入在存储过程中，你可以扩展这些做法来构建你自己的模型。 与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成使其更易于部署 R 模型以进行预测，将模型再定型合并为企业数据工作流的一部分也变得更加容易。

## <a name="previous-lesson"></a>上一课

[第 5 课： 训练和保存使用 T-SQL 的 R 模型](../r/sqldev-train-and-save-a-model-using-t-sql.md)

