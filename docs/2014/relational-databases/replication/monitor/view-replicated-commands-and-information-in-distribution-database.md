---
title: 视图复制的命令和分发数据库 （复制 TRANSACT-SQL 编程） 中的其他信息 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- sp_browsereplcmds
- transactional replication, monitoring
- distribution databases [SQL Server replication], viewing replicated commands
- viewing replicated commands
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
caps.latest.revision: 30
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c902d09512ae0c3ede9a7831908c41ab704628f3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026317"
---
# <a name="view-replicated-commands-and-other-information-in-the-distribution-database-replication-transact-sql-programming"></a>查看分发数据库中复制的命令和其他信息（复制 Transact-SQL 编程）
  在使用事务复制时，事务命令在分发代理将其传播到所有订阅服务器或订阅服务器中的分发代理请求更改之前存储在分发数据库中。 使用复制存储过程可以编程方式查看分发数据库中的这些挂起的命令。 有关详细信息，请参阅[复制存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql)。  
  
### <a name="to-view-replicated-commands-from-all-transactional-publications-in-the-distribution-database"></a>查看分发数据库中来自所有事务发布的复制命令  
  
1.  在分发服务器的分发数据库中，执行 [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql)。  
  
### <a name="to-view-replicated-commands-in-the-distribution-database-from-a-specific-article-or-from-a-specific-database-published-using-transactional-replication"></a>查看分发数据库中来自使用事务复制发布的某个特定项目或特定数据库的复制命令  
  
1.  （可选）在发布服务器的发布数据库中，执行 [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql)。 指定 **@publication** 和 **@article**。 请记录结果集中 **article id** 的值。  
  
2.  在分发服务器的分发数据库中，执行 [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql)。 （可选）为 **@article_id**。 （可选）为 **@publisher_database_id**指定发布数据库的 ID，此 ID 可以从 **sys.databases** 目录视图的 [database_id](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 列获得。  
  
## <a name="see-also"></a>请参阅  
 [以编程方式监视复制](monitoring-replication-overview.md)  
  
  
