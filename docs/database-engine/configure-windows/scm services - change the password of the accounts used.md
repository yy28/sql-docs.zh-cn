---
title: "更改 SQL Server 使用的帐户的密码（SQL Server 配置管理器） | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "过期密码 [SQL Server], SQL Server 代理"
  - "密码 [SQL Server], SQL Server 代理服务"
  - "密码 [SQL Server], 更改"
  - "过期密码 [SQL Server], 数据库引擎"
  - "密码 [SQL Server], SQL Server 服务"
  - "数据库引擎 [SQL Server], 密码"
  - "更改 SQL Server 使用的密码"
  - "修改密码"
ms.assetid: 5b6dcc03-6cae-45d3-acef-6f85ca6d615f
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 更改 SQL Server 使用的帐户的密码（SQL Server 配置管理器）
  本主题说明如何使用 SQL Server 配置管理器在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 代理使用的帐户的密码。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作为服务在计算机上运行，并使用最初在设置期间提供的凭据。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例使用域帐户运行但此帐户的密码已更改，则必须将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所用的密码更新为新密码。 如果不更新密码， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能无法访问某些域资源；如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 停止，则在更新密码后才能重新启动该服务。  
  
 若要更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证密码，请参阅[密码已过期](../../ssms/f1-help/password-expired.md)。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是为更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务设置而设计和授权使用的工具。 使用 Windows 服务控制管理器 (**services.msc**) 应用程序更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务不总是更改所有必要设置，并且可能会阻止服务正常运行。 但是在群集环境中，在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器更改活动节点上的密码之后，您必须使用服务控制管理器来更改被动节点上的密码。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 您必须是计算机管理员才能更改服务所用的密码。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### 更改 SQL Server（数据库引擎）服务所用的密码  
  
1.  单击 **“开始”** 按钮，依次指向 **“所有程序”**、“ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]”和 **“配置工具”**，然后单击 **“SQL Server 配置管理器”**。  
  
    > [!NOTE]  
    >  因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台程序的一个管理单元而不是单独的程序，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器在新版本的 Windows 中不显示为一个应用程序。  
    >   
    >  -   **Windows 10**：  
    >          要打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，请在“起始页”中键入 SQLServerManager13.msc（适用于 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]）。 对于早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请将 13 替换为较小的数字。 单击“SQLServerManager13.msc”可打开配置管理器。 要将配置管理器固定到“起始页”或“任务栏”，请右键单击“SQLServerManager13.msc”，然后单击“打开文件位置”。 在“Windows 文件资源管理器”中，右键单击“SQLServerManager13.msc”，然后单击“固定到‘开始’屏幕”或“固定到任务栏”。  
    > -   **Windows 8**：  
    >          若要打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，请在“搜索”超级按钮中的“应用”下，键入 **SQLServerManager\<version>.msc**（例如 **SQLServerManager13.msc**），然后按“Enter”。  
  
2.  在 SQL Server 配置管理器中，单击 **“SQL Server 服务”**。  
  
3.  在细节窗格中，右键单击“SQL Server (\<instancename>)”****，然后单击“属性”。  
  
4.  在“SQL Server (\<instancename>) 属性”对话框中的“登录”选项卡上，对于“帐户名”框中列出的帐户，在“密码”框和“确认密码”框中键入新密码，然后单击“确定”。  
  
     密码会立即生效，而不需要重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
#### 更改 SQL Server 代理服务所用的密码  
  
1.  单击 **“开始”** 按钮，依次指向 **“所有程序”**、“ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]”和 **“配置工具”**，然后单击 **“SQL Server 配置管理器”**。  
  
2.  在 SQL Server 配置管理器中，单击 **“SQL Server 服务”**。  
  
3.  在详细信息窗格中，右键单击“SQL Server 代理 (\<instancename>)”，然后单击“属性”。  
  
4.  在“SQL Server 代理 (\<instancename>) 属性”对话框中的“登录”选项卡上，对于“帐户名”框中列出的帐户，在“密码”框和“确认密码”框中键入新密码，然后单击“确定”。  
  
     在独立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上，密码会立即生效，无需重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在群集实例上，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源脱机，并需要重新启动。  
  
## 另请参阅  
 [管理服务操作指南主题（SQL Server 配置管理器）](../Topic/Managing%20Services%20How-to%20Topics%20\(SQL%20Server%20Configuration%20Manager\).md)  
  
  