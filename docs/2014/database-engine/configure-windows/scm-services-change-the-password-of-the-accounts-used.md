---
title: 更改 SQL Server （SQL Server 配置管理器）所使用的帐户的密码 |Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- expired password [SQL Server], SQL Server Agent
- passwords [SQL Server], SQL Server Agent service
- passwords [SQL Server], changing
- expired password [SQL Server], Database Engine
- passwords [SQL Server], SQL Server service
- Database Engine [SQL Server], passwords
- changing passwords used by SQL Server
- modifying passwords
ms.assetid: 5b6dcc03-6cae-45d3-acef-6f85ca6d615f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1454e29835c0087fb75c93a1680f452dfe0f2c05
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935078"
---
# <a name="change-the-password-of-the-accounts-used-by-sql-server-sql-server-configuration-manager"></a>更改 SQL Server 使用的帐户的密码（SQL Server 配置管理器）
  本主题说明如何使用 SQL Server 配置管理器在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 代理使用的帐户的密码。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作为服务在计算机上运行，并使用最初在设置期间提供的凭据。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例使用域帐户运行但此帐户的密码已更改，则必须将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所用的密码更新为新密码。 如果不更新密码， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能无法访问某些域资源；如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 停止，则在更新密码后才能重新启动该服务。  
  
 若要更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证密码，请参阅 [密码已过期](../password-expired.md)。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是为更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务设置而设计和授权使用的工具。 使用 Windows 服务控制管理器 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] services.msc **) 应用程序更改**服务不总是更改所有必要设置，并且可能会阻止服务正常运行。 但是在群集环境中，在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器更改活动节点上的密码之后，您必须使用服务控制管理器来更改被动节点上的密码。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 您必须是计算机管理员才能更改服务所用的密码。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### <a name="to-change-the-password-used-by-the-sql-server-database-engine-service"></a>更改 SQL Server（数据库引擎）服务所用的密码  
  
1.  单击 **“开始”** 按钮，依次指向 **“所有程序”** 、“ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]”和 **“配置工具”** ，然后单击 **“SQL Server 配置管理器”** 。  
  
    > [!NOTE]  
    >  因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台程序的一个管理单元而不是单独的程序，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器在新版本的 Windows 中不显示为一个应用程序。  
    >   
    >  -   **Windows 10**：  
    >          若要打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager，请在 "**开始" 页**上键入 sqlservermanager12.msc （对于 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ）。 对于早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请将 12 替换为较小的数字。 单击 SQLServerManager12.msc 可打开“配置管理器”。 若要将 Configuration Manager 固定到 "起始页" 或 "任务栏"，请右键单击 "Sqlservermanager12.msc"，然后单击 "**打开文件位置**"。 在 Windows 文件资源管理器中，右键单击 "Sqlservermanager12.msc"，然后单击 "**固定到****任务栏**"。  
    > -   **Windows 8**：  
    >          若要打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager，请在 "**搜索**" 超级按钮中的 "**应用**" 下，键入**sqlservermanager version>.msc （ \<version> **如 `SQLServerManager12.msc` ），然后按**enter**。  
  
2.  在 SQL Server 配置管理器中，单击 **“SQL Server 服务”** 。  
  
3.  在详细信息窗格中，右键单击**SQL Server （** \<instancename> **）**，然后单击 "**属性**"。  
  
4.  在 " **SQL Server （** \<instancename> **）属性**" 对话框的 "登录" 选项卡上，对于 "**帐户名**" 框中列出的帐户，在 "**密码**" 和 "**确认密码**" 框中键入新密码，然后单击 **"确定"**。  
  
     密码会立即生效，而不需要重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
#### <a name="to-change-the-password-used-by-the-sql-server-agent-service"></a>更改 SQL Server 代理服务所用的密码  
  
1.  单击 **“开始”** 按钮，依次指向 **“所有程序”** 、“ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]”和 **“配置工具”** ，然后单击 **“SQL Server 配置管理器”** 。  
  
2.  在 SQL Server 配置管理器中，单击 **“SQL Server 服务”** 。  
  
3.  在详细信息窗格中，右键单击**SQL Server 代理（** \<instancename> **）**，然后单击 "**属性**"。  
  
4.  在 " **SQL Server 代理（** \<instancename> **）属性**" 对话框的 "登录" 选项卡上，对于 "**帐户名**" 框中列出的帐户，在 "**密码**" 和 "**确认密码**" 框中键入新密码，然后单击 **"确定"**。  
  
     在独立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上，密码会立即生效，无需重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在群集实例上， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源脱机，并需要重新启动。  
  
## <a name="see-also"></a>另请参阅  
 [管理服务操作指南主题（SQL Server 配置管理器）](../managing-services-how-to-topics-sql-server-configuration-manager.md)  
  
  
