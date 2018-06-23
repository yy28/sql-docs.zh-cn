---
title: SQL Server 2014 的版本和组件 |Microsoft 文档
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- 32-bit vs. 64-bit editions [SQL Server]
- default components
- Workgroup Edition [SQL Server]
- Internet servers [SQL Server]
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- client/server applications [SQL Server]
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- 64-bit edition [SQL Server]
- IIS [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: e5186f02-dd91-47d0-8fa4-de3f41c76903
caps.latest.revision: 111
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 450c54feb6d8e360ca812524778762751318aab7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025372"
---
# <a name="editions-and-components-of-sql-server-2014"></a>SQL Server 2014 的版本和组件
  根据应用程序的需要，安装要求会有所不同。 不同版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 能够满足单位和个人独特的性能、运行时以及价格要求。 安装哪些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件还取决于您的具体需要。 下面各节将帮助您了解如何在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的不同版本和可用组件中做出最佳选择。  
  
## <a name="principal-editions-of-includesscurrentincludessscurrent-mdmd"></a>主要版本 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 下表介绍 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的主要版本。 有关详细信息，请参阅[支持的 SQL Server 2014 的版本功能](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|定义|  
|---------------------------------------|----------------|  
|Enterprise（64 位和 32 位）|作为高级版本， [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise 版提供了全面的高端数据中心功能，性能极为快捷、虚拟化不受限制，还具有端到端的商业智能 - 可为关键任务工作负荷提供较高服务级别，支持最终用户访问深层数据。|  
|Business Intelligence（64 位和 32 位）|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Business Intelligence 版提供了综合性平台，可支持组织构建和部署安全、可扩展且易于管理的 BI 解决方案。 它提供令人兴奋的功能，如数据浏览和可视化效果; 基于浏览器功能强大的数据聚合型功能和增强的集成管理。|  
|Standard（64 位和 32 位）|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Standard 版提供了基本数据管理和商业智能数据库，使部门和小型组织能够顺利运行其应用程序并支持将常用开发工具用于内部部署和云部署 - 有助于以最少的 IT 资源获得高效的数据库管理。|  
  
## <a name="specialized-editions-of-includesscurrentincludessscurrent-mdmd"></a>专业的版本 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 专业化版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 面向不同的业务工作负荷。 下表介绍 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的专业化版本。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Description|  
|---------------------------------------|-----------------|  
|Web（64 位和 32 位）|对于为从小规模至大规模 Web 资产提供可伸缩性、经济性和可管理性功能的 Web 宿主和 Web VAP 来说，[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Web 版本是一项总拥有成本较低的选择。|  
  
## <a name="breadth-editions-of-includesscurrentincludessscurrent-mdmd"></a>延伸版本 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 延伸版是针对特定的用户应用而设计的，可免费获取或只需支付极少的费用。 下表介绍 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的延伸版本。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Description|  
|---------------------------------------|-----------------|  
|Developer（64 位和 32 位）|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Developer 版支持开发人员基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]构建任意类型的应用程序。 它包括 Enterprise 版的所有功能，但有许可限制，只能用作开发和测试系统，而不能用作生产服务器。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer 是构建和测试应用程序的人员的理想之选。|  
|Express 版（64 位和 32 位）|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Express 是入门级的免费数据库，是学习和构建桌面及小型服务器数据驱动应用程序的理想选择。 它是独立软件供应商、开发人员和热衷于构建客户端应用程序的人员的最佳选择。 如果您需要使用更高级的数据库功能，则可以将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 无缝升级到其他更高端的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB 是 Express 的一种轻型版本，该版本具备所有可编程性功能，但在用户模式下运行，并且具有快速的零配置安装和必备组件要求较少的特点。|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-an-internet-server"></a>将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用于 Internet 服务器  
 在 Internet 服务器（如运行 Internet Information Services (IIS) 的服务器）上通常都会安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 客户端工具。 客户端工具包括连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的应用程序所使用的客户端连接组件。  
  
> [!NOTE]  
>  尽管可以在运行 IIS 的计算机上安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，但这种做法通常只用于仅包含一台服务器的小型网站。 大多数网站都将其中间层 IIS 系统安装在一台服务器上或服务器群集中，将数据库安装在另外一个服务器或服务器联合体上。  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用于客户端/服务器应用程序  
 在运行直接连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的客户端/服务器应用程序的计算机上，只能安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]客户端组件。 如果要在数据库服务器上管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，或者打算开发 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 应用程序，那么客户端组件安装也是一个不错的选择。  
  
 客户端工具选项安装以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能：向后兼容性组件、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]、连接组件、管理工具、软件开发包和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书组件。 有关详细信息，请参阅[从安装向导安装 SQL Server 2014&#40;安装&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。  
  
## <a name="deciding-among-includessnoversionincludesssnoversion-mdmd-components"></a>选择 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件  
 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装向导的“功能选择”页面选择安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]时要安装的组件。 默认情况下未选中树中的任何功能。  
  
 可根据下表中给出的信息确定最能满足需要的功能集合。  
  
|服务器组件|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 包括[!INCLUDE[ssDE](../includes/ssde-md.md)]（用于存储、处理和保护数据安全的核心服务）、复制、全文搜索、用于管理关系数据和 XML 数据的工具以及 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 服务器。|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 包括一些工具，可用于创建和管理联机分析处理 (OLAP) 以及数据挖掘应用程序。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 包括用于创建、管理和部署表格报表、矩阵报表、图形报表以及自由格式报表的服务器和客户端组件。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 还是一个可用于开发报表应用程序的可扩展平台。|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是一组图形工具和可编程对象，用于移动、复制和转换数据。 它还包括 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)](DQS) 组件。|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) 是针对主数据管理的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 解决方案。 可以配置 MDS 来管理任何领域（产品、客户、帐户）；MDS 中可包括层次结构、各种级别的安全性、事务、数据版本控制和业务规则，以及可用于管理数据的 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 。|  
  
|管理工具|Description|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 是用于访问、配置、管理和开发 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]组件的集成环境。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 使各种技术水平的开发人员和管理员都能使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务、服务器协议、客户端协议和客户端别名提供基本配置管理。|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 提供了一个图形用户界面，用于监视 [!INCLUDE[ssDE](../includes/ssde-md.md)] 实例或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例。|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] 优化顾问|[!INCLUDE[ssDE](../includes/ssde-md.md)] 优化顾问可以协助创建索引、索引视图和分区的最佳组合。|  
|数据质量客户端|提供了一个非常简单和直观的图形用户界面，用于连接到 DQS 数据库并执行数据清理操作。 它还允许您集中监视在数据清理操作过程中执行的各项活动。|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 提供 IDE 以便为以下商业智能组件生成解决方案： [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]。<br /><br /> （以前称作 Business Intelligence Development Studio）。<br /><br /> [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 还包含“数据库项目”，为数据库开发人员提供集成环境，以便在 Visual Studio 内为任何 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 平台（包括本地和外部）执行其所有数据库设计工作。 数据库开发人员可以使用 Visual Studio 中功能增强的服务器资源管理器，轻松创建或编辑数据库对象和数据或执行查询。|  
|连接组件|安装用于客户端和服务器之间通信的组件，以及用于 DB-Library、ODBC 和 OLE DB 的网络库。|  
  
|文档|Description|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的核心文档。|  
  
## <a name="see-also"></a>请参阅  
 [计划 SQL Server 安装](install/planning-a-sql-server-installation.md)   
 [从安装向导安装 SQL Server 2014&#40;安装程序&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
  