---
title: KILL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- KILL_TSQL
- KILL
dev_langs:
- TSQL
helpviewer_keywords:
- WITH STATUSONLY option
- terminating distributed transactions
- distributed transactions [SQL Server], terminating
- in-doubt transactions
- IDs [SQL Server], user processes
- ending distributed transactions [SQL Server]
- stopping distributed transactions
- session IDs [SQL Server]
- system process termination [SQL Server]
- stopping processes
- ending processes [SQL Server]
- UOW [SQL Server]
- orphaned transactions [SQL Server]
- unit of work [SQL Server]
- process termination [SQL Server]
- KILL statement
- terminating process
ms.assetid: 071cf260-c794-4b45-adc0-0e64097938c0
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3b40c02d7118b1d844263b1c298f256b74d95fea
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36255569"
---
# <a name="kill-transact-sql"></a>KILL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  终止基于会话 ID 或工作单元 (UOW) 的用户进程。 如果指定的会话 ID 或 UOW 有许多工作要撤消，则 KILL 语句可能需要一些时间来完成，特别是在涉及回滚长事务时。  
  
 KILL 可用于终止正常连接，这将在内部终止与指定会话 ID 关联的事务。 如果正在使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC)，该语句还可用于终止所有孤立和有疑问的分布式事务。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
  
