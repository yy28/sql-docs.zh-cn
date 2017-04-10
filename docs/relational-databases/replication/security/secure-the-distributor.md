---
title: "保护分发服务器的安全 | Microsoft Docs"
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
  - "安全性 [SQL Server 复制], 分发服务器"
  - "分发服务器 [SQL Server 复制], 安全性"
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 保护分发服务器的安全
  下列复制代理连接到分发服务器：日志读取器代理、快照代理、队列读取器代理、分发代理以及合并代理。 在遵守授予必要的最低权限并保护所有密码的存储这一原则的同时，为每个代理提供适当的登录名非常重要。  
  
-   有关管理登录名和密码的信息，请参阅 [管理登录名和密码在复制中的](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)。  
  
-   有关每个代理所需权限的详细信息，请参阅 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
 除了适当地管理登录名和密码，务必了解的角色 **repl_distributor** 远程服务器链接和 **distributor_admin** 帐户。  
  
## 保护发布服务器到分发服务器的连接  
 若要管理存储的过程执行在分发服务器上的发布服务器和更新信息时，支持必要的通信，复制会自动配置远程服务器 **repl_distributor**。  **Repl_distributor** 远程服务器项用于到分发数据库，而不管分发数据库包含在发布服务器实例 （本地分发服务器） 内还是驻留在远程进行通信 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例 （远程分发服务器）。  
  
 当分发数据库包含在本地实例上时，密码将随机产生并自动配置。 分发数据库位于远程实例上，管理员可以配置共享的密码在发布服务器和分发服务器; 安装过程然后使用此密码以提供身份验证流量遍历 **repl_distributor** 链接。  
  
 分发服务器上使用 **repl_distributor** 远程服务器项来验证调用服务器配置为分发服务器上发布，验证发布服务器上，提供的密码并验证存储的过程是一个复制期间执行存储过程。  
  
 为配置的密码 **repl_distributor** 在安装过程中的远程服务器项程序与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名， **distributor_admin**, ，它将添加到 **sysadmin** 分发服务器上的固定的服务器角色。  **Distributor_admin** 连接到分发服务器时，复制存储过程使用的登录名。  
  
> [!NOTE]  
>  未更改的密码 **distributor_admin** 手动。 始终使用 **sp_changedistributor_password** 存储过程中，或 **分发服务器属性** 或 **更新复制密码** 中的对话框 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], ，这是因为密码更改随后将应用到本地发布自动。  
  
## 快照文件夹的安全性  
 确保快照共享将读权限授予合并代理（对于合并发布）或分发代理（对于快照复制或事务复制）运行时所用的帐户，并将写权限授予快照代理运行时所用的帐户。 有关快照文件夹的详细信息，请参阅 [保护快照文件夹的安全](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
## 另请参阅  
 [查看和修改复制安全设置](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [启用加密的连接到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)   
 [复制安全最佳实践](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全和保护与 #40;复制和 #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  