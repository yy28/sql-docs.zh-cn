---
title: "MSSQL_ENG021798 | Microsoft Docs"
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
  - "MSSQL_ENG021798 错误"
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_ENG021798
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21798|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|在继续操作之前，必须通过 '%s' 添加 '%s' 代理作业。 请参阅 '%s' 的文档。|  
  
## 解释  
 若要创建发布，您必须 **sysadmin** 上发布服务器或成员的固定的服务器角色 **db_owner** 发布数据库中的固定的数据库角色。 如果您的成员 **db_owner** 如果，则会引发角色，此错误︰  
  
-   从 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]运行脚本。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中的安全模式已更改，因此必须更新这些脚本。  
  
-   存储的过程 **sp_addpublication** 在执行之前执行 [sp_addlogreader_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)。 这适用于所有的事务发布。  
  
-   存储的过程 **sp_addpublication** 在执行之前执行 [sp_addqreader_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)。 这适用于为排队更新订阅启用的事务发布 (值为 TRUE **@allow_queued_tran** 参数 **sp_addpublication**)。  
  
 存储的过程 **sp_addlogreader_agent** 和 **sp_addqreader_agent** 每创建代理作业，并允许您指定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户下运行的代理。 中的用户 **sysadmin** 角色、 代理作业隐式创建如果 **sp_addlogreader_agent** 和 **sp_addqreader_agent** 便不会执行; 代理运行的上下文下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分发服务器上的代理服务帐户。 尽管 **sp_addlogreader_agent** 和 **sp_addqreader_agent** 对中的用户不是必需 **sysadmin** 角色，它是最佳安全方案来为代理指定单独的帐户。 有关详细信息，请参阅 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## 用户操作  
 请确保按正确的顺序执行过程。 有关详细信息，请参阅 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。 如果有早期版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的复制脚本，请更新这些脚本以使其包含 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本所需的存储过程和参数。 有关详细信息，请参阅 [升级复制脚本 & #40;复制 TRANSACT-SQL 编程 & #41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)。  
  
## 另请参阅  
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  