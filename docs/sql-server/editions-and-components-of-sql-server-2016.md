---
title: "SQL Server 2016 的版本和组件 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Enterprise Edition [SQL Server]"
  - "Developer Edition [SQL Server]"
  - "32 位与64 位版本 [SQL Server]"
  - "默认组件"
  - "Workgroup Edition [SQL Server]"
  - "Internet 服务器 [SQL Server]"
  - "安装 SQL Server, 组件"
  - "安装程序 [SQL Server], 组件"
  - "SQL Server, 版本"
  - "SQL Server, 组件"
  - "客户端/服务器应用程序 [SQL Server]"
  - "版本 [SQL Server]"
  - "版本 [SQL Server]"
  - "安装程序 [SQL Server], 版本"
  - "SQL Server 安装向导"
  - "组件 [SQL Server]"
  - "Standard Edition [SQL Server]"
  - "64 位版本 [SQL Server]"
  - "IIS [SQL Server]"
  - "安装 SQL Server, 版本"
  - "版本 [SQL Server], 关于版本选项"
  - "安装程序 [SQL Server]"
ms.assetid: e5186f02-dd91-47d0-8fa4-de3f41c76903
caps.latest.revision: 121
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 121
---
# SQL Server 2016 的版本和组件
> 若要深入了解 SQL Server 2016 各版本支持的功能，请参阅 [SQL Server 2016 的各版本和支持的功能](../sql-server/sql-server-2016-的各版本和支持的功能.md)。

  根据应用程序的需要，安装要求会有所不同。 不同版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 能够满足单位和个人独特的性能、运行时以及价格要求。 安装哪些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件还取决于您的具体需要。 下面各节将帮助您了解如何在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的不同版本和可用组件中做出最佳选择。  
  
## <a name="includesscurrenttokensscurrentmdmd-editions"></a>[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本  
 下表介绍 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的各个版本。 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|定义|  
|---------------------------------------|----------------|  
|Enterprise|作为高级版本，[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise 版提供了全面的高端数据中心功能，性能极为快捷、虚拟化不受限制，还具有端到端的商业智能 - 可为关键任务工作负荷提供较高服务级别，支持最终用户访问深层数据。|  
|Standard|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Standard 版提供了基本数据管理和商业智能数据库，使部门和小型组织能够顺利运行其应用程序并支持将常用开发工具用于内部部署和云部署 - 有助于以最少的 IT 资源获得高效的数据库管理。|  
|Web|对于为从小规模至大规模 Web 资产提供可伸缩性、经济性和可管理性功能的 Web 宿主和 Web VAP 来说，[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Web 版本是一项总拥有成本较低的选择。|  
|开发人员|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Developer 版支持开发人员基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 构建任意类型的应用程序。 它包括 Enterprise 版的所有功能，但有许可限制，只能用作开发和测试系统，而不能用作生产服务器。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer 是构建 <br />                [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 和测试应用程序的人员的理想之选。|  
|Express 版本|Express 版本是入门级的免费数据库，是学习和构建桌面及小型服务器数据驱动应用程序的理想选择。 它是独立软件供应商、开发人员和热衷于构建客户端应用程序的人员的最佳选择。 如果您需要使用更高级的数据库功能，则可以将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 无缝升级到其他更高端的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB 是 Express 的一种轻型版本，该版本具备所有可编程性功能，但在用户模式下运行，并且具有快速的零配置安装和必备组件要求较少的特点。|  
  
## <a name="using-includessnoversiontokenssnoversionmdmd-with-an-internet-server"></a>将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用于 Internet 服务器  
 在 Internet 服务器（如运行 Internet Information Services (IIS) 的服务器）上通常都会安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 客户端工具。 客户端工具包括连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的应用程序所使用的客户端连接组件。  
  
> **注意：**尽管可以在运行 IIS 的计算机上安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，但这种做法通常只用于仅包含一台服务器的小型网站。 大多数网站都将其中间层 IIS 系统安装在一台服务器上或服务器群集中，将数据库安装在另外一个服务器或服务器联合体上。  
  
## <a name="using-includessnoversiontokenssnoversionmdmd-with-clientserver-applications"></a>将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用于客户端/服务器应用程序  
 在运行直接连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的客户端/服务器应用程序的计算机上，只能安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 客户端组件。 如果要在数据库服务器上管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，或者打算开发 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 应用程序，那么客户端组件安装也是一个不错的选择。  
  
 客户端工具选项安装以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能：向后兼容性组件、[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]、连接组件、管理工具、软件开发包和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书组件。 有关详细信息，请参阅[安装 SQL Server 2016](../database-engine/install-windows/install-sql-server-2016.md)。  
  
## <a name="deciding-among-includessnoversiontokenssnoversionmdmd-components"></a>选择 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件  
 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装向导的“功能选择”页面选择安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 时要安装的组件。 默认情况下未选中树中的任何功能。  
  
 可根据下表中给出的信息确定最能满足需要的功能集合。  
  
|服务器组件|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 包括 [!INCLUDE[ssDE](../includes/ssde-md.md)]、部分工具和 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 服务器，其中引擎是用于存储、处理和保护数据、复制及全文搜索的核心服务，工具用于管理数据库分析集成中和可访问 Hadoop 及其他异类数据源的 Polybase 集成中的关系数据和 XML 数据。|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 包括一些工具，可用于创建和管理联机分析处理 (OLAP) 以及数据挖掘应用程序。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 包括用于创建、管理和部署表格报表、矩阵报表、图形报表以及自由格式报表的服务器和客户端组件。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 还是一个可用于开发报表应用程序的可扩展平台。|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是一组图形工具和可编程对象，用于移动、复制和转换数据。 它还包括 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (DQS) 组件。|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) 是针对主数据管理的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 解决方案。 可以配置 MDS 来管理任何领域（产品、客户、帐户）；MDS 中可包括层次结构、各种级别的安全性、事务、数据版本控制和业务规则，以及可用于管理数据的 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]。|  
|[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]|[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] 支持在多个平台上使用可缩放的分布式 R 解决方案，并支持使用多个企业数据源（如 Linux、Hadoop 和 Teradata 等）。|  
  
|管理工具|Description|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 是用于访问、配置、管理和开发 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件的集成环境。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 使各种技术水平的开发人员和管理员都能使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。<br /><br /> 从 <br />                [下载 SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx) 中下载并安装 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务、服务器协议、客户端协议和客户端别名提供基本配置管理。|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 提供了一个图形用户界面，用于监视[!INCLUDE[ssDE](../includes/ssde-md.md)]实例或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例。|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] 优化顾问|[!INCLUDE[ssDE](../includes/ssde-md.md)]优化顾问可以协助创建索引、索引视图和分区的最佳组合。|  
|数据质量客户端|提供了一个非常简单和直观的图形用户界面，用于连接到 DQS 数据库并执行数据清理操作。 它还允许您集中监视在数据清理操作过程中执行的各项活动。|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 提供 IDE 以便为以下商业智能组件生成解决方案：[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]。<br /><br /> （以前称作 Business Intelligence Development Studio）。<br /><br /> [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 还包含“数据库项目”，为数据库开发人员提供集成环境，以便在 Visual Studio 内为任何 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 平台（包括本地和外部）执行其所有数据库设计工作。 数据库开发人员可以使用 Visual Studio 中功能增强的服务器资源管理器，轻松创建或编辑数据库对象和数据或执行查询。|  
|连接组件|安装用于客户端和服务器之间通信的组件，以及用于 DB-Library、ODBC 和 OLE DB 的网络库。|  
  
|文档|Description|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的核心文档。|  
  
  