---
title: "MSSQL_REPL020011 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_REPL020011 错误"
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_REPL020011
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|20011|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|进程无法在“%2”上执行“%1”。|  
  
## 解释  
 处理，如当日志读取器代理执行的事务复制期间可以在许多情况下引发此错误 **sp_replcmds** (进程无法在执行 'sp_replcmds' \< 服务器名>) 或 **sp_repldone** (进程无法在执行 sp_repldone \< 服务器名>)。  
  
## 用户操作  
 如果您只需从备份还原的数据库中会出现此错误，请确保已执行备份和还原文档，包括执行中概述的步骤 **sp_replrestart** 根据。 有关详细信息，请参阅 [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
 此错误是一个内部处理错误，如果在还原之外的环境中出现此错误，则通常表示必须删除或重新配置复制。 如果无法删除复制，请与客户支持部门联系以获取帮助。  
  
## 另请参阅  
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [sp_replcmds & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)  
  
  