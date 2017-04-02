---
title: "MSSQL_ENG024070 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG024070 错误"
ms.assetid: 23ac7e00-fab6-429b-9f85-2736a322aa65
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG024070
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|24070|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|客户端没有所需的特权。|  
  
## 解释  
 这是一个常规错误，不管是否进行复制，都会引发该错误。 对于复制拓扑中的服务器，引发该错误的原因通常是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 服务控制管理器，而不是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 配置管理器来更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户。 当您在更改服务帐户后尝试运行代理作业时，作业可能会失败，并显示类似如下的错误消息：  
  
 "执行以用户身份︰ \< 用户帐户>。 复制-复制快照子系统︰ 代理 \< 代理名称> 失败。 执行以用户身份︰ \< 用户帐户>。 客户端没有所需的特权。 该步骤失败。 [SQLSTATE 42000]（错误 14151）。 该步骤失败。”  
  
 出现此问题的原因是 Windows 服务控制管理器无法向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的新服务帐户授予所需权限。  
  
## 用户操作  
 为了避免以后再出现此问题，请始终使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器而非 Windows 服务控制管理器来更改服务帐户和密码。  
  
 若要解决此问题，请使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器将服务帐户更改为原始帐户。 然后，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器更改为新帐户。 执行此操作时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器会将新帐户添加到以下安全组中：  
  
 SQLServer2008SQLAgentUser$ComputerName$InstanceName  
  
 成为此安全组的成员，便可以向新帐户授予运行复制代理作业所需的权限。  
  
## 另请参阅  
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [管理复制中的登录名和密码](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)  
  
  