---
title: "通过 R 进行数据浏览和预测性建模 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 04/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: "20"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a64db58ce05675a3a2ac30e0bcea0d3924731a08
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="data-exploration-and-predictive-modeling-with-r"></a>通过 R 进行数据浏览和预测性建模

本主题介绍可通过与 SQL Server 的集成到数据科学过程改进。

适用于： SQL Server 2016 R Services、 SQL Server 自 2017 年机 Learnign 服务

## <a name="the-data-science-process"></a>数据科学过程

数据科学家经常使用 R 来浏览数据并构建预测模型。 此过程通常需要反复经历各种尝试和错误才能获得良好的预测模型。 有经验的数据科学家会使用 RODBC 包连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库并将数据提取到本地工作站，然后对数据进行浏览，最后再使用标准 R 包构建预测模型。

但是，这种方法存在许多缺点，该 hae 影响企业中的广泛地采用了 R。 

+ 数据移动可能速度慢、 效率低下，或不安全
+ R 本身也存在性能和规模限制

当你需要移动和分析大量数据，或者使用的数据集不适合计算机上可供使用的内存时，这些缺点就会变得更明显。

新的、 可扩展的包和随附的 R 函数[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]帮助你克服这些难题的许多。 

## <a name="whats-different-about-revoscaler"></a>有关 RevoScaleR 差别是什么？

**RevoScaleR** 包包含部分最常用 R 函数的实现，这些实现在经过重新设计后可提供并行度和缩放功能。 有关详细信息，请参阅[分布式计算使用 RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)。

RevoScaleR 包还允许更改 *执行上下文*。 这意味着，不管是完整解决方案还是单个函数，都应使用托管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机的资源进行计算，而不应使用本地工作站。 这样做有很多好处：避免不必要的数据移动，并可利用服务器计算机上更强大的计算资源。

## <a name="r-environment-and-packages"></a>R 环境和包

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中支持的 R 环境包含运行时、开源语言，以及多个包所支持和扩展的图形引擎。 该语言允许使用通过包实现的多种扩展。  

### <a name="using-other-r-packages"></a>使用其他 R 包

除了 Microsoft 机器学习中包含的专有 R 库，你可以在解决方案中，使用几乎任何 R 包包括：

+ 公共存储库提供的通用 R 包。 你可以从公共存储库（例如 CRAN，托管 6000 多个可供数据科学家使用的包）获取最常用的开源 R 包。
  
  对于 Windows 平台，R 包以 zip 文件形式提供，可以在获得 GPL 许可的情况下下载和安装。  
  
  有关如何安装适用于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]的第三方包的信息，请参阅 [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]提供的其他包和库。   
  
     **RevoScaleR** 包包括高性能大数据分析、支持常用数据科学任务的改进版函数、适用于 Naive Bayes 的优化学习模型、线性回归、时序模型、神经网络以及高级数学库。  
  
     **RevoPemaR** 包允许你在 R 中开发自己的并行外部存储器算法。  
  
     有关这些程序包以及如何使用它们的详细信息，请参阅[什么是 RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction)和[入门 RevoPemaR](https://msdn.microsoft.com/microsoft-r/pemar-getting-started)。 

+ **MicrosoftML**包含高度优化的机器学习算法和数据从 Microsoft 数据科学团队的转换的集合。 许多算法还在 Azure 机器学习中使用。 有关详细信息，请参阅[使用 MicrosoftML 包](../../advanced-analytics/using-the-microsoftml-package.md)。

### <a name="r-development-tools"></a>R 开发工具

当开发 R 解决方案，请务必下载 Microsoft R 客户端。 此免费下载内容还包括支持远程计算上下文和可扩展 alorithms 所需的库：

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]：**R 运行时的一个分发版以及一组包（例如 Intel 数学内核库），用于提升标准 R 操作的性能。  
  
+ **RevoScaleR：**一个可用来将计算推送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 R 包。 [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]。 它还包括一组常用 R 函数，这些函数在重新设计后具有更好的性能和可伸缩性。 你可以通过 **rx** 前缀来标识这些性能已改善的函数。 它还包括了针对各种源的增强数据提供程序；这些函数具有前缀 **Rx**。

你可以使用支持 R，如任何基于 Windows 的代码编辑器[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]或 RStudio。 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] 的下载包还包括 R 的常用命令行工具，例如 RGui.exe。

## <a name="use-new-data-sources-and-compute-contexts"></a>使用新数据源和计算上下文

当使用 RevoScaleR 包连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，查找在 R 代码中使用这些函数：

+ **RxSqlServerData** 是 RevoScaleR 包中提供的函数，支持通过改进型数据连接来连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]随附的新的可伸缩包和 R 函数来克服这些困难。
  
     可以在 R 代码中使用此函数来定义 *数据源*。 数据源对象指定数据所在的服务器和表，并管理在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中读写数据的任务。
  
-   **RxInSqlServer** 函数可用来指定计算上下文。  换言之，你可以指定执行 R 代码的位置：本地工作站或托管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机。  有关详细信息，请参阅[RevoScaleR 函数](https://msdn.microsoft.com/microsoft-r/scaler/scaler)。
  
     当你设置计算上下文时，该上下文仅影响支持远程执行上下文的计算，即 RevoScaleR 包及相关函数提供的 R 操作。 通常，基于标准 CRAN 包的 R 解决方案不能在远程计算上下文中运行，但如果是由 T-SQL 启动的，则它们可以在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机上运行。 不过，你可以使用 `rxExec` 函数调用各个 R 函数并在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中远程运行它们。

有关如何创建和使用数据源和执行上下文的示例，请参阅以下教程：

+ [对数据科学的深入探讨](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [使用 Microsoft R 数据分析](https://msdn.microsoft.com/en-us/microsoft-r/data-analysis-in-microsoft-r)

## <a name="deploy-r-code-to-production"></a>将 R 代码部署到生产

数据科学的一个重要部分是将你的分析提供给他人，或者使用预测模型来改善业务成果或流程。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，当 R 脚本或模型就绪以后，可以轻松地转移到生产。

有关如何将代码转移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的第三方包的信息，请参阅 [Operationalizing Your R Code](../../advanced-analytics/r/operationalizing-your-r-code.md)随附的新的可伸缩包和 R 函数来克服这些困难。

通常情况下，在开始部署时会对脚本进行清除，去掉生产过程中不需要的脚本。 当你将计算更接近移到数据时，可能会发现如何更有效地移动、 汇总，或存在比。 中的所有内容的数据 我们建议数据科研人员咨询数据库开发人员，了解如何提高性能，尤其是如果解决方案执行数据清理或工程的功能可能是 SQL 中更有效。 可能需要更改 ETL 流程来确保模型的构建或评分工作流不会失败，并可能需要以正确格式提供输入数据。

## <a name="see-also"></a>另请参阅

[Base R 函数和 ScaleR 函数之对比](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)

[用于处理 SQL Server 的 ScaleR 函数](../../advanced-analytics/r/scaler-functions-for-working-with-sql-server-data.md)
