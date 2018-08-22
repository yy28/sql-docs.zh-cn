---
title: 在 SQL Server 机器学习中的本机计分 |Microsoft Docs
description: 生成预测评分 dta 输入对写入 SQL 服务器上的 R 或 Python 中的预先训练模型的预测 T-SQL 函数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bf8f9a6362b72efddccbf5c2b0e54096c6e86aa7
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2018
ms.locfileid: "40394848"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>使用预测 T-SQL 函数的本机计分
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

预先训练的模型后，可以将新的输入的数据传递给函数，以生成预测值或*分数*。 在 SQL Server 2017 Windows 或 Linux，或在 Azure SQL 数据库中，可以在 TRANSACT-SQL 中使用 PREDICT 函数，以支持本机计分。 这只需要有已经过培训，可以调用使用 T-SQL 的一个模型。 

+ 什么是本机评分与实时评分
+ 工作方式
+ 支持的平台和要求

## <a name="what-is-native-scoring-and-how-is-it-different-from-real-time-scoring"></a>什么是本机计分，方式是不同于实时评分？

在 SQL Server 2016 中，Microsoft 创建了一种可扩展性框架，允许在 T-SQL 中执行 R 脚本。 此框架支持在 R，到训练复杂机器学习模型的简单函数范围中可能会执行任何操作。 但是，双进程体系结构需要调用外部 R 进程的每个调用，而不考虑操作的复杂性。 如果要从表和 SQL Server 中已有数据的分数针对它加载预先训练的模型，则调用外部 R 进程的开销表示不必要的性能成本。

_评分_是一个两步过程。 首先，指定要从表加载的预先训练的模型。 第二个，传递新输入到函数，以生成预测值的数据 (或_分数_)。 输入可以是表格或单个行。 可以选择可输出单个列的值表示概率，也可能会输出多个值，如置信区间、 错误或预测其他有用的补充。

如果输入包含很多行数据，它通常是更快地将预测值插入表中评分过程的一部分。  生成单个评分是更典型的场景，从窗体或用户请求，获取输入的值并返回到客户端应用程序的分数中。 为了提高性能，当生成连续的分数时，SQL Server 可能会缓存模型，以便可以重新加载到内存。

若要支持快速评分，SQL Server 机器学习服务 （和 Microsoft Machine Learning Server） 提供内置的计分库工作在 R 中或在 T-SQL 中使用的。 有不同的选项有具体取决于哪个版本。

**本机评分**

+ PREDICT 函数中 TRANSACT-SQL 支持_本机计分_SQL Server 2017 的任何实例中。 这只需要有已经过培训，可以调用使用 T-SQL 的一个模型。 使用 T-SQL 的本机计分相比具有以下优点：

    + 这种方式无需任何其他配置。
    + 不调用 R 运行时。 无需安装。

**实时评分**

+ **sp_rxPredict**实时评分可用于从任何支持的模型类型，生成分数而不会调用 R 运行时是存储的过程。

  此存储的过程也位于 SQL Server 2016 中，如果升级 R 组件使用的 Microsoft R Server 独立安装程序。 SQL Server 2017 还支持 sp_rxPredict。 因此，可能会使用此函数时使用 PREDICT 函数不支持的模型类型生成分数。

+ RxPredict 函数可用于快速评分 R 代码中。

对于所有这些计分方法的必须使用使用一个受支持的 RevoScaleR 或 MicrosoftML 算法训练的模型。

在操作中的实时评分的示例，请参阅[端到端贷款冲销预测构建使用 Azure HDInsight Spark 群集和 SQL Server 2016 R 服务](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>本机评分的工作原理

本机计分使用本机 c + + 库，microsoft 可以从特殊的二进制格式读取模型和生成评分。 由于一个模型可以单独发布和用于进行评分而无需调用 R 解释器，减少了多个进程交互的开销。 因此，本机计分支持更快的预测性能在企业生产方案中。

若要生成使用此库的分数，调用评分的函数，并传递所需的以下输入：

+ 兼容的模型。 请参阅[要求](#Requirements)部分了解详细信息。
+ 输入的数据，通常定义为 SQL 查询

该函数返回输入数据以及你想要传递的源数据的任何列的预测。

有关代码示例，以及如何准备所需的二进制格式中的模型，请参阅这篇文章的说明：

+ [如何执行实时评分](r/how-to-do-realtime-scoring.md)

一个包含本机计分的完整解决方案，请参阅 SQL Server 开发团队的这些示例：

+ 部署机器学习脚本：[使用 Python 模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ 部署机器学习脚本：[使用 R 模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)

## <a name="requirements"></a>要求

支持的平台是按如下所示：

+ SQL Server 2017 机器学习服务 （包括 Microsoft R Server 9.1.0）
    
    本机计分使用 PREDICT 需要 SQL Server 2017。
    它适用于任何版本的 SQL Server 2017，包括 Linux。

    您还可以执行实时评分使用 sp_rxPredict。 若要使用此存储的过程，您需要启用[SQL Server CLR 集成](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)。

+ SQL Server 2016

   实时评分使用 sp_rxPredict 可以实现的 SQL Server 2016，并还可以在 Microsoft R Server 上运行。 此选项要求 SQLCLR 若要启用，并安装 Microsoft R Server 升级。
   有关详细信息，请参阅[实时评分](Real-time-scoring.md)

### <a name="model-preparation"></a>模型准备

+ 必须事先使用某个受支持训练模型**rx**算法。 有关详细信息，请参阅[支持的算法](#bkmk_native_supported_algos)。
+ 必须使用 Microsoft R Server 9.1.0 中提供的新序列化函数保存模型。 序列化函数经过优化，可支持快速评分。

### <a name="bkmk_native_supported_algos"></a> 支持本机计分的算法

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

如果您需要使用 MicrosoftML 中的模型，使用与 sp_rxPredict 实时评分。

### <a name="restrictions"></a>限制

不支持以下模型类型：

+ 模型包含其他、 不受支持类型的 R 转换
+ 使用情况建模`rxGlm`或`rxNaiveBayes`RevoScaleR 中的算法
+ PMML 模型
+ 使用其他 R 库从 CRAN 或其他存储库中创建的模型
+ 模型包含任何其他 R 转换

## <a name="see-also"></a>另请参阅

[实时 SQL Server 机器学习中评分 ](real-time-scoring.md)