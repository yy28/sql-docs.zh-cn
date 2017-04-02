---
title: "MSSQL_ENG021797 | Microsoft Docs"
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
  - "MSSQL_ENG021797 错误"
ms.assetid: 54d83a1e-43fd-449c-a2b2-fdda2609a534
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG021797
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21797|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|'%s' 必须是有效的 Windows 登录名，且格式为: '计算机\登录名' 或 '域\登录名'。 请参阅 '%s' 的文档。|  
  
## 解释  
 如果指定的值，下列复制存储过程会引发此错误 **@job_login** 参数为 null 或无效。 如果的成员，可能出现此错误 **db_owner** 固定的数据库角色运行的脚本从以前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中的安全模式已更改，因此必须更新这些脚本。  
  
-   [sp_addlogreader_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
-   [sp_addqreader_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
-   [sp_addpublication_snapshot & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
-   [sp_addpushsubscription_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)  
  
-   [sp_addpullsubscription_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepushsubscription_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepullsubscription_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 成员可以执行这些存储的过程 **sysadmin** 上相应的服务器或成员的固定的服务器角色 **db_owner** 在相应的数据库的固定的数据库角色。 每个存储过程都创建代理作业，并允许指定用于运行代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。 中的用户 **sysadmin** 角色、 代理作业隐式创建即使未指定 Windows 帐户 （如果指定了帐户，它必须是有效）; 代理运行的上下文下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在相应的服务器的代理服务帐户。 虽然帐户不是必需的，但为代理指定单独的帐户却是最佳安全方法。 有关详细信息，请参阅 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## 用户操作  
 请确保指定为有效的 Windows 帐户 **@job_login** 每个过程的参数。 如果您具有早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的复制脚本，请更新这些脚本以包括 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]所需的存储过程和参数。 有关详细信息，请参阅 [升级复制脚本 & #40;复制 TRANSACT-SQL 编程 & #41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)。  
  
## 另请参阅  
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  