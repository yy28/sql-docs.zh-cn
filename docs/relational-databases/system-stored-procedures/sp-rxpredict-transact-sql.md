---
title: sp_rxPredict |微软文档
ms.date: 03/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 3c12349e48f474b53957ffac55415ccc0689eeca
ms.sourcegitcommit: fbe0ab88fa8d5aa3ea96629f4ccfa4da5caf74f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2020
ms.locfileid: "81012433"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly.md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

为给定的输入生成预测值，该输入由存储在 SQL Server 数据库中的二进制格式的机器学习模型组成。

近乎实时地在 R 和 Python 机器学习模型上提供评分。 `sp_rxPredict``rxPredict`是作为[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)和[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)中的 R 函数的包装提供的存储过程，以及 rx_predict [Python](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict)函数在[revoscaley](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)和[Microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)中提供。 它写于C++，专为评分操作进行了优化。

尽管必须使用 R 或 Python 创建模型，但一旦模型序列化并存储在目标数据库引擎实例上，即使未安装 R 或 Python 集成，也可以从该数据库引擎实例使用该模型。 有关详细信息，请参阅使用[sp_rxPredict 的实时评分](https://docs.microsoft.com/sql/machine-learning/real-time-scoring)。

## <a name="syntax"></a>语法

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>参数

**模型**

支持格式的预训练模型。 

**input**

有效的 SQL 查询

### <a name="return-values"></a>返回值

返回分数列以及输入数据源中的任何传递列。
如果算法支持生成此类值，则可以返回其他分数列，如置信区间。

## <a name="remarks"></a>备注

要启用存储过程的使用，必须在实例上启用 SQLCLR。

> [!NOTE]
> 使用此选项会产生安全影响。 如果在服务器上无法启用 SQLCLR，请使用替代实现，如[Transact-SQL PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017)函数。

用户需要`EXECUTE`数据库的权限。

### <a name="supported-algorithms"></a>支持的算法

要创建和训练模型，请使用[SQL Server 机器学习服务 （R 或 Python）、SQL](https://docs.microsoft.com/sql/machine-learning/what-is-sql-server-machine-learning) [Server 2016 R 服务](https://docs.microsoft.com/sql/machine-learning/r/sql-server-r-services)[、SQL Server 机器学习服务器（独立）（R 或 Python）](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone)或[SQL Server 2016 R 服务器（独立）](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone?view=sql-server-2016)提供的 R 或 Python 支持的算法之一。

#### <a name="r-revoscaler-models"></a>R： RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxd森林](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R： 微软ML模型

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rx快速森林](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rx快速线性](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R：微软ML提供的转换

  + [图里泽文本](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [Concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [分类](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python：重度模型

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python：微软模型

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python：微软提供的转换

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [Concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [分类](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>不支持的模型类型

不支持以下模型类型：

+ 使用 RevoScaleR`rxGlm`中的 或`rxNaiveBayes`算法的模型
+ R 中的 PMML 型号
+ 使用其他第三方库创建的模型 

## <a name="examples"></a>示例

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

除了是有效的 SQL 查询外*\@，inputData*中的输入数据还必须包括与存储模型中的列兼容的列。

`sp_rxPredict`仅支持以下 .NET 列类型：双精度、浮点、短列、u 短型、长列、ulong 和字符串。 在使用输入数据进行实时评分之前，您可能需要筛选出输入数据中不支持的类型。 

  有关相应的 SQL 类型的信息，请参阅 [SQL-CLR 类型映射](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或[映射 CLR 参数数据](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。

