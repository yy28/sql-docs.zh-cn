---
title: 使用 Python 模型预测潜在结果
description: 本教程介绍如何在 SQL Server 带有 T-sql 函数的存储过程中操作嵌入的 PYthon 脚本
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: b04e57c45c6113d4a0404a3a338e6beba4cda813
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468599"
---
# <a name="run-predictions-using-python-embedded-in-a-stored-procedure"></a>使用存储过程中嵌入的 Python 运行预测
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是[针对 SQL 开发人员的数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md)教程的一部分。 

在此步骤中, 你将学习如何*操作*你在上一步中训练和保存的模型。

在这种情况下, 操作化意味着将模型部署到生产环境以进行评分。 与 SQL Server 的集成使得这一点非常简单, 因为你可以在存储过程中嵌入 Python 代码。 若要基于新输入从模型中获取预测, 只需从应用程序中调用存储过程并传递新的数据。

本课程演示了两种基于 Python 模型创建预测的方法: 批处理评分, 并按行评分。

- **批处理评分:** 若要提供多行输入数据, 请将 SELECT 查询作为参数传递给存储过程。 结果是对应于输入事例的观测值表。
- **单个评分:** 作为输入传递一组单独的参数值。  存储过程将返回单个行或值。

评分所需的所有 Python 代码都作为存储过程的一部分提供。

## <a name="batch-scoring"></a>批处理评分

前两个存储过程演示了在存储过程中包装 Python 预测调用的基本语法。 这两个存储过程都需要数据表作为输入。

- 要使用的确切模型的名称作为输入参数提供给存储过程。 该存储过程从数据库表`nyc_taxi_models`中加载序列化模型。表中, 使用存储过程中的 SELECT 语句。
- 序列化模型存储在 python 变量`mod`中以供使用 Python 进一步处理。
- 需要评分的新案例是从中[!INCLUDE[tsql](../../includes/tsql-md.md)] `@input_data_1`指定的查询获取的。 读取查询数据时，行保存在默认数据帧 `InputDataSet`中。
- 这两个存储过程都`sklearn`使用中的函数来计算准确性指标 AUC (曲线下的区域)。 仅当还提供目标标签 (带标签_的列)_ 时, 才能生成 AUC 等准确性指标。 预测不需要目标标签 (变量`y`), 但准确性指标计算。

    因此, 如果没有要评分的数据的目标标签, 则可以修改该存储过程以删除 AUC 计算, 并仅返回功能 (存储过程中的变量`X` ) 中的提示概率。

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

Rrun 以下 T-sql 语句来创建存储过程。 此存储过程需要基于 scikit-learn 包的模型, 因为它使用特定于该包的函数:

+ 包含输入的数据帧传递到逻辑回归`predict_proba` `mod`模型的函数。 函数 (`probArray = mod.predict_proba(X)`) 返回一个 float, 该对象表示给定 tip (任意数量) 的概率。  `predict_proba`

```sql
DROP PROCEDURE IF EXISTS PredictTipSciKitPy;
GO

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

此存储过程使用相同的输入, 并与上一个存储过程创建相同的分数类型, 但使用 SQL Server 机器学习提供的**revoscalepy**包中的函数。

```sql
DROP PROCEDURE IF EXISTS PredictTipRxPy;
GO

CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
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
probList = probArray["tipped_Pred"].values 

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

## <a name="run-batch-scoring-using-a-select-query"></a>使用 SELECT 查询运行批处理评分

存储过程**PredictTipSciKitPy**和**PredictTipRxPy**需要两个输入参数: 

- 检索用于计分的数据的查询
- 定型模型的名称

通过将这些参数传递给存储过程, 您可以选择特定的模型或更改用于评分的数据。

1. 若要使用**scikit-learn**模型进行评分, 请调用存储过程**PredictTipSciKitPy**, 并将模型名称和查询字符串作为输入传递。

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    存储过程返回作为输入查询的一部分传入的每个行程的预测概率。 
    
    如果使用 SSMS (SQL Server Management Studio) 来运行查询, 则概率将显示为**结果**窗格中的表。 "**消息**" 窗格输出的准确性指标 (AUC 或 "曲线下") 的值为0.56。

2. 若要使用**revoscalepy**模型进行评分, 请调用存储过程**PredictTipRxPy**, 并将模型名称和查询字符串作为输入传递。

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>单行评分

有时, 你可能想要传入一个事例, 从应用程序中获取值, 并基于这些值返回一个结果, 而不是批处理评分。 例如, 您可以设置一个 Excel 工作表、web 应用程序或报表来调用存储过程, 并将其传递给用户键入或选择的输入。

在本部分中, 你将了解如何通过调用两个存储过程来创建单个预测:

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy)是使用 scikit-learn 模型为单行评分设计的。
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy)是使用 revoscalepy 模型为单行评分设计的。
+ 如果尚未训练过模型, 请返回到[步骤 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

这两种模型都将一系列单个值作为输入, 例如乘客计数、行程距离等。 表值函数`fnEngineerFeatures`用于将纬度和经度值从输入转换为新特征的直接距离。 [第4课](sqldev-py4-create-data-features-using-t-sql.md)介绍了此表值函数。

这两个存储过程都基于 Python 模型创建分数。

> [!NOTE]
> 
> 从外部应用程序调用存储过程时, 必须提供 Python 模型所需的所有输入功能, 这一点很重要。 若要避免错误, 除了验证数据类型和数据长度外, 还可能需要将输入数据强制转换或转换为 Python 数据类型。

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

花点时间查看存储过程的代码, 该代码使用**scikit-learn**模型执行评分。

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeSciKitPy;
GO

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
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
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

以下存储过程使用**revoscalepy**模型执行评分。

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeRxPy;
GO

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
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
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
probList = probArray["tipped_Pred"].values

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

### <a name="generate-scores-from-models"></a>从模型生成分数

创建存储过程后, 就可以轻松地根据每个模型生成分数。 只需打开一个新的**查询**窗口, 然后为每个特征列键入或粘贴参数。 这些功能列的七个必需值按顺序排列:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. 若要使用**revoscalepy**模型生成预测, 请运行以下语句:
  
    ```sql
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. 若要使用**scikit-learn**模型生成分数, 请运行以下语句:

    ```sql
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

这两个过程的输出都是使用指定的参数或功能为出租车行程支付 tip 的概率。

## <a name="conclusions"></a>结论

在本教程中, 已了解如何使用存储过程中嵌入的 Python 代码。 与[!INCLUDE[tsql](../../includes/tsql-md.md)]集成使你可以更轻松地部署用于预测的 Python 模型, 并将模型重新训练纳入企业数据工作流的一部分。

## <a name="previous-step"></a>上一步

[训练和保存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>请参阅

[SQL Server 中的 Python 扩展](../concepts/extension-python.md)
