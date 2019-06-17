---
title: 停止复制拓扑（复制 Transact-SQL 编程）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- administering replication, quiescing
- quiesce [SQL Server replication]
- transactional replication, backup and restore
ms.assetid: 7626d575-9994-47be-b772-5b6f1b7ef7ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 59c179c81c1b6b60787603f5953b85e583668c80
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63161722"
---
# <a name="quiesce-a-replication-topology-replication-transact-sql-programming"></a>静止复制拓扑（复制 Transact-SQL 编程）
   为了“停止”系统，需要停止所有节点上已发布表的操作，并确保每个节点都已收到来自所有其他节点的所有更改。 本主题说明了如何停止复制拓扑（这是许多管理任务所必需的操作），以及如何确保节点收到来自其他节点的全部更改。  
  
### <a name="to-quiesce-a-transactional-replication-topology-with-read-only-subscriptions"></a>停止包含只读订阅的事务复制拓扑  
  
1.  停止发布服务器上所有已发布表中的活动。  
  
2.  在发布服务器的发布数据库中，执行 [sp_posttracertoken (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql)。  
  
3.  在发布服务器的发布数据库中，执行 [sp_helptracertokenhistory](/sql/relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql)。  
  
4.  确保每个订阅服务器已收到跟踪令牌。  
  
### <a name="to-quiesce-a-transactional-replication-topology-with-updatable-subscriptions"></a>停止包含可更新订阅的事务复制拓扑  
  
1.  停止发布服务器和所有订阅服务器上所有已发布表中的活动。  
  
2.  如果任何订阅服务器使用排队更新订阅：  
  
    1.  如果队列读取器代理未以连续模式运行，请运行该代理。 有关运行代理的详细信息，请参阅[复制代理可执行文件概念](../concepts/replication-agent-executables-concepts.md)或[启动和停止复制代理 (SQL Server Management Studio)](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
    2.  若要验证队列是否为空，请在每个订阅服务器上执行 [sp_replqueuemonitor](/sql/relational-databases/system-stored-procedures/sp-replqueuemonitor-transact-sql) 。  
  
3.  在发布服务器的发布数据库中，执行 [sp_posttracertoken](/sql/relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql)。  
  
4.  在发布服务器的发布数据库中，执行 [sp_helptracertokenhistory](/sql/relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql)。  
  
5.  确保每个订阅服务器已收到跟踪令牌。  
  
### <a name="to-quiesce-a-peer-to-peer-transactional-replication-topology"></a>停止对等事务复制拓扑  
  
1.  停止所有节点上所有已发布表中的活动。  
  
2.  对拓扑中每个发布数据库执行 [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) 。  
  
3.  如果日志读取器代理或分发代理未以连续模式运行，请运行该代理。 必须在启动分发代理之前启动日志读取器代理。 有关运行代理的详细信息，请参阅[复制代理可执行文件概念](../concepts/replication-agent-executables-concepts.md)或[启动和停止复制代理 (SQL Server Management Studio)](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
4.  对拓扑中每个发布数据库执行 [sp_helppeerresponses](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql) 。 确保结果集包含来自所有其他节点的响应。  
  
### <a name="to-ensure-a-peer-to-peer-node-has-received-all-prior-changes"></a>确保对等节点已收到所有以前的更改  
  
1.  对要检查的节点上的发布数据库执行 [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) 。  
  
2.  如果日志读取器代理或分发代理未以连续模式运行，请运行该代理。 必须在启动分发代理之前启动日志读取器代理。 有关运行代理的详细信息，请参阅[复制代理可执行文件概念](../concepts/replication-agent-executables-concepts.md)或[启动和停止复制代理 (SQL Server Management Studio)](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
3.  对要检查的节点上的发布数据库执行 [sp_helppeerresponses](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql) 。 确保结果集包含来自所有其他节点的响应。  
  
### <a name="to-quiesce-a-merge-replication-topology"></a>停止合并复制拓扑  
  
1.  停止发布服务器和所有订阅服务器上所有已发布表中的活动。  
  
2.  为每个订阅运行两次合并代理：首先同步所有订阅，然后再同步每个订阅一次。 这样可确保所有更改都复制到所有节点。 有关运行代理的详细信息，请参阅[复制代理可执行文件概念](../concepts/replication-agent-executables-concepts.md)或[启动和停止复制代理 (SQL Server Management Studio)](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
    > [!NOTE]  
    >  如果同步过程中出现冲突，则运行合并代理两次之后冲突解决所需的更改可能不会传播到所有节点。  
  
## <a name="see-also"></a>请参阅  
 [管理对等拓扑（复制 Transact-SQL 编程）](administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [为事务复制测量滞后时间和验证连接](../monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
