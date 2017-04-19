---
title: "通过 R 进行数据浏览和预测性建模 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: 20
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 220405d5131bb79f72e51028b9388975788acc86
ms.lasthandoff: 04/11/2017

---
# <a name="data-exploration-and-predictive-modeling-with-r"></a>通过 R 进行数据浏览和预测性建模
  数据科学家经常使用 R 来浏览数据并构建预测模型。 此过程通常需要反复经历各种尝试和错误才能获得良好的预测模型。 有经验的数据科学家会使用 RODBC 包连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库并将数据提取到本地工作站，然后对数据进行浏览，最后再使用标准 R 包构建预测模型。  
  
 但是，这种方法有缺点。 数据移动可能速度慢、效率不高或安全性不好，而 R 本身也存在性能和规模限制。 当你需要移动和分析大量数据，或者使用的数据集不适合计算机上可供使用的内存时，这些缺点就会变得更明显。  
  
 你可以使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]随附的新的可伸缩包和 R 函数来克服这些困难。 **RevoScaleR** 包包含部分最常用 R 函数的实现，这些实现在经过重新设计后可提供并行度和缩放功能。 RevoScaleR 包还允许更改 *执行上下文*。 这意味着，不管是完整解决方案还是单个函数，都应使用托管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机的资源进行计算，而不应使用本地工作站。 这样做有很多好处：避免不必要的数据移动，并可利用服务器计算机上更强大的计算资源。  
  
 本部分将指导数据科学家正确使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 并正确执行与 R 解决方案的开发和测试相关的任务。  
  
##  <a name="bkmk_RDevTools"></a> R 开发工具  
 Microsoft R 客户端为数据科学家提供了一个开发和测试预测模型的完整环境。 R 客户端包括：  
  
-  **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]：**R 运行时的一个分发版以及一组包（例如 Intel 数学内核库），用于提升标准 R 操作的性能。  
  
-   **RevoScaleR：**一个可用来将计算推送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 R 包。 [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]。 它还包括一组常用 R 函数，这些函数在重新设计后具有更好的性能和可伸缩性。 你可以通过 **rx** 前缀来标识这些性能已改善的函数。 它还包括了针对各种源的增强数据提供程序；这些函数具有前缀 **Rx**。  
  
-   **可以免费选用的开发工具：**你可以使用支持 R 的任何基于 Windows 的代码编辑器，例如 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 或 RStudio。 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] 的下载包还包括 R 的常用命令行工具，例如 RGui.exe。  
  
##  <a name="bkmk_packages"></a> R 环境和包  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中支持的 R 环境包含运行时、开源语言，以及多个包所支持和扩展的图形引擎。 该语言允许使用通过包实现的多种扩展。  
  
 可以通过多个来源获取其他 R 包，将之用于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ：  
  
  
-   公共存储库提供的通用 R 包。 你可以从公共存储库（例如 CRAN，托管 6000 多个可供数据科学家使用的包）获取最常用的开源 R 包。  
  
     此外还有支持特殊领域（例如财务、基因组等）预测分析的包。  
  
     对于 Windows 平台，R 包以 zip 文件形式提供，可以在获得 GPL 许可的情况下下载和安装。  
  
     有关如何安装适用于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]的第三方包的信息，请参阅 [Install Additional R Packages on SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
-   [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]提供的其他包和库。   
  
     **RevoScaleR** 包包括高性能大数据分析、支持常用数据科学任务的改进版函数、适用于 Naive Bayes 的优化学习模型、线性回归、时序模型、神经网络以及高级数学库。  
  
     **RevoPemaR** 包允许你在 R 中开发自己的并行外部存储器算法。  
  
     有关这些包以及如何使用它们的详细信息，请参阅[数据浏览和预测性建模（教程：SQL Server R Services）](http://msdn.microsoft.com/library/65589d17-bd34-4baa-8ba1-998f60d0344f)。  
  
## <a name="using-data-sources-and-compute-contexts"></a>使用数据源和计算上下文  
 使用 RevoScaleR 包连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，可以在 R 代码中使用一些重要的新函数：  
  
-   [RxSqlServerData](http://msdn.microsoft.com/library/0d2c53a6-b64b-4760-9903-825238b772d6) 是 RevoScaleR 包中提供的函数，支持通过改进型数据连接来连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]随附的新的可伸缩包和 R 函数来克服这些困难。  
  
     可以在 R 代码中使用此函数来定义 *数据源*。 数据源对象指定数据所在的服务器和表，并管理在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中读写数据的任务。  
  
-   [RxInSqlServer](http://msdn.microsoft.com/library/24bd1f0a-ec68-4b96-bf42-a4073014f1f1) 函数可用来指定计算上下文。  换言之，你可以指定执行 R 代码的位置：本地工作站或托管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机。  
  
     当你设置计算上下文时，该上下文仅影响支持远程执行上下文的计算，即 RevoScaleR 包及相关函数提供的 R 操作。 通常，基于标准 CRAN 包的 R 解决方案不能在远程计算上下文中运行，但如果是由 T-SQL 启动的，则它们可以在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机上运行。 不过，你可以使用 `rxExec` 函数调用各个 R 函数并在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中远程运行它们。  
  
 有关如何创建和使用数据源和执行上下文的示例，请参阅以下教程：
 
 + [对数据科学的深入探讨](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
 +  [RevoScaleR SQL Server 入门](https://msdn.microsoft.com/microsoft-r/scaler-sql-server-getting-started)。  
  
## <a name="deploying-your-r-code-to-production"></a>将 R 代码部署到生产  
 数据科学的一个重要部分是将你的分析提供给他人，或者使用预测模型来改善业务成果或流程。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，当 R 脚本或模型就绪以后，可以轻松地转移到生产。  
  
 有关如何将代码转移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的第三方包的信息，请参阅 [Operationalizing Your R Code](../../advanced-analytics/r-services/operationalizing-your-r-code.md)随附的新的可伸缩包和 R 函数来克服这些困难。  
  
 通常情况下，在开始部署时会对脚本进行清除，去掉生产过程中不需要的脚本。 随着你将计算移动到更靠近数据的位置，你可能会发现更高效的方法来移动、汇总或呈现数据，而不是任何事情都通过 R 来执行。  
  
 我们建议数据科学家向数据库开发人员咨询提高性能的方法，特别是当解决方案执行采用 SQL 时可能更为高效的数据清理或功能工程时。 可能需要更改 ETL 流程来确保模型的构建或评分工作流不会失败，并可能需要以正确格式提供输入数据。  
  
##  <a name="bkmk_SQLInR"></a> 本节内容  

[ScaleR 函数和 CRAN R 函数之对比](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions2)

[用于处理 SQL Server 的 ScaleR 函数](../../advanced-analytics/r-services/scaler-functions-for-working-with-sql-server-data.md)
   
## <a name="see-also"></a>另请参阅  

 
 [SQL Server R 服务功能和任务](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 
 [Operationalizing Your R Code](../../advanced-analytics/r-services/operationalizing-your-r-code.md)  
  
  

