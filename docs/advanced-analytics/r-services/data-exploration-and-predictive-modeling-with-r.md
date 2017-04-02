---
title: "通过 R 进行数据浏览和预测性建模 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# 通过 R 进行数据浏览和预测性建模
  数据科学家经常使用 R 来浏览数据并构建预测模型。 此过程通常需要反复经历各种尝试和错误才能获得良好的预测模型。 有经验的数据科学家会使用 RODBC 包连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库并将数据提取到本地工作站，然后对数据进行浏览，最后再使用标准 R 包构建预测模型。  
  
 但是，这种方法有缺点。 数据移动可能速度慢、效率不高或安全性不好，而 R 本身也存在性能和规模限制。 当你需要移动和分析大量数据，或者使用的数据集不适合计算机上可供使用的内存时，这些缺点就会变得更明显。  
  
 可以通过使用新的可扩展包来克服这些难题和 R 函数附带 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 **RevoScaleR** 包包含部分最常用 R 函数的实现，这些实现在经过重新设计后可提供并行度和缩放功能。 RevoScaleR 包还允许更改 *执行上下文*。 这意味着，不管是完整解决方案还是单个函数，都应使用托管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机的资源进行计算，而不应使用本地工作站。 这样做有很多好处：避免不必要的数据移动，并可利用服务器计算机上更强大的计算资源。  
  
 本部分将指导数据科学家正确使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 并正确执行与 R 解决方案的开发和测试相关的任务。  
  
##  <a name="bkmk_RDevTools"></a> R 开发工具  
 Microsoft R 客户端为数据科学家提供了一个完整的环境，用于开发和测试预测模型。 R 客户端包括︰  
  
-  **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** R 运行时和提升的标准 R 操作性能的包，如 Intel 数学内核库，一组分发。  
  
-   **RevoScaleR:** R 包，您可以将计算推送到的实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]。 它还包括一组常见已经过重新设计，以提供更好的性能和可伸缩性的 R 函数。 你可以通过 **rx** 前缀来标识这些性能已改善的函数。 它还包括增强的数据提供程序不同的源;这些函数具有前缀 **Rx**。  
  
-   **免费开发工具的选择︰** 可以使用任何基于 Windows 的代码编辑器，如支持 R、 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 或 RStudio。 下载 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] 还包括常用的命令行工具，用于如 RGui.exe R。  
  
##  <a name="bkmk_packages"></a> R 环境和包  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中支持的 R 环境包含运行时、开源语言，以及多个包所支持和扩展的图形引擎。 该语言允许使用通过包实现的多种扩展。  
  
 可以通过多个来源获取其他 R 包，将之用于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ：  
  
  
-   从公共存储库的一般用途的 R 包。 你可以从公共存储库（例如 CRAN，托管 6000 多个可供数据科学家使用的包）获取最常用的开源 R 包。  
  
     此外还有支持特殊领域（例如财务、基因组等）预测分析的包。  
  
     Windows 平台上，为多个 R 包以 zip 文件形式提供和可以下载并安装带有 GPL 许可证。  
  
     有关如何安装适用于第三方程序包的信息 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，请参阅 [SQL Server 上安装其他 R 包](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
-   其他软件包和由提供的库 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。   
  
      **RevoScaleR** 包包括高性能大数据分析，支持常见数据科学任务，对于 Naive Bayes、 线性回归，时序模型，神经网络和高级的数学库的最佳学习器的函数的改进版本。  
  
     **RevoPemaR** 包允许你在 R 中开发自己的并行外部存储器算法。  
  
     有关这些包以及如何使用它们的详细信息，请参阅 [数据浏览和预测性建模 & #40;教程︰ SQL Server R 服务 & #41;](../../advanced-analytics/r-services/sql-server-r-services.md)。  
  
## 使用数据源和计算上下文  
 当使用 RevoScaleR 包连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，有一些在 R 代码中使用的重要新功能︰  
  
-   [RxSqlServerData](RxSqlServerData.md) 是要支持改进的数据连接到的 RevoScaleR 程序包中提供一个函数 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
     可以在 R 代码中使用此函数来定义 *数据源*。 数据源对象指定数据所在的服务器和表，并管理在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中读写数据的任务。  
  
-    [RxInSqlServer](rxInSqlServer.md) 函数可以用于指定 *计算上下文*。  换而言之，您可以指示应执行的 R 代码的位置︰ 在本地工作站上或承载的计算机上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
     设置计算上下文，它也会影响仅支持远程执行上下文，这意味着 R 操作提供的 RevoScaleR 包和相关函数的计算。 通常情况下，基于标准 CRAN 软件包的 R 解决方案无法在运行的远程计算上下文，但它们可以运行在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 如果通过 T-SQL 启动计算机。 但是，您可以使用 `rxExec` 函数来调用各个 R 函数，然后在远程运行这些 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。  
  
 有关如何创建和使用数据源和执行上下文的示例，请参阅三个教程︰
 
 + [数据科学深入了解](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
 +  [RevoScaleR SQL Server 入门](https://msdn.microsoft.com/microsoft-r/rserver/rserver-scaler-sql-server-getting-started)。  
  
## 将 R 代码部署到生产  
 数据科学的一个重要部分是将你的分析提供给他人，或者使用预测模型来改善业务成果或流程。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，当 R 脚本或模型就绪以后，可以轻松地转移到生产。  
  
 有关如何将您的代码在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，请参阅 [留给 R 代码](../../advanced-analytics/r-services/operationalizing-your-r-code.md)。  
  
 通常情况下，在开始部署时会对脚本进行清除，去掉生产过程中不需要的脚本。 对数据移动计算更近时，您可能会发现更高效地移动、 汇总或显示比 R.中的所有内容的数据的方法  
  
 我们建议数据科学家咨询数据库开发人员关于如何提高性能，尤其是在该解决方案可进行数据清理或功能工程，可能是在 SQL 中更有效。 可能需要对 ETL 过程的更改来确保工作流构建或评分模型不会发生故障，并且可用采用正确的格式输入的数据。  
  
##  <a name="bkmk_SQLInR"></a> 本节内容  

[ScaleR 函数和 CRAN R 函数的比较](Summary%20of%20rx%20Functions.md)

[与 SQL Server 一起使用的 scaleR 函数](../../advanced-analytics/r-services/scaler-functions-for-working-with-sql-server-data.md)
   
## 另请参阅  

 
 [SQL Server R 服务功能和任务](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 
 [实现 R 代码](../../advanced-analytics/r-services/operationalizing-your-r-code.md)  
  
  