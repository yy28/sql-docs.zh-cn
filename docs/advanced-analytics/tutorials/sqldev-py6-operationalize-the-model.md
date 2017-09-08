---
title: "步骤 6： 实施该模型 |Microsoft 文档"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b33f3876f054d7e7150a18967d5cfa37dd2d82bf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="step-6-operationalize-the-model"></a>步骤 6：操作模型

在此步骤中，你将了解到*具有可操作性*定型和上一步中保存的模型。 在这种情况下具有可操作性"将模型部署到生产评分"的方式。 这是很简单的操作如果 Python 代码包含在存储过程。 然后可以从应用程序，在新的观测值进行预测来调用存储的过程。

你将了解从存储过程调用 Python 模型的两个方法：

- **批量评分模式**：使用 SELECT 查询提供多行数据。 存储过程将返回与输入事例对应的观测表。
- **单个评分模式**：传递一组单独的参数值作为输出。  存储过程将返回单个行或值。

## <a name="scoring-using-the-scikit-learn-model"></a>评分使用 scikit-了解模型

存储的过程_PredictTipSciKitPy_使用 scikit-学习模型。 此存储的过程说明了 Python 预测调用包装在存储过程的基本语法。

- 要使用的模型的名称是作为输入参数提供给该存储过程。 
- 存储的过程将从数据库表然后加载序列化的模型`nyc_taxi_models`.table，存储过程中使用 SELECT 语句。
- Python 变量中存储的序列化的模型`mod`进行进一步处理使用 Python。
- 从获取需要要评分的新用例[!INCLUDE[tsql](../../includes/tsql-md.md)]中指定查询`@input_data_1`。 读取查询数据时，行保存在默认数据帧 `InputDataSet`中。
- 此数据帧传递给`predict_proba`函数的逻辑回归模型， `mod`，这由使用 scikit-学习模型。 
- `predict_proba`函数 (`probArray = mod.predict_proba(X)`) 返回**float**表示 （的任意数量） 的提示将得到的概率。
- 存储的过程还计算准确性度量值，AUC （曲线下的区域）。 如果你还提供目标标签 （即附属列），则仅可以生成准确性度量值，如 AUC。 预测不需要目标标签 (变量`y`)，而不是准确性度量值计算。

  因此，如果你没有要评分的数据的目标标签，你可以修改存储的过程以删除 AUC 计算，并只需从功能返回的提示概率 (变量`X`存储过程中)。

```SQL
CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
  EXEC sp_execute_external_script
    @language = N'Python',
    @script = N'
        import pickle;
        import numpy;
        import pandas;
        from sklearn import metrics
        
        mod = pickle.loads(lmodel2)
        
        X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
        y = numpy.ravel(InputDataSet[["tipped"]])
        
        probArray = mod.predict_proba(X)
        probList = []
        for i in range(len(probArray)):
          probList.append((probArray[i])[1])
        
        probArray = numpy.asarray(probList)
        fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
        aucResult = metrics.auc(fpr, tpr)
        print ("AUC on testing data is: " + str(aucResult))
        
        OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
        ',  
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

## <a name="scoring-using-the-revoscalepy-model"></a>评分使用 revoscalepy 模型

存储的过程_PredictTipRxPy_使用模型使用创建**revoscalepy**库。 它的工作方式为大致相同_PredictTipSciKitPy_过程中，但使用的一些更改**revoscalepy**函数。

```SQL
CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict_ex(mod, X)
      probList = []
      for i in range(len(probArray._results["tipped_Pred"])):
        probList.append((probArray._results["tipped_Pred"][i]))
      
      probArray = numpy.asarray(probList)
      fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
      aucResult = metrics.auc(fpr, tpr)
      print ("AUC on testing data is: " + str(aucResult))
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',    
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

## <a name="batch-scoring-using-a-select-query"></a>使用 SELECT 查询进行批量评分

存储的过程**PredictTipSciKitPy**和**PredictTipRxPy**需要两个输入参数： 

- 查询以检索评分的数据
- 训练模型的名称

