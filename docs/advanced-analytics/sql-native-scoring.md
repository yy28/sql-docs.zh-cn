---
title: 使用预测 T-SQL 语句的 SQL Server 机器学习服务的本机计分
description: 生成预测评分 dta 输入对写入 SQL 服务器上的 R 或 Python 中的预先训练模型的预测 T-SQL 函数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: bd0a79a3991c34ddbcf874aca80160299074919a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513214"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>使用预测 T-SQL 函数的本机计分
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本机计分用途[预测 T-SQL 函数](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)和本机 c + + 扩展功能，SQL Server 2017 中的以生成预测值或*分数*附近真实时间中的新数据输入。 此方法提供预测和预测工作负荷的最快可以处理速度，但附带了平台和库要求： 仅从 RevoScaleR 和 revoscalepy 函数具有 c + + 实现。

本机计分要求你具有已训练的模型。 在 SQL Server 2017 Windows 或 Linux，或在 Azure SQL 数据库中，您可以调用 PREDICT 函数中 TRANSACT-SQL 来调用本机针对作为输入参数提供的新数据评分。 PREDICT 函数返回所提供的数据输入评分。

## <a name="how-native-scoring-works"></a>本机评分的工作原理

本机计分使用本机 c + + 库可以读取已训练的模型，Microsoft 提供的以前存储在特殊的二进制格式或保存到磁盘以原始字节流的形式，为你提供的新数据输入生成评分。 对模型进行训练，因为已发布和存储，它可以用于评分而无需调用 R 或 Python 解释器。 在这种情况下，多个进程交互的开销已降低，从而在企业生产方案中要快得多的预测性能。

若要使用本机计分，调用预测 T-SQL 函数并传递所需的以下输入：

+ 基于受支持的算法的兼容模型。
+ 输入的数据，通常定义为 SQL 查询。

该函数返回输入数据以及你想要传递的源数据的任何列的预测。

## <a name="prerequisites"></a>先决条件

预测与可在所有版本的 SQL Server 2017 数据库引擎，并且默认情况下，包括 Windows、 SQL Server 2017 (Windows)、 SQL Server 2017 (Linux) 或 Azure SQL 数据库上的 SQL Server 2017 机器学习服务支持。 不需要安装 R、 Python、 或启用其他功能。

+ 必须事先使用某个受支持训练模型**rx**下面列出的算法。

+ 模型使用进行序列化[rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)对于 R，并[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)适用于 Python。 这些序列化函数已经过优化，以支持快速评分。

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

如果您需要使用 MicrosoftML 或 microsoftml 中的模型，使用[实时评分 sp_rxPredict](real-time-scoring.md)。

不受支持的模型类型包括以下类型：

+ 模型包含其他转换
+ 使用情况建模`rxGlm`或`rxNaiveBayes`RevoScaleR 或 revoscalepy 等效项中的算法
+ PMML 模型
+ 使用其他开放源代码或第三方库创建的模型

## <a name="example-predict-t-sql"></a>例如：预测 (T-SQL)

在此示例中，您创建模型，，，然后从 T-SQL 调用实时预测函数。

### <a name="step-1-prepare-and-save-the-model"></a>步骤 1. 准备并保存模型

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

使用以下语句来填充数据的数据表格**鸢尾花**数据集。

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

以下代码将创建一个基于模型**iris**数据集并将其保存到名为表**模型**。

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
> 请务必使用[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) RevoScaleR 保存模型的函数。 标准 R`serialize`函数不能生成所需的格式。

可以运行以下命令以查看存储的模型以二进制格式之类的语句：

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>步骤 2. 对模型运行预测

下面的简单预测语句从决策树模型使用获取分类**本机计分**函数。 它预测鸢尾花种类基于你提供的属性、 花瓣长度和宽度。

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

如果收到错误，"执行期间出现错误的函数 PREDICT。 模型已损坏或无效"，这通常意味着您的查询未返回一个模型。 检查是否键入模型名称正确，或者如果模型表为空。

> [!NOTE]
> 因为返回的列和值**PREDICT**因模型类型而异，则必须使用定义返回的数据的架构**WITH**子句。

## <a name="next-steps"></a>后续步骤

一个包含本机计分的完整解决方案，请参阅 SQL Server 开发团队的这些示例：

+ 部署机器学习脚本：[使用 Python 模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ 部署机器学习脚本：[使用 R 模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)