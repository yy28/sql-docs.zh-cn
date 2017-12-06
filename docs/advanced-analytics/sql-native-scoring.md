---
title: "本机评分 |Microsoft 文档"
ms.custom: 
ms.date: 09/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 8cce800526dbf89da77508713b4dd2aa2eead4ae
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="native-scoring"></a>本机评分

本主题介绍 SQL Server 2017 对以近实时的机器学习模型提供评分的功能。

+ 什么是本机评分与实时评分
+ 工作方式
+ 支持的平台和要求

## <a name="what-is-native-scoring-and-how-is-it-different-from-realtime-scoring"></a>什么是本机评分，方式是不同于实时评分？

在 SQL Server 2016 中，Microsoft 创建了一种扩展性框架，允许要在执行从 T-SQL 的 R 脚本。 此框架支持在 R 中，从简单的函数到培训复杂机器学习模型不等，可能执行任何操作。 但是，双过程体系结构需要调用外部 R 进程对于每个调用，而不考虑该操作的复杂性。 如果要从表和已在 SQL Server 中的数据对其评分加载预先训练的模型，则调用外部 R 进程的开销表示不必要的性能成本。

_评分_过程分为两步。 首先，你指定一个预先训练的模型，用于从表加载。 其次，传递新输入的函数，以生成预测值的数据 (或_评分_)。 输入可以是表格或单个行。 你可以选择输出单个列的值表示的概率，也可能会输出一些值，如置信区间、 错误或其他有用的补数与预测。

当输入包含很多行数据时，通常是更快地将预测值插入表评分过程的一部分。  在您从窗体或用户请求，获取输入的值并返回到客户端应用程序的分数方案中更常见的是生成单个评分。 若要提高性能，生成连续评分时，SQL Server 可能缓存模型，以便可以重新加载到内存。

若要支持快速评分，SQL Server 机器学习服务 （和 Microsoft 机器学习服务器），请提供内置在 R 中或在 T-SQL 中工作的评分库。 有您有具体取决于哪个版本的不同选项。

**本机评分**

+ 在 TRANSACT-SQL 中的预测函数支持_本机评分_的 SQL Server 2017 任何实例中。 它仅要求您具有已定型，可以调用使用 T-SQL 的该模型。 使用 T-SQL 的本机评分具有以下优势：

    + 这种方式无需任何其他配置。
    + 不调用 R 运行时。 无需来安装。

**实时评分**

+ **sp_rxPredict**实时评分，可以用于从任何支持的模型类型，而不会调用 R 运行时生成的分数是存储的过程。

  此存储的过程也会提供在 SQL Server 2016 中，如果升级使用的 Microsoft R Server 独立安装程序的 R 组件。 SQL Server 2017 还支持 sp_rxPredict。 因此，你可能会使用此函数时使用预测函数不支持的模型类型生成评分。

+ RxPredict 函数可以用于在 R 代码中的快速评分。

对于所有这些计分方法的你必须使用模型进行定型使用支持的 RevoScaleR 或 MicrosoftML 算法之一。

有关实时操作中评分的示例，请参阅[端到端贷款 ChargeOff 预测生成使用 Azure HDInsight Spark 群集和 SQL Server 2016 R 服务](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>如何本机评分正常工作

本机评分使用从 Microsoft 可从特殊的二进制格式读取模型和生成评分的本机 c + + 库。 由于模型可以单独发布和用于评分而无需调用 R 解释程序，减少了多个流程的互操作的开销。 因此，本机评分支持更快的预测性能企业生产方案中。

若要生成使用此库的评分，调用评分函数，并传递以下必需的输入：

+ 兼容的模型。 请参阅[要求](#Requirements)部分了解详细信息。
+ 输入的数据，通常定义为 SQL 查询

该函数返回输入数据，以及你想要传递的源数据的任何列的预测。

有关代码示例，以及如何准备所需的二进制格式中的模型，请参阅此文章的说明：

+ [如何执行实时评分](r/how-to-do-realtime-scoring.md)

有关完整的解决方案，其中包含本机评分，请参阅 SQL Server 开发团队的这些示例：

+ 部署你的 ML 脚本：[使用 Python 模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ 部署你的 ML 脚本：[使用 R 模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)

## <a name="requirements"></a>要求

支持的平台是，如下所示：

+ SQL Server 自 2017 年 1 机器学习服务 （包括 Microsoft R Server 9.1.0）
    
    使用预测本机评分需要 SQL Server 自 2017 年。
    它适用于任何版本的 SQL Server 2017，包括 Linux。

    你还可以执行实时评分使用 sp_rxPredict。 若要使用此存储的过程要求你启用[SQL Server CLR 集成](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)。

+ SQL Server 2016

   实时评分使用 sp_rxPredict，可以使用 SQL Server 2016，并还可以在 Microsoft R Server 上运行。 此选项需要 SQLCLR 启用，并安装 Microsoft R Server 升级。
   有关详细信息，请参阅[实时评分](Real-time-scoring.md)

### <a name="model-preparation"></a>模型准备

+ 必须事先使用支持之一定型模型**rx**算法。 有关详细信息，请参阅[支持算法](#bkmk_native_supported_algos)。
+ 必须使用新的序列化函数提供 Microsoft R Server 9.1.0 中保存模型。 序列化函数进行了优化以支持快速评分。

### <a name="bkmk_native_supported_algos"></a>支持本机评分的算法

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

如果你需要使用从 MicrosoftML 的模型，使用实时 sp_rxPredict 评分。

### <a name="restrictions"></a>限制

不支持以下模型类型：

+ 模型包含其他、 不受支持类型的 R 转换
+ 模型使用`rxGlm`或`rxNaiveBayes`中 RevoScaleR 算法
+ PMML 模型
+ 使用其他 R 库从 CRAN 或其他存储库创建的模型
+ 模型包含任何其他 R 转换
