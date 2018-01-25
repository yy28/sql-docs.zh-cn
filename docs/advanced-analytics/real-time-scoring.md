---
title: "实时评分 |Microsoft 文档"
ms.custom: 
ms.date: 11/03/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3fce545d18876014e577b1f4e67800d4940881f3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="realtime-scoring"></a>实时评分

本主题介绍在 SQL Server 2016 和支持以近实时的机器学习模型评分的 SQL Server 2017 中可用的功能。

> [!TIP]
> 本机评分是实时的一种特殊评分的实现非常快评分，使用本机的 T-SQL 的预测函数，并仅在 SQL Server 2017 中可用。 有关详细信息，请参阅[本机评分](sql-native-scoring.md)。

## <a name="how-realtime-scoring-works"></a>实时评分的工作原理

在特定模型类型使用支持 RevoScaleR 或 MicrosoftML 算法创建的情况下，实时评分支持在 SQL Server 2016 和 SQL Server 自 2017 年中。 它使用本机 c + + 库生成评分，根据用户输入提供给机器学习模型的特殊的二进制格式存储。

由于可以用于训练的模型评分而无需调用外部语言运行时，减少了多个进程的开销。 此设置用于评分方案的生产支持更快的预测性能。 因为数据绝不会离开 SQL Server，则可以生成结果，并将其插入到新表中不使用 R 和 SQL 之间的任何数据转换。

实时评分是一个多步骤过程：

1. 基于每个数据库，必须启用未评分的存储的过程。
2. 加载以二进制格式预先训练的模型。
3. 提供新的输入的数据，表格或单个行，作为对模型的输入。
4. 若要生成评分，调用 sp_rxPredict 存储过程。

## <a name="get-started"></a>要开始

有关代码示例和说明，请参阅[如何执行本机评分或实时评分](r/how-to-do-realtime-scoring.md)。

有关举例说明如何 rxPredict 可以使用以获得评分，请参阅[端到端贷款 ChargeOff 预测生成使用 Azure HDInsight Spark 群集和 SQL Server 2016 R 服务](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

> [!TIP]
> 如果你正在以独占方式在 R 代码，也可以使用[rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)以快速获得评分的函数。

## <a name="requirements"></a>需求

在这些平台上支持实时评分：

+ SQL Server 2017 机器学习服务
+ SQL Server R Services 2016，与 Microsoft R Server 9.1.0 到的 R Services 实例的升级或更高版本
+ 机器学习服务器（独立）

SQL Server 上必须启用实时提前评分功能。 这是因为此功能要求的基于 CLR 的库安装到 SQL Server。

有关实时信息评分在分布式环境中基于 Microsoft R Server，请参阅[publishService](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)函数中提供[mrsDeploy 包](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)，支持作为新评分 R Server 上运行的 web 服务的实时的发布模型。

### <a name="restrictions"></a>限制

+ 必须事先使用支持之一定型模型**rx**算法。 有关详细信息，请参阅[支持算法](#bkmk_rt_supported_algos)。 实时评分与`sp_rxPredict`支持 RevoScaleR 和 MicrosoftML 算法。

+ 必须使用新的序列化函数保存模型： [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) ，和[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) for Python。 已优化这些序列化函数以支持快速评分。

+ 实时评分不使用解释器解释器;因此，可能需要解释器的任何功能不支持在评分的步骤。  这些情况可能包括：

  + 模型使用`rxGlm`或`rxNaiveBayes`算法当前不支持

  + 使用一个 R 的转换函数或包含一个转换，如公式的 RevoScaleR 模型<code>A ~ log(B)</code>中实时评分不支持。 若要使用此类型的模型，我们建议在上执行转换，然后再将数据传递到实时计分输入数据。

+ 针对较小的数据集，范围从少量的行到数百个上千个行上的快速预测当前优化实时评分。 对超大型数据集，使用[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)可能更快。

### <a name="a-namebkmkrtsupportedalgosalgorithms-that-support-realtime-scoring"></a><a name="bkmk_rt_supported_algos">支持实时评分的算法

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)\*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  模型标记为\*还支持使用预测函数的本机评分。

+ MicrosoftML models

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ 提供的 MicrosoftML 的转换

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>不受支持的模型类型

不支持以下模型类型：

+ 模型包含其他、 不受支持类型的 R 转换
+ 模型使用`rxGlm`或`rxNaiveBayes`中 RevoScaleR 算法
+ PMML 模型
+ 使用其他 R 库从 CRAN 或其他存储库创建的模型
+ 模型包含任何其他类型的 R 之外此处列出的转换

### <a name="known-issues"></a>已知问题

+ `sp_rxPredict`作为模型传递 NULL 值时将返回不准确消息:"System.Data.SqlTypes.SqlNullValueException:Data 中 Null"。

## <a name="next-steps"></a>后续步骤

[如何执行实时评分](r/how-to-do-realtime-scoring.md)
