---
title: "查看分发数据库中复制的命令和其他信息（复制 Transact-SQL 编程） | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_browsereplcmds"
  - "事务复制, 监视"
  - "分发数据库 [SQL Server 复制], 查看复制的命令"
  - "查看复制的命令"
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 查看分发数据库中复制的命令和其他信息（复制 Transact-SQL 编程）
  在使用事务复制时，事务命令在分发代理将其传播到所有订阅服务器或订阅服务器中的分发代理请求更改之前存储在分发数据库中。 使用复制存储过程可以编程方式查看分发数据库中的这些挂起的命令。 有关详细信息，请参阅 [复制存储过程和 #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。  
  
### 查看分发数据库中来自所有事务发布的复制命令  
  
1.  在分发数据库上分发服务器上，执行 [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md)。  
  
### 查看分发数据库中来自使用事务复制发布的某个特定项目或特定数据库的复制命令  
  
1.  （可选）在发布服务器上对发布数据库中，执行 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)。 指定 **@publication** 和 **@article**。 请记录结果集中 **article id** 的值。  
  
2.  在分发数据库上分发服务器上，执行 [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md)。 （可选）指定从步骤 2 获得的文章 ID **@article_id**。 （可选）指定的发布数据库的 ID **@publisher_database_id**, ，从中可以从获取 **database_id** 中的列 [sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目录视图。  
  
## 另请参阅  
 [以编程方式监视复制](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  