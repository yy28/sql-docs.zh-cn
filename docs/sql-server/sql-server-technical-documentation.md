---
title: "SQL Server 技术文档 | Microsoft Docs"
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: 
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
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: aad94f116c1a8b668c9a218b32372424897a8b4a
ms.openlocfilehash: 334c3d130a1d0c8371c1a7810d82d443e1fbecc8
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---
# <a name="sql-server-technical-documentation"></a>SQL Server 技术文档
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 > 有关与以前版本的 SQL Server 相关的内容，请参阅 [SQL Server 2014 安装](https://msdn.microsoft.com/en-US/library/bb500469(SQL.120).aspx)。

 用于帮助安装、配置和使用 SQL Server&2016; 的文档。 内容包括端到端示例、代码示例和视频。 有关 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 语言的主题，请参阅 [语言参考](../t-sql/language-reference.md)。

还可以使用帮助查看器来脱机查看 SQL Server 文档。 有关详细信息，请参阅 [SQL Server 的帮助查看器和脱机内容](../release-notes/sql-server-help-installation.md)。

**SQL Server 2017**

- [SQL Server 2017 发行说明](../sql-server/sql-server-2017-release-notes.md)
- [SQL Server 2017 的新增功能](../sql-server/what-s-new-in-sql-server-2017.md)
 
**SQL Server 2016：**
 
- [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)
- [SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)
    
 **试用 SQL Server！**    
 - [**从评估中心下载 SQL Server 2016**](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) 
 - **[加速已安装有 SQL Server 2016 的虚拟机](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**    
 - **[下载 SQL Server Management Studio 的最新版本](https://msdn.microsoft.com/library/mt238290.aspx)**   
      
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

    
## <a name="earlier-sql-server-versions"></a>早期 SQL Server 版本
- [SQL Server 2014 联机丛书](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx)
- [安装 SQL Server 2014 Express 和其他较旧的 SQL Server 版本](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)。 （**感谢你参与 [Scott Hanselman](http://www.hanselman.com/) 的演讲，了解如何将所有安装程序包链接收集到一个地方！**）  
- [SQL Server 2012 技术文档](https://technet.microsoft.com/library/bb418433(v=sql.10).aspx)  
- [SQL Server 2008 R2 产品文档](https://msdn.microsoft.com/library/hh278298(v=sql.10).aspx)  
- [SQL Server 2008 技术文档](https://msdn.microsoft.com/library/hh994727(v=sql.10).aspx) 
- [SQL Server 2005 存档文档](https://msdn.microsoft.com/library/hh278313(v=sql.10).aspx)    

**示例数据库**  
- [Wide World Importers 示例数据库](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)  
- [适用于 SQL Server 2016 的 AdventureWorks 示例数据库和脚本](https://www.microsoft.com/en-us/download/details.aspx?id=49502) 
- [GitHub 上的 SQL Server 示例](https://github.com/Microsoft/sql-server-samples) 
   
 ## <a name="more-information"></a>详细信息   
+ [SQL Server 配置管理器](../relational-databases/sql-server-configuration-manager.md)
+ [SQL Server 更新中心](https://msdn.microsoft.com/library/ff803383.aspx) 链接和有关所有受支持版本的信息 
+ [安装 SQL Server 数据库引擎](../database-engine/install-windows/install-sql-server-database-engine.md) 
+ [安装带有 SSMS 的 SQL Server 管理工具](https://msdn.microsoft.com/library/bb500441.aspx) 
+ [Visual Studio 2015 中的 SQL Server Data Tools](https://msdn.microsoft.com/mt186501.aspx)
+ [视频、示例和社区资源](https://msdn.microsoft.com/library/dn237258.aspx)
  
[!INCLUDE[feedback_stackoverflow_msdn_connect-md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

