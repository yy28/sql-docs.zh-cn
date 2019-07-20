---
title: 使用预测 T-sql 语句的本机计分
description: 使用预测 T-sql 函数生成预测, 根据 SQL Server 上的 R 或 Python 中编写的预先训练的模型对 dta 输入进行评分。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: b148bd1ca51a7121ae043e2b616100e295c008aa
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344756"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>使用预测 T-sql 函数的本机计分
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本机计分使用[预测 t-sql 函数](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)和 SQL Server 2017 中的C++本机扩展功能, 以近乎实时的速度为新数据输入生成预测值或*分数*。 此方法可提供预测和预测工作负荷的最快处理速度, 但需要满足平台和库要求: 只有 RevoScaleR 和 revoscalepy 中的C++函数具有实现。

本机计分要求您具有已训练的模型。 在 SQL Server 2017 Windows 或 Linux 或 Azure SQL 数据库中, 可以调用 Transact-sql 中的 PREDICT 函数来针对作为输入参数提供的新数据调用本机计分。 PREDICT 函数返回您提供的数据输入的分数。

## <a name="how-native-scoring-works"></a>本机评分的工作原理

本机计分使用 Microsoft C++提供的本机库, 这些库可读取已训练的模型, 以前以特殊二进制格式存储, 或以原始字节流的形式保存到磁盘, 并为提供的新数据输入生成分数。 由于已对模型进行定型、发布和存储, 因此它可用于评分, 无需调用 R 或 Python 解释器。 这样, 就减少了多个进程交互的开销, 从而提高了企业生产方案的预测性能。

若要使用本机计分, 请调用预测 T-sql 函数并传递以下必需的输入:

+ 基于支持的算法的兼容模型。
+ 输入数据, 通常定义为 SQL 查询。

函数将返回输入数据的预测, 以及要传递的源数据的任何列。

## <a name="prerequisites"></a>先决条件

预测在所有版本的 SQL Server 2017 数据库引擎上都可用, 并在默认情况下启用, 包括 Windows SQL Server 2017 机器学习服务、SQL Server 2017 (Windows)、SQL Server 2017 (Linux) 或 Azure SQL 数据库。 不需要安装 R、Python 或启用其他功能。

+ 必须使用下面列出的某个受支持的**rx**算法预先训练该模型。

+ 使用[rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) for R 和用于 Python 的[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)序列化模型。 已对这些序列化函数进行了优化, 以支持快速评分。

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

如果需要使用 MicrosoftML 或 MicrosoftML 中的模型, 请使用[sp_rxPredict 的实时计分](real-time-scoring.md)。

不支持的模型类型包括以下类型:

+ 包含其他转换的模型
+ 在 RevoScaleR 或`rxGlm` revoscalepy `rxNaiveBayes`等效项中使用或算法的模型
+ PMML 模型
+ 使用其他开源或第三方库创建的模型

## <a name="example-predict-t-sql"></a>例如：PREDICT (T-SQL)

在此示例中, 您将创建一个模型, 然后从 T-sql 调用实时预测函数。

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

使用以下语句来用**iris**数据集中的数据填充数据表。

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

现在, 创建一个表用于存储模型。

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

下面的代码创建基于**iris**数据集的模型, 并将其保存**到名为**model 的表中。

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
> 请确保使用 RevoScaleR 中的[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)函数保存模型。 标准 R `serialize`函数无法生成所需的格式。

您可以运行如下语句, 以二进制格式查看存储的模型:

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>步骤 2. 对模型运行预测

以下简单的 PREDICT 语句使用**本机计分**函数获取决策树模型中的分类。 它基于提供的属性、花瓣长度和宽度预测 iris 物种。

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

如果收到错误 ", 则在函数预测执行过程中出现错误。 模型已损坏或无效 ", 这通常意味着查询未返回模型。 检查您键入的模型名称是否正确, 或模型表是否为空。

> [!NOTE]
> 由于**预测**返回的列和值可以根据模型类型而改变, 因此您必须使用**WITH**子句定义返回的数据的架构。

## <a name="next-steps"></a>后续步骤

有关包含本机计分的完整解决方案, 请参阅 SQL Server 开发团队中的以下示例:

+ 部署 ML 脚本:[使用 Python 模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ 部署 ML 脚本:[使用 R 模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)