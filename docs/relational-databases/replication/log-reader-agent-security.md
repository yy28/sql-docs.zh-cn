---
title: "日志读取器代理安全性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.security.LRA.f1"
helpviewer_keywords: 
  - "“日志读取器代理安全性”对话框"
ms.assetid: d6981e74-ddb8-41b8-9ea1-56c2ece63b8a
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 日志读取器代理安全性
  使用 **“日志读取器代理安全性”** 对话框可指定以下项：  
  
-   用于在分发服务器上运行日志读取器代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。 Windows 帐户也称为“进程帐户 ”，因为代理进程是在此帐户下运行。  
  
-   日志读取器代理与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器建立连接时所处的上下文。 通过模拟 Windows 帐户，或在指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户的上下文中可以进行连接。  
  
    > [!NOTE]  
    >  即使发布服务器与分发服务器在同一台计算机上，日志读取器代理也会与发布服务器建立连接。 日志读取器代理还可以与分发服务器建立连接；这些连接始终是通过模拟运行代理的 Windows 帐户来建立的。  
  
     对于 Oracle 发布服务器，指定日志读取器代理连接到发布服务器中的上下文 **发布服务器属性** 对话框 (可从 **分发服务器属性** 对话框)。 有关详细信息，请参阅 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 所有帐户必须是有效的，并且为每个帐户指定了正确的密码。 在运行代理之前不会对帐户和密码进行验证。  
  
## 选项  
 **进程帐户**  
 输入用于在分发服务器上运行日志读取器代理的 Windows 帐户。 指定必须在最低限度的 Windows 帐户是成员的 **db_owner** 分发数据库中的固定的数据库角色。  
  
 **密码** 和 **确认密码**  
 输入 Windows 帐户的密码。  
  
 **连接到发布服务器**  
 选择日志读取器代理来建立的连接到发布服务器通过模拟中指定的帐户是否 **进程帐户** 文本框中或通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户。 如果选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户，请输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和密码。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议您选择模拟 Windows 帐户，而不是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户。  
  
 Windows 帐户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接所使用的帐户必须至少是属于 **db_owner** 发布数据库中的固定的数据库角色。  
  
## 另请参阅  
 [管理复制中的登录名和密码](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [复制代理安全性模式](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [复制代理概述](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  