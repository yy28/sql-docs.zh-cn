---
title: 预测潜在结果使用 Python 模型-SQL Server 机器学习
description: 本教程显示如何将 SQL Server 中的嵌入式的 PYthon 脚本进行操作的存储过程带有 T-SQL 函数
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9a75c25528003d0133cfd33c3eaddc20a8241692
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644766"
---
# <a name="run-predictions-using-python-embedded-in-a-stored-procedure"></a>运行使用 Python 在存储过程中嵌入的预测
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是教程的一部分[SQL 开发人员的数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步骤中，你学习*实施*训练和上一步中保存的模型。

在此方案中，操作化是指将模型部署到生产环境进行评分。 与 SQL Server 的集成使，这相当容易，因为可以在存储过程中嵌入 Python 代码。 若要从基于新的输入的模型获取预测，只需从应用程序调用存储的过程，并将新数据传递。

本课演示如何创建基于 Python 模型的预测的两个方法： 批处理评分和评分行的行。

- **批处理评分：** 若要提供的输入数据的多个行，将 SELECT 查询作为参数传递给存储过程。 结果是与输入事例对应的观测值的表。
- **单个评分：** 将一组单独的参数值传递作为输入。  存储过程将返回单个行或值。

作为存储过程的一部分提供了进行评分所需的所有 Python 代码。

## <a name="batch-scoring"></a>批处理计分

前两个存储的过程说明了在存储过程中包装 Python 预测调用的基本语法。 这两个存储的过程需要的数据的表作为输入。

- 作为对存储过程的输入参数提供要使用的确切模型的名称。 存储的过程将从数据库表中加载序列化的模型`nyc_taxi_models`.table，存储过程中使用 SELECT 语句。
- 序列化的模型存储在 Python 变量`mod`进行进一步处理使用 Python。
- 需要要评分的新用例从获取[!INCLUDE[tsql](../../includes/tsql-md.md)]中指定查询`@input_data_1`。 读取查询数据时，行保存在默认数据帧 `InputDataSet`中。
- 这两个存储的过程使用函数从`sklearn`来计算准确性指标，AUC （曲线下面积）。 如果你还提供的目标标签只能生成准确性度量值，如 AUC ( _tipped_列)。 预测不需要的目标标签 (变量`y`)，但准确性指标计算。

    因此，如果没有要评分的数据的目标标签，您可以修改存储的过程来删除 AUC 计算，并从功能返回仅提示概率 (变量`X`存储过程中)。

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

运行以下 T-SQL 语句以便创建存储的过程。 此存储的过程需要 scikit 所基于的模型-了解包，因为它使用特定于该包的函数：

+ 包含输入的数据框架传递给`predict_proba`函数的逻辑回归模型`mod`。 `predict_proba`函数 (`probArray = mod.predict_proba(X)`) 返回**float**表示 （的任意数量） 会支付小费的概率。

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

此存储的过程使用相同的输入和创建相同的类型的评分为上一存储过程，但使用函数从**revoscalepy**随 SQL Server 机器学习提供的包。

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

## <a name="run-batch-scoring-using-a-select-query"></a>运行批处理计分使用的 SELECT 查询

存储的过程**PredictTipSciKitPy**并**PredictTipRxPy**需要两个输入参数： 

- 检索用于评分的数据的查询
- 训练模型的名称

通过将这些参数传递给存储过程，可以选择特定模型或更改用于进行评分的数据。

1. 若要使用**scikit-了解**用于评分的模型，请调用存储的过程**PredictTipSciKitPy**、 传递模型名称和查询字符串作为输入。

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    存储的过程返回作为输入的查询的一部分传递每个行程的预测的概率。 
    
    如果运行的查询使用 SSMS (SQL Server Management Studio)，概率会显示为一个表中**结果**窗格。 **消息**窗格包含大约 0.56 值的输出结果的准确性指标 （AUC 或曲线下的面积）。

2. 若要使用**revoscalepy**用于评分的模型，请调用存储的过程**PredictTipRxPy**、 传递模型名称和查询字符串作为输入。

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>单行计分

有时，而不是批处理评分，你可能想要在单个的情况下，传递从应用程序，获取值并返回单个结果基于这些值。 例如，可以设置 Excel 工作表、 web 应用程序或报表调用存储的过程，并向其传递输入类型化或所选的用户。

在本部分中，将了解如何通过调用两个存储的过程创建单个预测：

+ [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy)专为单行计分使用 scikit-了解模型。
+ [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy)专为单行计分使用 revoscalepy 模型。
+ 如果未尚未定型模型，返回到[步骤 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)！

作为输入的单个值，例如乘客计数、 行程距离等一系列这两个模型采用。 表值函数， `fnEngineerFeatures`，用于将纬度和经度值从一项新功能的输入转换、 直接距离。 [第 4 课](sqldev-py4-create-data-features-using-t-sql.md)包含此表值函数的说明。

这两个存储的过程创建基于 Python 模型的分数。

> [!NOTE]
> 
> 提供从外部应用程序调用存储的过程时，Python 模型所需的所有输入的功能至关重要。 若要避免错误，可能需要强制转换或将输入的数据转换为 Python 数据类型，除了验证数据类型和数据长度。

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

花点时间查看代码执行评分使用的存储过程**scikit-了解**模型。

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

以下存储的过程执行使用评分**revoscalepy**模型。

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

### <a name="generate-scores-from-models"></a>若要从模型生成分数

已创建的存储的过程后，很容易生成基于任一模型评分。 只需打开一个新**查询**窗口中，键入或粘贴用于和参数的每个功能列。 七个所需的值为针对这些特征列，按顺序：
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. 若要使用生成预测**revoscalepy**模型中，运行此语句：
  
    ```sql
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. 若要通过使用生成的评分**scikit-了解**模型中，运行此语句：

    ```sql
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

这两个过程的输出是正在使用指定的参数或功能出租车行程支付小费的概率。

## <a name="conclusions"></a>结论

在本教程中，已学习了如何使用存储过程中嵌入 Python 代码。 与集成[!INCLUDE[tsql](../../includes/tsql-md.md)]可以更轻松部署 Python 模型用于预测以及将合并作为企业数据工作流的一部分重新训练模型。

## <a name="previous-step"></a>上一步

[训练和保存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>另请参阅

[SQL Server 中的 Python 扩展](../concepts/extension-python.md)
