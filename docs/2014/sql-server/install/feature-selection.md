---
title: 功能选择 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- feature selection, Setup
helpviewer_keywords:
- SQL Server Installation Wizard, Components to Install page
- Components to Install page [SQL Server Installation Wizard]
ms.assetid: 73182088-153b-4634-a060-d14d1fd23b70
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cedec01a7e8c7da94f75c00e377a2c965bd58c7d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087407"
---
# <a name="feature-selection"></a>功能选择
  使用  安装向导的“功能选择” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 页上的复选框为您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装选择组件。  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-features"></a>安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能  
 在 **“功能选择”** 页上， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能分为两个主要部分： **“实例功能”** 和 **“共享功能”**。  
  
 **实例功能** 表示为每个实例安装一次的组件，这样，你将具有它们的多个副本（每个实例一个）。 每个实例都可以是具有不同修补程序级别的单独版本。 在您安装某一修补程序时，无论该修补程序是 Service Pack、修补程序还是累积更新，它都仅更新给定计算机上一个实例的文件，并且还会更新共享功能（如果这些共享功能尚未更新）。  
  
 **“共享功能”** 是指给定计算机上所有实例所共有的功能。 上述每个共享功能都设计为与可并行安装的支持的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本向后兼容（Service Pack、累积更新和修补程序）。  
  
> [!NOTE]  
>  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集：**[!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 组件是仅有的两个支持故障转移群集的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能。 可以在故障转移群集节点上安装其他组件，如 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，但这些组件不能识别群集，因此当该故障转移群集节点脱机时，这些组件的服务不进行故障转移。 有关详细信息，请参阅 [AlwaysOn 故障转移群集实例 (SQL Server)](../failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)。  
  
### <a name="instance-features"></a>实例功能  
 选择各个组件组时， **“说明”** 窗格中会显示相应的说明。 您可以选中任意一些复选框。 若要继续，必须进行选择。  
  
|功能|Description|  
|--------------|-----------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 包括[!INCLUDE[ssDE](../../includes/ssde-md.md)]（用于存储、处理和保护数据安全的核心服务）、复制、全文搜索、用于管理关系数据和 XML 数据的工具以及 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 服务器。 数据库引擎的功能如下：<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)] 是用于存储、处理和保护数据的核心服务。<br /><br /> 复制：可选：复制是一组技术，用于将数据和数据库对象从一个数据库复制和分发到另一个数据库，然后在数据库之间进行同步以维护一致性。<br /><br /> 全文搜索：可选：全文搜索提供了针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中基于纯字符的数据发出全文查询的功能。<br /><br /> [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]： 可选： [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 是一种数据清理解决方案，使您能够发现数据源中的不一致和不正确数据并提供计算机辅助且交互式方法来清理您的数据。 选中此复选框将安装 DQS 服务器。 完成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装之后，您必须运行 DQSInstaller.exe 文件，才能 *完成* DQS 服务器安装。 如果你安装的 SQL server 默认实例，此文件是位于 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。MSSQLSERVER\MSSQL\Binn。<br /><br /> <br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集：** 选择“数据库引擎服务”时，复制和全文搜索组件是必需的，并由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集安装的安装程序自动选择。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包括一些工具，可用于创建和管理联机分析处理 (OLAP) 以及数据挖掘应用程序。|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] – 本机|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式包括用于创建、管理和部署表格报表、矩阵报表、图形报表以及自由格式报表的服务器和客户端组件。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 还是一个可用于开发报表应用程序的可扩展平台。|  
  
