---
title: SQL Server 2014 中的废止 SQL Server 功能 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 0678bfbc-5d3f-44f4-89c0-13e8e52404da
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8f7ab6cdbc1b6e0e3dc7d26fb579943a0c8fa95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73637771"
---
# <a name="discontinued-sql-server-features-in-sql-server-2014"></a>SQL Server 2014 中不再推荐使用的 SQL Server 功能
  本主题介绍升级到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 后不再可用的功能。  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a>
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]
  
 
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中没有停止使用的功能。  
  
## <a name="discontinued-features-in-includesssql11includessssql11-mdmd"></a>
  [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]
  
  
### <a name="discontinued-active-directory-helper-service"></a>停止使用的 Active Directory Helper 服务  
 Active Directory Helper 服务和相关组件已删除。 下表列出了已删除的关联组件：  
  
|类别|废弃的功能|替代功能|  
|--------------|--------------------------|-----------------|  
|系统存储过程|sp_ActiveDirectory_Obj<br /><br /> sp_ActiveDirectory_SCP<br /><br /> sp_ActiveDirectory_Start|没有可以替换的表|  
  
## <a name="discontinued-features-in-sql-server-2008-r2"></a>SQL Server 2008 R2 中停止使用的功能  
  
### <a name="64-bit-platform-support-in-reporting-services"></a>Reporting Services 中的 64 位平台支持  
 从 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 开始，[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 组件不再支持运行 Windows Server 2003 或 Windows Server 2003 R2 的基于 Itanium 的服务器。 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 继续支持其他 64 位操作系统，包括 Windows Server 2008 for Itanium-Based Systems 和 Windows Server 2008 R2 for Itanium-Based Systems。 若要在 Windows Server 2003 或 Windows Server 2003 R2 的基于 Itanium 的系统版本上从具有 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 安装升级到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，您必须首先升级操作系统。  
  
## <a name="discontinued-features-in-sql-server-2008"></a>SQL Server 2008 中已不再使用的功能  
  
### <a name="discontinued-sql-dmo-from-sql-server-express-installation"></a>SQL Server Express 安装中已不再使用的 SQL-DMO  
 用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 SQL-DMO 已从 [!INCLUDE[ssExpressEd10](../includes/ssexpressed10-md.md)] 中删除。 我们建议您尽快修改当前使用此功能的应用程序。 如果必须支持针对[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] EXPRESS 的 sql-dmo，请从[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=24793)安装功能包的向后兼容组件。 请使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理对象 (SMO) 进行新的开发工作。  
  
### <a name="discontinued-option-for-web-assistant"></a>已不再使用的用于 Web 助手的选项  
 用于启用 Web 助手的 `sp_configure` 选项已从 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中删除。 建议改用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 。  
  
### <a name="surface-area-configuration-tool"></a>外围应用配置工具  
 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中已不再推荐使用外围应用配置器工具。 下表显示了此版本中可用于配置设置、选项和组件功能的工具。  
  
|替换设置和组件功能|如何配置|  
|-------------------------------------------------|----------------------|  
|协议、连接和启动选项|使用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager。|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)]功能|使用基于策略的管理、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的属性设置或 sp_Configure。|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]功能|使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的属性设置。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] - EnableIntegrated Security 属性|使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的属性设置。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -“预定事件和报表传递”以及“Web 服务和 HTTP 访问”|编辑 RSReportServer.config 配置文件。|  
|命令行选项|在此版本中不支持。|  
|SOAP 和 [!INCLUDE[ssSB](../includes/sssb-md.md)] 端点|使用[CREATE endpoint](/sql/t-sql/statements/create-endpoint-transact-sql)和[ALTER endpoint](/sql/t-sql/statements/alter-endpoint-transact-sql)。|  
  
### <a name="discontinued-command-prompt-parameters-for-sql-server-setup"></a>已不再使用的 SQL Server 安装程序命令提示符参数  
 下表显示的是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中不再支持的早期版本 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中的安装程序命令提示符参数。  
  
|已不再推荐使用的参数|替代参数|  
|----------------------------|---------------------------|  
|ADDLOCAL|/ACTION=Uninstall 和 /FEATURES|  
|DISABLENETWORKPROTOCOLS|TCP/IP<sup>1</sup>的/TCPENABLED|  
|DISABLENETWORKPROTOCOLS|Named Pipes<sup>1</sup>的/NPENABLED|  
|INSTALLSQLDATADIR|/SQLUSERDBDIR<br /><br /> /SQLUSERDBLOGDIR<br /><br /> /SQLBACKUPDIR<br /><br /> /SQLTEMPDBDIR<br /><br /> /SQLTEMPDBLOGDIR|  
|REINSTALL|在此版本中无等效参数。|  
|REINSTALLMODE|在此版本中无等效参数。|  
|REMOVE|/ACTION=Uninstall 和 /FEATURES|  
|SAMPLEDATABASE|在此版本中无等效参数。|  
|SAVESYSDB|在此版本中无等效参数。|  
|SKUUPGRADE<sup>2</sup>|在此版本中无等效参数。|  
|UPGRADE|/ACTION=Upgrade 和 /FEATURES|  
|USESYSDB|在此版本中无等效参数。|  
  
 <sup>1</sup>这些参数仅对安装有效。  
  
 <sup>2</sup>开始[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]时，指定/Action = EditionUpgrade，以随时将现有版本[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的升级到其他版本，而无需使用原始安装媒体。 有关支持的版本升级的详细信息，请参阅 [Supported Version and Edition Upgrades](../database-engine/install-windows/supported-version-and-edition-upgrades.md)。  
  
 有关详细信息，请参阅 [从命令提示符安装 SQL Server 2014](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
  
