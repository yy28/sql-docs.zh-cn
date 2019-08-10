---
title: 安装 SQL Server 2014 |Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ed522c64e0f9652e3ffb310f98348c402193ef8
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889244"
---
# <a name="install-sql-server-2014"></a>安装 SQL Server 2014
## <a name="download-sql-server-2014-expresshttpwwwhanselmancomblogdownloadsqlserverexpressaspx"></a>[下载 SQL Server 2014 Express](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **感谢您在一个位置收集所有安装程序包链接的[Hanselman](http://www.hanselman.com/) 。**
  
 本主题概要介绍用于安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的不同安装选项。 有关可安装的各种[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]组件以及安装过程的详细信息, 请参阅[SQL Server 2014 的安装](installation-for-sql-server.md)。  
> **注意:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在32位和64位版本中可用。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 32 位和 64 位版本可通过安装向导或命令提示符进行安装。 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]组件的详细信息, 请参阅[SQL Server 2014 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)和[SQL Server 2014 各个版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 默认情况下，不会将示例数据库和示例代码作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的一部分进行安装。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Edition 以外的其他 SQL Server 版本，若要安装示例数据库和示例代码，请参阅 [CodePlex 网站](https://go.microsoft.com/fwlink/?LinkId=87843)。 若要了解对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]示例数据库和示例代码的支持，请参阅 [数据库和示例概述](https://go.microsoft.com/fwlink/?LinkId=110391)。  
  
 在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]前，请查看安装要求、系统配置检查和安全注意事项。 有关详细信息，请参阅 [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md)。 有关针对 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的不同安装方案的信息，请参阅下一节中的主题。  
  
  
## <a name="install-includesscurrentincludessscurrent-mdmd-components"></a>安装[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]组件  
  
|主题|描述|  
|-----------|-----------------|  
|[关于 SQL Server 数据库引擎](../sql-server-database-engine-overview.md)|说明如何安装和配置 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。|  
|[安装 SQL Server 复制](install-sql-server-replication.md)|说明如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制。|  
|[安装 Distributed Replay](../../tools/distributed-replay/install-distributed-replay-overview.md)|列出了有关安装 Distributed Replay 功能的主题。|  
|[安装 SQL Server 管理工具](../../sql-server/install/install-sql-server-management-tools.md)|说明如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具。|  
|[安装 SQL Server PowerShell](install-sql-server-powershell.md)|介绍安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 组件的注意事项。|  
  
## <a name="how-to-install-includesscurrentincludessscurrent-mdmd"></a>如何安装[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
|标题|描述|  
|-----------|-----------------|  
|[安装操作指南主题](../../sql-server/install/installation-how-to-topics.md)|提供 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的各种安装方法的过程主题链接，这些方法包括使用安装向导、命令提示符、配置文件或 SysPrep。|  
|[在 Server Core 上安装 SQL Server 2014](install-sql-server-on-server-core.md)|查看该主题可了解如何在 Windows Server Core 上安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。|  
|[验证 SQL Server 安装](validate-a-sql-server-installation.md)|查看 SQL 发现报告的用法，以便确认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本以及在计算机上安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。|  
|[系统配置检查器的检查参数](check-parameters-for-the-system-configuration-checker.md)|讨论系统配置检查器 (SCC) 的功能。|  
  
## <a name="configuration"></a>配置  
  
|主题|描述|  
|-----------|-----------------|  
|[配置 Windows 防火墙以允许 SQL Server 访问](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|本主题概述了防火墙配置和 Windows 防火墙配置方法。|  
|[将多宿主计算机配置为允许 SQL Server 访问](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|本主题介绍如何在多宿主环境中对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和高级安全 Windows 防火墙进行配置，以便为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例提供多个网络连接。|  
|[配置 Windows 防火墙以允许 Analysis Services 访问](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|可以按照本主题中提供的步骤配置端口和防火墙设置，以允许对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 PowerPivot for SharePoint 进行访问。|  
  
## <a name="related-sections"></a>相关章节  
 [安装 SQL Server 2014 BI 功能](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BI 平台的一部分的功能包括 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 功能包括：[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]，以及用于创建或使用分析数据的若干客户端应用程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装文档中的本节说明如何安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
 [SQL Server 故障转移群集安装](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装文档中的本节介绍了如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集。  
  
## <a name="see-also"></a>请参阅  
 [计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)   
 [升级到 SQL Server 2014](upgrade-sql-server.md)   
 [卸载 SQL Server 2014](../../sql-server/install/uninstall-sql-server.md)   
 [高可用性解决方案 (SQL Server)](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
