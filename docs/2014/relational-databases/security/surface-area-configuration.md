---
title: 外围应用配置器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reducing attackable surface area
- upgrading SQL Server, security
- surface area configuration [SQL Server]
- surface area configuration [SQL Server], about surface area configuration
- attackable surface area [SQL Server]
- installing SQL Server, security
ms.assetid: f741169c-1453-4ad2-830b-bf2be27d712f
caps.latest.revision: 79
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8ed369dbd8cd63f7d1cb9e63adf0721fcb07e612
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2018
ms.locfileid: "40396433"
---
# <a name="surface-area-configuration"></a>外围应用配置器
  在新安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的默认配置中，许多功能并未启用。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只是有选择地安装和启动关键服务和功能，以最大限度地减少可能受到恶意用户攻击的功能数。 系统管理员可以在安装时更改这些设置，也可以有选择地启用或禁用运行中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的功能。 此外，如果从其他计算机进行连接，则在配置协议之前某些组件可能不可用。  
  
> [!NOTE]  
>  与新安装不同，升级期间不会关闭任何现有服务或功能；但在升级完成后可应用其他外围应用配置器选项。  
  
## <a name="protocols-connection-and-startup-options"></a>协议、连接和启动选项  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器可以启动和停止服务，配置启动选项，以及启用协议和其他连接选项。  
  
#### <a name="to-start-sql-server-configuration-manager"></a>启动 SQL Server 配置管理器  
  
1.  在 **“开始”** 菜单中，依次指向 **“所有程序”**、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **“配置工具”**，然后单击 **“SQL Server 配置管理器”**。  
  
    -   使用 **“SQL Server 服务”** 区域可以启动组件并配置自动启动选项。  
  
    -   使用“SQL Server 网络配置”区域可以启用连接协议和连接选项（如，TCP/IP 固定端口或强制加密）。  
  
 有关详细信息，请参阅 [SQL Server Configuration Manager](../sql-server-configuration-manager.md)。 此外，远程连接还取决于是否对防火墙进行了正确配置。 有关详细信息，请参阅 [配置 Windows 防火墙以允许 SQL Server 访问](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
## <a name="enabling-and-disabling-features"></a>启用和禁用功能  
 可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的方面来配置启用和禁用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]功能。  
  
#### <a name="to-configure-surface-area-using-facets"></a>使用方面配置外围应用  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的组件。  
  
2.  在对象资源管理器中，右键单击服务器，然后单击“方面”。  
  
3.  在“查看方面”对话框中，展开“方面”列表，然后选择相应的“外围应用配置器”方面（“外围应用配置器”、“Analysis Services 的外围应用配置器”或“Reporting Services 的外围应用配置器”）。  
  
4.  在 **“方面属性”** 区域，选择要用于每个属性的值。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 若要定期检查某个方面的配置，请使用基于策略的管理。 有关基于策略的管理的详细信息，请参阅 [使用基于策略的管理来管理服务器](../policy-based-management/administer-servers-by-using-policy-based-management.md)。  
  
 也可以使用 `sp_configure` 存储过程来设置[!INCLUDE[ssDE](../../includes/ssde-md.md)]选项。 有关详细信息，请参阅 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)版本的组合自动配置的最大工作线程数。  
  
 若要更改 **的** EnableIntegrated Security [!INCLUDE[ssRS](../../includes/ssrs.md)]属性，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的属性设置。 若要更改“预定事件和报表传递”  属性和“Web 服务和 HTTP 访问”  属性，请编辑 **RSReportServer.config** 配置文件。  
  
## <a name="command-prompt-options"></a>命令提示符选项  
 使用 **Invoke-PolicyEvaluation**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell cmdlet 可以调用外围应用配置器策略。 有关详细信息，请参阅 [使用数据库引擎 cmdlets](../../database-engine/use-the-database-engine-cmdlets.md)。  
  
## <a name="soap-and-service-broker-endpoints"></a>SOAP 和 Service Broker 端点  
 若要关闭端点，请使用基于策略的管理。 若要创建和更改端点的属性，可使用 [CREATE ENDPOINT (Transact-SQL)](/sql/t-sql/statements/create-endpoint-transact-sql) 和 [ALTER ENDPOINT (Transact-SQL)](/sql/t-sql/statements/alter-endpoint-transact-sql)。  
  
## <a name="related-content"></a>相关内容  
 [SQL Server 数据库引擎和 Azure SQL Database 的安全中心](security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
