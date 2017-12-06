---
title: "步骤 6： 具有可操作性 Python 模型时使用 SQL Server |Microsoft 文档"
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: da38ad56ff82d836fa34e42d3505d3a588344cfa
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="step-6-operationalize-the-python-model-using-sql-server"></a>步骤 6： 具有可操作性 Python 模型时使用 SQL Server

使用本教程，本文摘自[SQL 开发人员的数据库中 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步骤中，您学习*具有可操作性*定型和上一步中保存的模型。

在此方案中，操作化意味着模型部署到生产环境进行评分。 与 SQL Server 的集成使此非常简单，因为你可以在存储过程中嵌入的 Python 代码。 若要利用基于新输入的模型的预测，只需从应用程序调用存储的过程，然后将新数据传递。

本课演示如何创建基于 Python 模型的预测的两种方法： 批处理评分，和评分逐行。

- **批量计分：**若要提供输入数据的多个行，SELECT 查询作为参数传递到存储过程。 结果是一个表的输入事例与对应的观察结果。
- **单个评分：**作为输入传递的单个参数值集。  存储过程将返回单个行或值。

作为存储过程的一部分提供了所有所需的评分的 Python 代码。

| 存储的过程名称 | 批处理或单 | 模型源|
|----|----|----|
|PredictTipRxPy|批处理 (batch)| revoscalepy 模型|
|PredictTipSciKitPy|批处理 (batch) |scikit-了解模型|
|PredictTipSingleModeRxPy|单个行| revoscalepy 模型|
|PredictTipSingleModeSciKitPy|单个行| scikit-了解模型|

## <a name="batch-scoring"></a>批处理评分

前两个存储的过程说明了 Python 预测调用包装在存储过程的基本语法。 这两个存储的过程要求数据将的表作为输入。

- 要使用的确切模型的名称是作为输入参数提供给该存储过程。 存储的过程将从数据库表中加载的序列化的模型`nyc_taxi_models`.table，存储过程中使用 SELECT 语句。
- Python 变量中存储的序列化的模型`mod`进行进一步处理使用 Python。
- 从获取需要要评分的新用例[!INCLUDE[tsql](../../includes/tsql-md.md)]中指定查询`@input_data_1`。 读取查询数据时，行保存在默认数据帧 `InputDataSet`中。
- 这两个存储的过程使用函数从`sklearn`来计算准确性度量值，AUC （曲线下的区域）。 如果你还提供目标标签只能生成准确性度量值，如 AUC (_附属式_列)。 预测不需要目标标签 (变量`y`)，而不是准确性度量值计算。

    因此，如果你没有要评分的数据的目标标签，你可以修改存储的过程以删除 AUC 计算，并从功能返回仅提示概率 (变量`X`存储过程中)。

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

存储的过程应已创建为你。 如果找不到它，运行以下的 T-SQL 语句，以便创建存储的过程。

此存储的过程需要基于 scikit 的模型-了解包，因为它使用特定于该程序包的函数：

+ 包含输入的数据框架传递给`predict_proba`函数的逻辑回归模型， `mod`。 `predict_proba`函数 (`probArray = mod.predict_proba(X)`) 返回**float**表示 （的任意数量） 的提示将得到的概率。

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

### <a name="predicttiprxpy"></a>PredictTipRxPy

此存储的过程使用相同的输入并创建相同类型的评分与前面的存储过程，但使用函数从**revoscalepy**包中提供 SQL Server 机器学习。

> [!NOTE] 
> 为此存储过程以及代码的早期版本和 RTM 版本中，以便反映对 revoscalepy 包更改之间略有更改。 请参阅[更改](#changes)表获取详细信息。

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
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict(mod, X)
      prob_list = prob_array["tipped_Pred"].values 
      
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

## <a name="run-batch-scoring-using-a-select-query"></a>运行批处理计分使用 SELECT 查询

存储的过程**PredictTipSciKitPy**和**PredictTipRxPy**需要两个输入参数： 

- 查询以检索评分的数据
- 训练模型的名称

通过将这些自变量传递给存储过程，你可以选择特定模型或更改用于评分的数据。

1. 若要使用**scikit-了解**模型进行评分，则调用存储的过程**PredictTipSciKitPy**、 传递的模型名称和查询字符串作为输入。

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    存储的过程返回作为输入的查询的一部分传递中每个行程的预测的概率。 
    
    如果你使用 SSMS (SQL Server Management Studio) 用于运行查询，概率将显示为表中**结果**窗格。 **消息**窗格中包含的大约 0.56 值的输出结果的准确性度量值 （AUC 或曲线下的区域）。

2. 若要使用**revoscalepy**模型进行评分，则调用存储的过程**PredictTipRxPy**、 传递的模型名称和查询字符串作为输入。

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>单行评分

有时，而不是批量计分，你可能想要在单个的情况下，将传递应用程序，从获取值并返回单个结果基于这些值。 例如，无法设置 Excel 工作表、 web 应用程序或报表调用存储的过程，并向其传递输入类型化或选定的用户。

在本部分中，你将了解如何通过调用两个存储的过程中创建单个预测：

+ [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy)专为单行评分使用 scikit-学习模型。
+ [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy)专为单行评分使用 revoscalepy 模型。
+ 如果在尚未尚未训练模型，返回到[步骤 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)！

作为输入的一系列单个值，如乘客计数、 行程距离等这两个模型采用。 表值函数， `fnEngineerFeatures`，用于将纬度和经度值从一种新功能的输入转换、 直接距离。 [第 4 课](sqldev-py4-create-data-features-using-t-sql.md)包含此表值函数的说明。

这两个存储的过程创建基于 Python 模型的分数。

> [!NOTE]
> 
> 很重要，提供所需的 Python 模型，在调用存储的过程时从外部应用程序的所有输入的功能。 若要避免错误，可能需要强制转换或将输入的数据转换为 Python 数据类型，除了验证数据类型和数据长度。

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

花点时间查看执行评分使用存储过程的代码**scikit-了解**模型。

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

以下存储的过程执行评分使用**revoscalepy**模型。

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
      from revoscalepy.functions.RxPredict import rx_predict;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict(mod, X)
      
      probList = []
      prob_list = prob_array["tipped_Pred"].values
      
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

### <a name="generate-scores-from-models"></a>根据模型生成评分

已创建的存储的过程后，很容易生成任一模型所基于的评分。 只需打开新**查询**窗口中，并键入或粘贴为每个特征列的参数。 七个所需的值为这些功能列，按顺序：
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. 要通过使用生成预测**revoscalepy**模型，运行此语句：
  
    ```SQL
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. 若要通过使用生成的评分**scikit-了解**模型，运行此语句：

    ```SQL
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

这两个过程的输出时，提示为与指定的参数或功能 taxi 行程正在付费的概率。

### <a name="changes"></a>更改

本部分列出了本教程中使用的代码更改。 进行这些更改以反映最新**revoscalepy**版本。 有关 API 的帮助，请参阅[Python 函数库参考](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)。

| 更改的详细信息 | 说明|
| ----|----|
| 删除`import pandas`中的所有示例| 现在默认情况下加载的 pandas|
| 函数`rx_predict_ex`更改为`rx_predict`| 需要 RTM 和预发行版本`rx_predict_ex`|
| 函数`rx_logit_ex`更改为`rx_logit`| 需要 RTM 和预发行版本`rx_logit_ex`|
| ` probList.append(probArray._results["tipped_Pred"])`更改为`prob_list = prob_array["tipped_Pred"].values`| 更新 API|

如果你安装使用 SQL Server 自 2017 年的预发布版本的 Python 服务，我们建议你升级。 你还可以通过使用机器学习服务器的最新版本升级中的 Python 和 R 组件。 有关详细信息，请参阅[使用绑定来升级的 SQL Server 实例](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="conclusions"></a>结论

在本教程中，你已了解如何使用存储过程中嵌入的 Python 代码。 与集成[!INCLUDE[tsql](../../includes/tsql-md.md)]，可以更轻松，若要部署 Python 模型以预测，并将企业数据工作流的一部分重新训练模型。

## <a name="previous-step"></a>上一步

[步骤 5： 训练和保存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>另请参阅

[机器学习服务与 Python](../python/sql-server-python-services.md)