> [!IMPORTANT]  
>  1.  安装程序不为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 扩展部署中的多个节点配置负载平衡和单 URL 寻址。 若要完成扩展部署，必须使用 Windows Server、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Application Center 或第三方群集管理软件。 有关设置 Web 场部署的详细信息，请参阅[为横向扩展部署配置 Reporting Services](http://go.microsoft.com/fwlink/?LinkId=199448) (http://go.microsoft.com/fwlink/?LinkId=199448)。  
> 2.  有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件的浏览器要求，请参阅 [规划 Reporting Services 和 Power View 浏览器支持 (Reporting Services 2014)](../../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)。  
> 3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不支持同时在 64 位平台上和 64 位服务器的 32 位子系统 (WOW64) 上进行并行配置。  
  
### <a name="shared-features"></a>共享功能  
 由一台计算机上的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例共享的功能安装在一个目录中。 其中包括：  
  
|功能|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -SharePoint|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式是一种基于服务器的应用程序，用于创建、管理报表并将报表传递到电子邮件、多种文件格式和基于 Web 的交互格式。 SharePoint 模式将报表查看和报表管理体验与 SharePoint 产品集成在一起。 有关详细信息，请参阅 [Reporting Services 报表服务器（SharePoint 模式）](../../../2014/reporting-services/reporting-services-report-server-sharepoint-mode.md)。|  
|用于 SharePoint 产品的[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Add-in for SharePoint Products|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 用于 SharePoint 产品包括管理和用户界面组件，以便将 SharePoint 产品与外接[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在 SharePoint 模式下的报表服务器。 有关详细信息，请参阅[在何处查找用于 SharePoint 产品的 Reporting Services 外接程序](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。|  
|数据质量客户端|Data Quality Client 是一个独立的应用程序，它连接到 DQS 服务器，并提供一个直观的图形用户界面来执行数据清除和数据匹配操作，以及在 DQS 中执行管理任务。|  
|客户端工具连接|客户端工具包括用于在客户端和服务器之间进行通信的组件，其中包括用于 DB-Library、OLEDB for OLAP、ODBC、ADODB 和 ADOMD+ 的各种网络库。|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 是一组图形工具和可编程对象，用于移动、复制和转换数据。|  
|客户端工具向后兼容性|客户端工具向后兼容性包括以下组件：<br /><br /> SQL 分布式管理对象 (SQL-DMO)。 有关详细信息，请参阅 [SQL Server 2014 中不再使用的 SQL Server 功能](../../../2014/getting-started/discontinued-sql-server-features-in-sql-server-2014.md)。<br /><br /> 决策支持对象 (DSO)。 有关详细信息，请参阅 [SQL Server 2014 中 Analysis Services 功能的重大更改](../../../2014/analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2014.md)。|  
|客户端工具 SDK|包括包含针对程序员的资源的软件开发包。|  
|文档组件|文档组件包括用于查看和管理帮助内容的组件。|  
|管理工具 - 基本|**管理工具 - 基本：** 它包含以下项：<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 为支持[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]， [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]， **sqlcmd**实用程序，和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]PowerShell 提供程序<br /><br /> **管理工具 - 完整：** 除基本版本中的组件以外，完整版还包括以下组件：<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 对于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的支持<br /><br /> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]<br /><br /> Database Engine Tuning Advisor<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具管理|  
|Distributed Replay 控制器|Distributed Replay 控制器协调分布式的重播客户端的操作。 在每个 Distributed Replay 环境中只能有一个控制器实例。 有关详细信息，请参阅 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)。|  
|Distributed Replay 客户端|多个 Distributed Replay 客户端一起来模拟 SQL Server 实例的工作负荷。 在每个 Distributed Replay 环境中可以有一个或多个客户端。 有关详细信息，请参阅 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)。|  
|SQL 客户端连接 SDK|为数据库应用程序开发包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (ODBC/OLE DB) SDK。|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 是一个平台，用于将整个组织内不同系统中的数据集成到单一主数据源，以确保准确性和进行审核。 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 选项安装 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]、程序集、Windows PowerShell 管理单元以及 Web 应用程序和服务的文件夹和文件。|  
  
 默认情况下，共享组件安装到 %Program Files%Microsoft SQL Server\\中。 若要更改安装路径，请单击 **“浏览”** 按钮。 如果更改一个共享组件的安装路径，则要同时更改其他共享组件的安装路径。 后续安装会将共享组件安装到与原始安装相同的位置。  
  
 **实例根目录**-默认情况下，实例根目录为 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\。 若要指定非默认的根目录，请单击“浏览”按钮或提供一个路径名。  
  
 在基于 x64 的操作系统上，您可以指定 64 位组件的安装位置，以及 32 位组件在 WOW64 子系统上的安装位置。  
  
## <a name="disk-space-requirements"></a>磁盘空间要求  
 使用“磁盘成本摘要”页可以检查选择安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的磁盘空间要求。  
  
### <a name="options"></a>选项  
 如果所需的磁盘空间太大，应考虑以下选项：  
  
-   将安装目录更改为具有更多磁盘空间的驱动器。  
  
-   更改要安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。  
  
-   通过移动其他文件或应用程序在指定驱动器上腾出更多可用空间。  
  
## <a name="installing-adventureworks-sample-databases"></a>安装 AdventureWorks 示例数据库  
 默认情况下，不会将示例数据库和示例代码作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的一部分进行安装。 有关安装示例数据库和示例代码的详细信息，请参阅[Microsoft SQL Server 社区项目和示例](http://go.microsoft.com/fwlink/?LinkId=87843)(http://go.microsoft.com/fwlink/?LinkId=87843)。  
  
 安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后还可以获得有关示例的其他信息。 从**启动**菜单上，单击**所有程序**，单击**[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**，单击**文档和教程**然后单击 **[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]示例概述**。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 的版本和组件](../editions-and-components-of-sql-server-2016.md)  
  
  
