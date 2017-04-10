---
title: "为事务复制启用协调备份（复制 Transact-SQL 编程） | Microsoft Docs"
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
  - "事务复制, 备份和还原"
  - "sp_replicationdboption"
  - "使用备份同步 [SQL Server 复制]"
  - "协调备份 [SQL Server 复制]"
  - "备份 [SQL Server 复制], 事务复制"
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 为事务复制启用协调备份（复制 Transact-SQL 编程）
  在为数据库启用事务复制时，可以指定在传递到分发数据库之前必须备份所有事务。 也可以对分发数据库启用协调备份，以便在传播到分发服务器的事务未备份前不会截断发布数据库的事务日志。 有关详细信息，请参阅 [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
### 为与事务复制一起发布的数据库启用协调备份  
  
1.  在发布服务器，使用 [DATABASEPROPERTYEX & #40;Transact SQL & #41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) 函数返回 **IsSyncWithBackup** 发布数据库的属性。 如果函数返回 **1**，则表明已为发布的数据库启用了协调备份。  
  
2.  如果在步骤 1 中的函数返回 **0**, ，执行 [sp_replicationdboption & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 在发布数据库上的发布服务器。 为 **@optname** 指定值 **sync with backup**，并为 **@value** 指定 **true**。  
  
    > [!NOTE]  
    >  如果将 **sync with backup** 选项更改为 **false**，则运行日志读取器代理或达到运行间隔（如果日志读取器代理配置为连续运行）之后将更新发布数据库的截断点。 由控制的最大间隔 **– MessageInterval** 代理参数 （其默认值为 30 秒）。  
  
### 为分发数据库启用协调备份  
  
1.  在分发服务器上，使用 [DATABASEPROPERTYEX & #40;Transact SQL & #41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) 函数返回 **IsSyncWithBackup** 分发数据库的属性。 如果函数返回 **1**，则表明已为分发数据库启用了协调备份。  
  
2.  如果在步骤 1 中的函数返回 **0**, ，执行 [sp_replicationdboption & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 在分发数据库上分发服务器上。 为 **@optname** 指定值 **sync with backup** ，并为 **@value** 指定 **true**。  
  
### 禁用协调备份  
  
1.  在发布服务器上对发布数据库或分发数据库上的分发服务器上，执行 [sp_replicationdboption & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。 为 **@optname** 指定值 **sync with backup** ，并为 **@value** 指定 **false**。  
  
  