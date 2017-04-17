---
title: "SQL Server 2016 技术文档 | Microsoft Docs"
ms.date: 03/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.portal.f1
helpviewer_keywords:
- documentation [SQL Server], home page
- Help [SQL Server]
- SQL Server, documentation
- home page [SQL Server]
- Help [SQL Server], documentation home page
- Books Online [SQL Server], home page
- portal page [SQL Server]
ms.assetid: 674933a8-e423-4d44-a39b-2a997e2c2333
caps.latest.revision: 106
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 034e10f491c3c327d6a7b2a044f57121636c3c06
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-technical-documentation"></a>SQL Server 技术文档
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

 用于帮助安装、配置和使用 SQL Server&2016; 的文档。 内容包括端到端示例、代码示例和视频。 有关 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 语言的主题，请参阅 [语言参考](../t-sql/language-reference.md)。

**SQL Server vNext**

有关最新版本的说明，请参阅 [SQL Server vNext 版本说明](../sql-server/sql-server-vnext-release-notes.md)

有关新增功能的最新信息，请参阅 [SQL Server vNext 中的新增功能](../sql-server/what-s-new-in-sql-server-vnext.md)
 
**SQL Server 2016：**
 
 [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)

[SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)
    
 **试用 SQL Server！**    
    
 - [**从评估中心下载 SQL Server 2016**](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)    
    
- **[加速已安装有 SQL Server 2016 的虚拟机](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**    
    
-  **[下载 SQL Server Management Studio 的最新版本](https://msdn.microsoft.com/library/mt238290.aspx)**   
    
  
    
## <a name="sql-server-technologies"></a>SQL Server 技术    
    
|||    
|-|-|    
|![SQL 数据库引擎](../sql-server/media/sql-database-engine.png "SQL 数据库引擎")|**[数据库引擎](../database-engine/configure-windows/sql-server-database-engine.md)**<br /><br /> 数据库引擎是用于存储、处理和保护数据的核心服务。 数据库引擎提供了受控访问和快速事务处理，以满足企业内最苛刻的数据消费应用程序的要求。 数据库引擎还提供了大量的支持以保持高可用性。|    
|![R Server](../sql-server/media/r-server.png "R Server")|**[R Services](../advanced-analytics/r-services/r-services.md)**<br /><br /> Microsoft R 服务提供了多种将受欢迎的 R 语言并入企业工作流的方法。<br /><br /> [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] 将 R 语言与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]集成，以便轻松通过调用 [!INCLUDE[tsql](../includes/tsql-md.md)] 存储过程生成、重新导流模型，并对模型评分。<br /><br /> Microsoft R Server 在企业中为 R 提供多平台可扩展支持，并且支持 Hadoop 和 Teradata 等数据源。|    
|![Data Quality Services](../sql-server/media/data-quality-services.png "Data Quality Services")|**[Data Quality Services](../data-quality-services/data-quality-services.md)**<br /><br /> SQL Server Data Quality Services (DQS) 向您提供知识驱动型数据清理解决方案。 DQS 使您可以生成知识库，然后使用此知识库，同时采用计算机辅助方法和交互方法，执行数据更正和消除重复的数据。 您可以使用基于云的引用数据服务，并可以生成一个数据管理解决方案将 DQS 与 SQL Server Integration Services 和 Master Data Services 相集成。|    
|![Integration Services](../sql-server/media/integration-services.png "Integration Services")|**[Integration Services](../integration-services/sql-server-integration-services.md)**<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是一个生成高性能数据集成解决方案的平台，其中包括对数据仓库提供提取、转换和加载 (ETL) 处理的包。|    
|![Master Data Services](../sql-server/media/master-data-services.png)|**[Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)**<br /><br /> [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 是用于主数据管理的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 解决方案。 基于 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 生成的解决方案可帮助确保报表和分析均基于适当的信息。 使用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]，您可以为主数据创建中央存储库，并随着主数据随时间变化而维护一个可审核的安全对象记录。|    
|![Analysis Services](../sql-server/media/analysis-services.png "Analysis Services")|**[Analysis Services](../analysis-services/analysis-services.md)**<br /><br /> [!INCLUDE[ssASnoversion_md](../includes/ssasnoversion-md.md)] 是一个针对个人、团队和公司商业智能的分析数据平台和工具集。 服务器和客户端设计器通过使用 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]、Excel 和 SharePoint Server 环境，支持传统的 OLAP 解决方案、新的表格建模解决方案以及自助式分析和协作。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 还包括数据挖掘，以便你可以发现隐藏在大量数据中的模式和关系。|    
|![复制服务](../sql-server/media/replication-services.png "复制服务")|**[复制](../relational-databases/replication/sql-server-replication.md)**<br /><br /> 复制是一组技术，用于在数据库间复制和分发数据和数据库对象，然后在数据库间进行同步操作以维持一致性。 使用复制时，可以通过局域网和广域网、拨号连接、无线连接和 Internet，将数据分发到不同位置以及分发给远程用户或移动用户。|    
|![Reporting Services](../sql-server/media/reporting-services.png "Reporting Services")|**[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)**<br /><br /> Reporting Services 提供企业级的 Web 报表功能，从而使您可以创建从多个数据源提取数据的表，发布各种格式的表，以及集中管理安全性和订阅。|    
     
   
 ## <a name="more-information"></a>详细信息   
+ [SQL Server 配置管理器](../relational-databases/sql-server-configuration-manager.md)
+ [SQL Server 更新中心](https://msdn.microsoft.com/library/ff803383.aspx) 链接和有关所有受支持版本的信息 
+ [安装 SQL Server 数据库引擎](../database-engine/install-windows/install-sql-server-database-engine.md) 
+ [安装带有 SSMS 的 SQL Server 管理工具](https://msdn.microsoft.com/library/bb500441.aspx) 
+ [Visual Studio 2015 中的 SQL Server Data Tools](https://msdn.microsoft.com/mt186501.aspx)
+ [视频、示例和社区资源](https://msdn.microsoft.com/library/dn237258.aspx)
+ [SQL Server 2016 简介](https://www.microsoft.com/en-us/server-cloud/products/sql-server/default.aspx?WT.srch=1&WT.mc_id=SEM_%5B_uniqid%5D&utm_source=Bing&utm_medium=CPC&utm_term=SQL%20Server%202016&utm_campaign=Data_Management)  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect-md](../includes/feedback-stackoverflow-msdn-connect-md.md)]


