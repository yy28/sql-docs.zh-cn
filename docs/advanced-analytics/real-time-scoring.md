---
title: 在 SQL Server 机器学习中的实时评分 |Microsoft Docs
description: 生成使用 sp_rxPredict，计分 dta 输入对 SQL Server 上以 R 编写的预先训练模型的预测。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d5a3d0318f925918ef98ae18744e4287d6b81108
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2018
ms.locfileid: "40396268"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>使用 SQL Server 机器学习中 sp_rxPredict 实时评分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

此文章介绍了如何评分在近乎实时的适用于 SQL Server 关系数据，使用机器学习模型写入在 R 中 

> [!Note]
> 本机计分是非常快评分使用本机 T-SQL 的预测函数的特殊实现实时评分。 有关详细信息和可用性，请参阅[本机计分](sql-native-scoring.md)。

## <a name="how-real-time-scoring-works"></a>如何实时评分的工作原理

实时评分对 RevoScaleR 或 MicrosoftML 函数如基于特定模型类型支持在 SQL Server 2016 和 SQL Server 2017 [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)或[rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). 它使用本机 c + + 库来生成评分，根据用户输入提供给机器学习模型存储在特殊的二进制格式。

可用于训练的模型评分而无需调用外部语言运行时，由于减少了多个进程的开销。 这用于生产评分方案支持更快的预测性能。 因为数据不会离开 SQL Server，则可以生成结果，并将其插入到新表中不使用任何 R 和 SQL 之间的数据转换。

实时评分是一个多步骤过程：

1. 必须在每个数据库的基础上启用执行评分存储的过程。
2. 加载预先训练的模型以二进制格式。
3. 提供新的输入的数据、 表格或单个行，作为模型的输入。
4. 若要生成评分，调用 sp_rxPredict 存储过程。

## <a name="get-started"></a>入门

有关代码示例和说明，请参阅[如何执行本机计分或实时评分](r/how-to-do-realtime-scoring.md)。

有关如何使用 rxPredict 进行评分的示例，请参阅[端到端贷款冲销预测构建使用 Azure HDInsight Spark 群集和 SQL Server 2016 R 服务](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

> [!TIP]
> 如果你正在以独占方式在 R 代码中，您还可以使用[rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)以快速获得评分的函数。

## <a name="requirements"></a>要求

在这些平台上支持实时评分：

+ SQL Server 2017 机器学习服务
+ SQL Server R Services 2016，与升级到 9.1.0 或更高版本的 R 组件

SQL Server 上必须启用预先要将基于 CLR 的库添加到 SQL Server 的实时评分的功能。

有关在基于 Microsoft R Server 分布式环境中的实时评分的信息，请参阅[publishService](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)函数中提供[mrsDeploy 包](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)，它也支持发布模型进行实时评分为新的 R Server 上运行的 web 服务。

### <a name="restrictions"></a>限制

+ 必须事先使用某个受支持训练模型**rx**算法。 有关详细信息，请参阅[支持的算法](#bkmk_rt_supported_algos)。 使用实时评分`sp_rxPredict`支持的 RevoScaleR 和 MicrosoftML 算法。

+ 必须使用新的序列化函数保存模型： [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)对于 R，并[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)适用于 Python。 这些序列化函数已经过优化，以支持快速评分。

+ 实时评分不会使用解释器;因此，可能需要解释器的任何功能不支持在评分步骤。  这些情况可能包括：

  + 使用情况建模`rxGlm`或`rxNaiveBayes`目前不支持的算法

  + 使用 R 转换函数或包含一个转换，如公式的 RevoScaleR 模型<code>A ~ log(B)</code>中实时评分不支持。 若要使用此类型的模型，我们建议你在执行转换以输入数据，然后再将数据传递到实时评分。

+ 针对快速预测对小型数据集，范围从少量的行到成千上万行的当前优化实时评分。 在大型数据集，使用[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)可能更快。

### <a name="a-namebkmkrtsupportedalgosalgorithms-that-support-real-time-scoring"></a><a name="bkmk_rt_supported_algos">支持实时评分的算法

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  模型标记为\*还支持使用预测函数的本机计分。

+ MicrosoftML 模型

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ 转换提供的 MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>不受支持的模型类型

非显式列出的那些在上一节中的 R 转换不支持实时评分。 

对于开发人员已习惯使用 RevoScaleR 和其他特定于 Microsoft R 的库，不支持的函数包括`rxGlm`或`rxNaiveBayes`RevoScaleR，PMML 模型中的算法和其他使用 CRAN 的其他 R 库创建的模型或其他存储库。

### <a name="known-issues"></a>已知问题

+ `sp_rxPredict` 作为模型传递 NULL 值时返回不准确的消息:"System.Data.SqlTypes.SqlNullValueException:Data 中 Null"。

## <a name="next-steps"></a>后续步骤

[如何执行实时评分](r/how-to-do-realtime-scoring.md)
