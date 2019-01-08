---
title: 管理数据库引擎服务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, accessing
- Database Engine [SQL Server], services
- managing services [SQL Server], about service management
- services [SQL Server]
- SQL Server Agent service, managing
- SQL Server services, about SQL Server service
- MSSQLServer
- server configuration [SQL Server]
- managing services [SQL Server]
- SQL Server Agent service
- services [SQL Server], managing
- administering SQL Server, services
- SQL Server services
ms.assetid: aa732e43-53ba-4eea-bb9b-089da0766fc1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e747a85c816c8e57757be9acb61b14204266ff35
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "52639233"
---
# <a name="manage-the-database-engine-services"></a>管理数据库引擎服务
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作为服务运行在操作系统上。 服务是一种在系统后台运行的应用程序。 服务通常提供一些核心操作系统功能，例如 Web 服务、事件日志或文件服务。 运行的服务可以不在计算机桌面上显示用户界面。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理和一些其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件都作为服务运行。 这些服务通常会在操作系统启动时自动启动。 但是，也有些服务默认情况下不会自动启动，这取决于安装过程中如何进行指定。 本部分说明了如何管理各种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。 登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例之前，您需要了解如何启动、停止、暂停、恢复和重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 登录成功之后，就可以执行各种任务，如管理服务器或查询数据库。  
  
## <a name="using-the-sql-server-service"></a>使用 SQL Server 服务  
 启动 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例时即启动了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。 启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务之后，用户便可以与服务器建立新的连接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务可以在本地或远程作为服务来启动和停止。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务若是默认实例，则被称为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)；若是命名实例，则被称为 MSSQL$\<实例名>。  
  
## <a name="using-sql-server-configuration-manager"></a>使用 SQL Server 配置管理器  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器可以停止、启动、或暂停各种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器无法管理 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 服务。  
  
 您也可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器来查看所选服务的属性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是一个 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台 (MMC) 管理单元。 有关 MMC 和管理单元工作方式的详细信息，请参阅 Windows 帮助。  
  
 **访问 SQL Server 配置管理器**  
  
-   在 **“开始”** 菜单中，依次指向 **“所有程序”**、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **“配置工具”**，然后单击 **“SQL Server 配置管理器”**。  
  
 **使用 Windows 8 访问 SQL Server 配置管理器**  
  
 因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台程序的一个管理单元而不是单独的程序，所以，当运行 Windows 8.0 时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器不显示为一个应用程序。 若要打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，请在“搜索”超级按钮中的“应用”下，键入 **SQLServerManager12.msc**（对于 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]）、**SQLServerManager11.msc**（对于 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]）或 **SQLServerManager10.msc**（对于 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]），然后按 **Enter**。  
  
## <a name="in-this-section"></a>本节内容  
  
|||  
|-|-|  
|[管理服务的安全要求](security-requirements-for-managing-services.md)|[防止 SQL Server 实例自动启动（SQL Server 配置管理器）](scm-services-prevent-automatic-startup-of-an-instance.md)|  
|[配置 Windows 服务帐户和权限](configure-windows-service-accounts-and-permissions.md)|[为 SQL Server 更改服务启动帐户（SQL Server 配置管理器）](scm-services-change-the-service-startup-account.md)|  
|[在网络上或不在网络上运行 SQL Server](run-sql-server-with-or-without-a-network.md)|[配置服务器启动选项（SQL Server 配置管理器）](scm-services-configure-server-startup-options.md)|  
|[SQL Server Browser 服务（数据库引擎和 SSAS）](sql-server-browser-service-database-engine-and-ssas.md)|[更改 SQL Server 使用的帐户的密码（SQL Server 配置管理器）](scm-services-change-the-password-of-the-accounts-used.md)|  
|[数据库引擎服务启动选项](database-engine-service-startup-options.md)|[配置 SQL Server 错误日志](scm-services-configure-sql-server-error-logs.md)|  
|[启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务](start-stop-pause-resume-restart-sql-server-services.md)|[更改服务器身份验证模式](change-server-authentication-mode.md)|  
|[在单用户模式下启动 SQL Server](start-sql-server-in-single-user-mode.md)|[SQL 编写器服务](sql-writer-service.md)|  
|[以最小配置启动 SQL Server](start-sql-server-with-minimal-configuration.md)|[广播关闭消息（命令提示符）](broadcast-a-shutdown-message-command-prompt.md)|  
|[连接到其他计算机（SQL Server 配置管理器）](scm-services-connect-to-another-computer.md)|[登录到 SQL Server 实例（命令提示符）](log-in-to-an-instance-of-sql-server-command-prompt.md)|  
|[将 SQL Server 实例设置为自动启动（SQL Server 配置管理器）](scm-services-set-an-instance-to-start-automatically.md)|[配置数据库引擎访问的文件系统权限](configure-file-system-permissions-for-database-engine-access.md)|  
  
## <a name="related-content"></a>相关内容  
 [配置 SQL Server 代理](../../ssms/agent/sql-server-agent.md)  
  
 [登录到 SQL Server](logging-in-to-sql-server.md)  
  
  