KILL { session ID | UOW } [ WITH STATUSONLY ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
KILL 'session_id'  
[;]   
```  
  
## <a name="arguments"></a>参数  
 session ID  
 要终止的进程的会话 ID。 session ID 是在建立连接时为每个用户连接分配的唯一整数 (int)。 在连接期间，会话 ID 值与该连接捆绑在一起。 连接结束时，则释放该整数值，并且可以将它重新分配给新的连接。  
以下查询可帮助确定想要终止的 `session_id`：  
 ```sql  
 SELECT conn.session_id, host_name, program_name,
     nt_domain, login_name, connect_time, last_request_end_time 
FROM sys.dm_exec_sessions AS sess
JOIN sys.dm_exec_connections AS conn
    ON sess.session_id = conn.session_id;
```  
  
UOW  
适用范围：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 标识分布式事务的工作单元 ID (UOW)。 UOW 是可以从 sys.dm_tran_locks 动态管理视图的 request_owner_guid 列获取的 GUID。 也可以从错误日志中或通过 MS DTC 监视器获取 UOW。 有关监视分布式事务的详细信息，请参阅 MS DTC 文档。  
  
 使用 KILL UOW 可终止孤立的分布式事务。 这些事务不与任何真实的会话 ID 相关联，与虚拟的会话 ID = '-2' 相关联。 可使标识孤立事务变得更为简单，其方法是查询 sys.dm_tran_locks、sys.dm_exec_sessions 或 sys.dm_exec_requests 动态管理视图中的会话 ID 列。  
  
 WITH STATUSONLY  
 生成由于更早的 KILL 语句而正在回滚的指定 session ID 或 UOW 的进度报告。 KILL WITH STATUSONLY 不终止或回滚 session ID 或 UOW，该命令只显示当前的回滚进度。  
  
## <a name="remarks"></a>Remarks  
 KILL 命令通常用于终止这样一些进程：它们以锁阻塞了其他重要进程，或者正在执行一个查询，而该查询正在使用必需的系统资源。 系统进程和运行扩展存储过程的进程不能被终止。  
  
 应当小心使用 KILL，特别是正在运行重要进程时。 用户不能取消自己的进程。 其他不能取消的进程包括：  
  
-   AWAITING COMMAND  
-   CHECKPOINT SLEEP  
-   LAZY WRITER  
-   LOCK MONITOR  
-   SIGNAL HANDLER  
  
使用 @@SPID 可显示当前会话的 session ID 值。  
  
 若要获取活动会话 ID 值的报告，可以查询 sys.dm_tran_locks、sys.dm_exec_sessions 和 sys.dm_exec_requests 动态管理视图中的 session_id 列。 还可以查看 sp_who 系统存储过程返回的 SPID 列。 如果特定 SPID 的回滚正在进行，则该 SPID 的 sp_who 结果集中的 cmd 列指示 KILLED/ROLLBACK。  
  
 当特定的连接在数据库资源上有锁并阻塞其他连接的进程时，`blocking_session_id` 的 `sys.dm_exec_requests` 列或 `blk` 返回的 `sp_who` 列中将显示该阻塞连接的会话 ID。  
  
 KILL 命令可用于解决有疑问的分布式事务。 这些事务是未解决的分布式事务，它们是由于无计划地重新启动数据库服务器或 MS DTC 协调器而产生的。 有关未决事务的详细信息，请参阅[使用标记的事务一致地恢复相关的数据库的事务（完全恢复模式）](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)中的“两阶段提交”一节。  
  
## <a name="using-with-statusonly"></a>使用 WITH STATUSONLY  
 仅当前面的 KILL session ID|UOW 语句导致 session ID 或 UOW 当前正在回滚时，KILL WITH STATUSONLY 才会生成报告。 进度报告指出已完成的回滚量（百分比）和估计的剩余时间（秒），格式如下：  
  
 `Spid|UOW <xxx>: Transaction rollback in progress. Estimated rollback completion: <yy>% Estimated time left: <zz> seconds`  
  
 如果执行 KILL session ID|UOW WITH STATUSONLY 语句时，session ID 或 UOW 的回滚已完成，或者没有 session ID 或 UOW 正在回滚，KILL session ID|UOW WITH STATUSONLY 返回以下错误：  
  
 ```
"Msg 6120, Level 16, State 1, Line 1"  
"Status report cannot be obtained. Rollback operation for Process ID <session ID> is not in progress."
```  
  
 通过重复不带 WITH STATUSONLY 选项的同一 KILL session ID|UOW 语句，可以获得相同的状态报告；但不推荐这样做。 如果在运行新的 KILL 语句之前回滚已完成并且已将 session ID 重新分配给新任务，那么重复 KILL session ID 语句可能会终止新进程。 指定 WITH STATUSONLY 将防止这种情况发生。  
  
## <a name="permissions"></a>权限  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]：** 需要具有 ALTER ANY CONNECTION 权限。 ALTER ANY CONNECTION 包括在 sysadmin 或 processadmin 固定服务器角色的成员身份中。  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]：** 需要具有 KILL DATABASE CONNECTION 权限。 服务器级别主体登录名具有 KILL DATABASE CONNECTION。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-kill-to-terminate-a-session"></a>A. 使用 KILL 终止会话  
 以下示例显示如何终止会话 ID `53`。  
  
```sql  
KILL 53;  
GO  
```  
  
### <a name="b-using-kill-session-id-with-statusonly-to-obtain-a-progress-report"></a>B. 使用 KILL session ID WITH STATUSONLY 获取进度报告  
 以下示例为特定的会话 ID 生成回滚进程的状态。  
  
```sql  
KILL 54;  
KILL 54 WITH STATUSONLY;  
GO  
  
--This is the progress report.  
spid 54: Transaction rollback in progress. Estimated rollback completion: 80% Estimated time left: 10 seconds.  
```  
  
### <a name="c-using-kill-to-terminate-an-orphaned-distributed-transaction"></a>C. 使用 KILL 终止孤立的分布式事务  
 以下示例显示如何终止 UOW 为 `D5499C66-E398-45CA-BF7E-DC9C194B48CF` 的孤立分布式事务（session ID = -2）。  
  
```sql  
KILL 'D5499C66-E398-45CA-BF7E-DC9C194B48CF';  
```  

  
## <a name="see-also"></a>另请参阅  
 [KILL STATS JOB (Transact-SQL)](../../t-sql/language-elements/kill-stats-job-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION (Transact-SQL)](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [SHUTDOWN (Transact-SQL)](../../t-sql/language-elements/shutdown-transact-sql.md)   
 [@@SPID (Transact-SQL)](../../t-sql/functions/spid-transact-sql.md)   
 [sys.dm_exec_requests (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_tran_locks (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [sp_lock (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  
