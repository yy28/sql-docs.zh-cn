---
title: "“连接到 Master Data Services 数据库”对话框 | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.mds.configmanager.srvconnect.f1"
ms.assetid: b2f8c9b9-c31e-4f0d-9095-978709423190
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# “连接到 Master Data Services 数据库”对话框
  使用 **“连接到 Master Data Services 数据库”** 对话框可以选择 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。  
  
 在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中，可以从以下页面访问该对话框：  
  
-   在 **“数据库配置”** 页上，单击 **“选择数据库”** 。使用此对话框可以选择要为其配置系统设置的数据库。  
  
-   在 **“Web 配置”** 页上的 **“将应用程序与数据库相关联”**下，单击 **“选择”** 可以选择要与您的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 网站或应用程序相关联的数据库。  
  
## 选择数据库  
 指定用于连接到承载 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 数据库的本地或远程 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例的信息。 若要连接到某一远程实例，必须为远程连接启用该实例。  
  
|控件名称|Description|  
|------------------|-----------------|  
|**SQL Server 实例**|指定要承载 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 数据库的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例的名称。 该实例可以是本地或远程计算机上的默认实例或命名实例。 通过键入以下内容指定信息：<br /><br /> 键入一个句点 (.)，可以连接到本地计算机上的默认实例。<br /><br /> 键入服务器名或 IP 地址，可以连接到指定的本地或远程计算机上的默认实例。<br /><br /> 键入服务器名或 IP 地址以及实例名称，可以连接到指定的本地或远程计算机上的命名实例。 以 server_name\\instance_name 格式指定此信息。|  
|**身份验证类型**|选择在连接到指定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例时要使用的身份验证的类型。 用于连接的凭据确定在“Master Data Services 数据库”下拉列表中显示的数据库。<br /><br /> 身份验证类型包括：<br /><br /> **当前用户 - 集成安全性**：通过使用当前 Windows 用户帐户的凭据，使用集成 Windows 身份验证进行连接。 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 使用登录到计算机并打开了该应用程序的用户的 Windows 凭据。 您不能在应用程序中指定其他 Windows 凭据。 如果您想要使用其他 Windows 凭据进行连接，则必须作为该用户登录到计算机，然后打开 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。<br /><br /> **SQL Server 帐户**：使用 SQL Server 帐户进行连接。 在您选择此选项后， **“用户名”** 和 **“密码”** 字段将启用，并且您必须为指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 帐户指定凭据。|  
|**“用户名”**|指定将用于连接到指定的 SQL Server 实例的用户帐户的名称。 该帐户必须是指定的 **实例上** sysadmin [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 角色的成员：<br /><br /> “身份验证类型”为“当前用户 - 集成安全性”时，“用户名”框为只读，并且它显示登录到计算机的 Windows 用户帐户的名称。<br /><br /> 在 **“身份验证类型”** 为 **“SQL Server 帐户”**时， **“用户名”** 框将启用，并且您必须为指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 帐户指定凭据。|  
|**“密码”**|指定与用户帐户关联的密码：<br /><br /> “身份验证类型”为“当前用户 - 集成安全性”时，“密码”框为只读，并且使用指定 Windows 用户帐户的凭据进行连接。<br /><br /> 在 **“身份验证类型”** 为 **“SQL Server 帐户”**时， **“密码”** 框将启用，并且您必须指定与指定的用户帐户相关联的密码。|  
|**Connect**|使用指定的凭据连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例。|  
|**“主数据服务数据库”**|基于以下条件显示指定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库：<br /><br /> 当用户是此实例的 **sysadmin** 服务器角色的成员时，将显示此实例中的所有 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。<br /><br /> 当用户是此实例中任何 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库的 **db_owner** 数据库角色的成员时，将显示这些 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。<br /><br/> 有关 SQL Server 角色的详细信息，请参阅[服务器级别角色](../relational-databases/security/authentication-access/server-level-roles.md)和[数据库级别角色](../relational-databases/security/authentication-access/database-level-roles.md)。|  
  
## 另请参阅  
 [“数据库配置”页（Master Data Services 配置管理器）](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Master Data Services 入门 (SQL Server 2016)](../Topic/Get%20Started%20with%20Master%20Data%20Services%20\(SQL%20Server%202016\).md)  
  
  