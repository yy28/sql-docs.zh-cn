---
title: 使用 T-SQL PREDICT 本机评分
description: 使用 PREDICT T-SQL 函数生成预测，针对 SQL Server 上使用 R 或 Python 编写的预定型模型对数据输入进行评分。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 766adecbc91f88ed0796e4214b7e4074fc564f01
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727284"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>使用 PREDICT T-SQL 函数本机评分
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本机评分使用 [PREDICT T-SQL 函数](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)和 SQL Server 2017 中的本机 C++ 扩展功能生成近乎实时的新数据输入的预测值或分数  。 此方法提供尽可能最快的预测和预测工作负载处理速度，但是对平台和库有要求：只有 RevoScaleR 和 revoscalepy 中的函数才具有 C++ 实现。

本机评分要求你具有已定型的模型。 在 SQL Server 2017 Windows 或 Linux 中，或在 Azure SQL 数据库中，可以调用 Transact-SQL 中的 PREDICT 函数，以针对作为输入参数提供的新数据调用本机评分。 PREDICT 函数返回所提供的数据输入的分数。

## <a name="how-native-scoring-works"></a>本机评分的工作原理

本机评分使用 Microsoft 中的本机 C++ 库，这些库可读取之前以特殊二进制格式存储或作为原始字节流保存到磁盘的已定型模型，并为提供的新数据输入生成分数。 由于已对模型进行定型、发布和存储，因此它可用于评分，而无需调用 R 或 Python 解释器。 这样，减少了多个流程交互的开销，从而在企业生产场景中提供了更快速的预测性能。

若要使用本机评分，请调用 PREDICT T-SQL 函数并传递以下必需的输入：

+ 基于受支持算法的兼容模型。
+ 输入数据，通常定义为 SQL 查询。

此函数将返回输入数据的预测以及要传递的源数据的任何列。

## <a name="prerequisites"></a>必备条件

PREDICT 在所有版本的 SQL Server 2017 数据库引擎上都可用，并且默认启用，包括 Windows 上的 SQL Server 机器学习服务、SQL Server 2017 (Windows)、SQL Server 2017 (Linux) 或 Azure SQL 数据库。 无需安装 R、Python 或启用其他功能。

+ 必须使用下面列出的某个受支持的 rx 算法预定型该模型  。

+ 使用适用于 R 的 [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 和适用于 Python 的 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) 对模型进行序列化。 已对这些序列化函数进行了优化，以支持快速评分。

<a name="bkmk_native_supported_algos"></a> 

## <a name="supported-algorithms"></a>支持的算法

+ revoscalepy 模型

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

如果需要使用 MicrosoftML 或 microsoftml 中的模型，请[使用 sp_rxPredict 实时评分](real-time-scoring.md)。

不受支持的模型类型包括以下类型：

+ 包含其他转换的模型
+ 使用 RevoScaleR 或 revoscalepy 等效项中的 `rxGlm` 或 `rxNaiveBayes` 算法的模型
+ PMML 模型
+ 使用其他开放源代码或第三方库创建的模型

## <a name="example-predict-t-sql"></a>示例：PREDICT (T-SQL)

在此示例中，需要创建一个模型，然后调用 T-SQL 中的实时预测函数。

### <a name="step-1-prepare-and-save-the-model"></a>步骤 1。 准备并保存模型

运行以下代码以创建示例数据库和所需的表。

```sql
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
  "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

使用以下语句，以使用 iris 数据集的数据填充数据表  。

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

现在，创建用于存储模型的表。

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

以下代码创建基于 iris 数据集的模型，并将其保存到名为“模型”的表中   。

```sql
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE] 
> 请确保使用 RevoScaleR 的 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 函数保存模型。 标准 R `serialize` 函数无法生成所需格式。

可以运行如下语句，以二进制格式查看存储的模型：

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>步骤 2. 对模型运行 PREDICT

以下简单的 PREDICT 语句使用 native scoring 函数获取决策树模型中的分类  。 它根据提供的属性、花瓣长度和宽度预测 iris 种类。

```sql
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

如果收到错误“函数 PREDICT 执行期间出错。 模型已损坏或无效”，这通常意味着查询未返回模型。 检查键入的模型名称是否正确，或模型表是否为空。

> [!NOTE]
> 由于 PREDICT 返回的列和值可能因模型类型而有所不同，因此必须使用 WITH 子句定义返回数据的架构   。

## <a name="next-steps"></a>后续步骤

有关包含本机评分的完整解决方案，请参阅 SQL Server 开发团队中的以下示例：

+ 部署 ML 脚本：[使用 Python 模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ 部署 ML 脚本：[使用 R 模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)