在本节中，你将了解如何将这些自变量传递给要轻松地更改模型和用于评分的数据的存储过程。

1. 定义输入的数据，以获得评分，如下所示调用存储的过程。 此示例使用存储的过程 PredictTipSciKitPy 评分，并且将传入模型的名称和查询字符串

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    存储的过程返回作为输入的查询的一部分传递中每个行程的预测的概率。 如果你使用 SSMS (SQL Server Management Studio) 用于运行查询，概率将显示为表中**结果**窗格。 **消息**窗格中包含的大约 0.56 值的输出结果的准确性度量值 （AUC 或曲线下的区域）。

2. 若要使用**revoscalepy**模型进行评分，则调用存储的过程**PredictTipRxPy**，并在模型名称和查询字符串中传递。

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="score-individual-rows-using-scikit-learn-model"></a>评分使用 scikit 的各个行-了解模型

有时，而不是批处理评分，你可能要在单个的情况下，将传递获取值，从应用程序，并获取单个结果基于这些值。 例如，你可以设置 Excel 工作表、Web 应用程序或 Reporting Services 报表，以调用存储过程和提供用户键入或选择的输入信息。

在本部分中，你将了解如何通过调用存储的过程中创建单个预测。

1. 花点时间查看存储过程的代码[PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy)和[PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy)，它们的下载的一部分。 这些存储的过程使用 scikit-了解和 revoscalepy 模型，并执行评分，如下所示：

  - 作为输入提供了模型的名称和多个单个值。 这些输入包括乘客计数、 行程距离等。
  - 表值函数，`fnEngineerFeatures`接受输入的值，将转换的纬度和经度定向距离。 [第 4 课](sqldev-py4-create-data-features-using-t-sql.md)包含此表值函数的说明。
  - 如果从外部应用程序调用存储的过程，请确保输入的数据匹配所需的输入的 Python 模型功能。 这可能包括强制转换或将输入的数据转换为 Python 数据类型，或验证的数据类型和数据长度。
  - 存储的过程创建基于存储的 Python 模型的分数。

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

下面是执行评分使用存储过程的定义**scikit-了解**模型。

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeSciKitPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      probList = []
      probList.append((mod.predict_proba(X)[0])[1])
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
    ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
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
GO
```

### <a name="predicttipsinglemoderxpy"></a>PredictTipSingleModeRxPy

下面是执行评分使用存储过程的定义**revoscalepy**模型。

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
    SELECT * FROM [dbo].[fnEngineerFeatures]( 
      @passenger_count,
      @trip_distance,
      @trip_time_in_secs,
      @pickup_latitude,
      @pickup_longitude,
      @dropoff_latitude,
      @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict_ex(mod, X)
      
      probList = []
      probList.append(probArray._results["tipped_Pred"])
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
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
GO
```

2.  若要试用一下，打开一个新**查询**窗口中，并调用存储过程，针对每个功能列中键入参数。

    ```SQL
    -- Call stored procedure PredictTipSingleModeSciKitPy to score using SciKit-Learn model
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    -- Call stored procedure PredictTipSingleModeRxPy to score using revoscalepy model
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```
    
    对于这些功能列，按顺序是七个值：
    
    -   *passenger_count*
    -   *trip_distance*
    -   *trip_time_in_secs*
    -   *pickup_latitude*
    -   *pickup_longitude*
    -   *dropoff_latitude*
    -   *dropoff_longitude*

3. 这两个过程的输出时，提示支付的 taxi 行程的上述参数或功能的概率。

## <a name="conclusions"></a>结论

在本教程中，你已了解如何使用存储过程中嵌入的 Python 代码。 与集成[!INCLUDE[tsql](../../includes/tsql-md.md)]，可以更轻松，若要部署 Python 模型以预测，并将企业数据工作流的一部分重新训练模型。

## <a name="previous-step"></a>上一步
[步骤 6：操作模型](sqldev-py6-operationalize-the-model.md)

## <a name="see-also"></a>另请参阅

[机器学习服务与 Python](../python/sql-server-python-services.md)

