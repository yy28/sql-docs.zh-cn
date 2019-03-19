---
title: sp_rxPredict | Microsoft Docs
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: HeidiSteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 50e25162f88c42c0728f951702d304975fb7091b
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161594"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

生成的机器学习模型存储在 SQL Server 数据库中的二进制格式包含给定输入的预测的值。

提供了 R 和 Python 机器学习模型中近实时地评分。 `sp_rxPredict` 为提供包装的存储的过程`rxPredict`中的 R 函数[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)并[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)，和[rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) Python 函数中[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)并[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)。 它用 c + + 编写的并专门针对计分操作进行了优化。

虽然必须序列化并存储在目标数据库引擎实例上的二进制格式后使用 R 或 Python，创建模型，但可以使用它从该数据库引擎实例，即使未安装 R 或 Python 集成。 有关详细信息，请参阅[实时评分 sp_rxPredict](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)。

## <a name="syntax"></a>语法

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>参数

**model**

预先训练的模型中受支持的格式。 

**input**

有效的 SQL 查询

### <a name="return-values"></a>返回值

返回评分列，以及输入的数据源中的任何传递列。
其他评分列，如置信区间，则可以算法是否支持生成这样的值返回。

## <a name="remarks"></a>备注

若要启用的存储过程的使用，必须在实例上启用 SQLCLR。

> [!NOTE]
> 会存在安全隐患 enabing 到此选项。 使用备用实现，如下所示[TRANSACT-SQL 预测](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017)函数，如果不能在服务器上启用 SQLCLR。

用户需求`EXECUTE`针对数据库的权限。

### <a name="supported-algorithms"></a>支持的算法

若要创建和训练模型，使用适用于 R 或 Python，受支持的算法之一提供的[SQL Server 2016 R Services](https://docs.microsoft.com/sql/advanced-analytics/r/sql-server-r-services?view=sql-server-2017)， [SQL Server 2016 R Server （独立版）](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2016)， [SQL Server 2017 机器学习服务 （R 或 Python）](https://docs.microsoft.com//sql/advanced-analytics/what-is-sql-server-machine-learning?view=sql-server-2017)，或[SQL Server 2017 服务器 （独立版） （R 或 Python）](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2017)。

#### <a name="r-revoscaler-models"></a>:RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>:MicrosoftML 模型

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>:转换提供的 MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python: revoscalepy 模型

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python: microsoftml 模型

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python:转换提供的 microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-referencee/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>不受支持的模型类型

不支持以下模型类型：

+ 使用情况建模`rxGlm`或`rxNaiveBayes`RevoScaleR 中的算法
+ 在 R 中的 PMML 模型
+ 使用其他第三方库创建的模型 

## <a name="examples"></a>示例

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

除了成为有效的 SQL 查询中的输入数据*@inputData*必须包括在存储模型中的列与列兼容。

`sp_rxPredict` 仅支持以下.NET 列类型： 双精度型、 float、 short、 ushort、 long、 ulong 和字符串。 您可能需要筛选出输入数据中不支持的类型，然后再使用它进行实时评分。 

  有关相应 SQL 类型的信息，请参阅[SQL-CLR 类型映射](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或[映射 CLR 参数数据](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。

