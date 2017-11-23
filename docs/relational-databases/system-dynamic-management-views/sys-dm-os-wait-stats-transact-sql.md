---
title: "sys.dm_os_wait_stats (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_wait_stats_TSQL
- dm_os_wait_stats
- sys.dm_os_wait_stats
- sys.dm_os_wait_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_wait_stats dynamic management view
ms.assetid: 568d89ed-2c96-4795-8a0c-2f3e375081da
caps.latest.revision: "111"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: b171317170d9144edb71dfb29b36940ce6d7ee31
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmoswaitstats-transact-sql"></a>sys.dm_os_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回执行的线程所遇到的所有等待的相关信息。 可以使用此聚合视图来诊断 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以及特定查询和批处理的性能问题。 [sys.dm_exec_session_wait_stats &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)提供会话的类似信息。  
  
> [!NOTE] 
> 若要从我们称之为**[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** ，使用名称**sys.dm_pdw_nodes_os_wait_stats**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar(60)**|等待类型的名称。 有关详细信息，请参阅[等待类型](#WaitTypes)，本主题中更高版本。|  
|waiting_tasks_count|**bigint**|该等待类型的等待数。 该计数器在每开始一个等待时便会增加。|  
|wait_time_ms|**bigint**|该等待类型的总等待时间（毫秒）。 该时间包括 signal_wait_time_ms。|  
|max_wait_time_ms|**bigint**|该等待类型的最长等待时间。|  
|signal_wait_time_ms|**bigint**|正在等待的线程从收到信号通知到其开始运行之间的时差。|  
|pdw_node_id|**int**|此分布的节点标识符。 <br/> **适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
  
## <a name="permissions"></a>Permissions  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层，需要`VIEW DATABASE STATE`数据库中的权限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准版和基本层，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。  
  
##  <a name="WaitTypes"></a>等待的类型  
 **资源等待**工作线程请求访问资源，因为正由其他某个工作线程或尚不可用的资源不可用时，会发生资源等待。 资源等待的示例包括锁等待、闩锁等待、网络等待以及磁盘 I/O 等待。 锁等待和闩锁等待是指等待同步对象  
  
**队列等待**  
 当工作线程空闲，等待分配工作时便会发生队列等待。 队列等待通常发生在系统后台任务（如监视死锁以及清除已删除的记录等任务）中。 这些任务将等待工作请求被放入工作队列。 即使没有新数据包放入队列，队列等待也可能定期处于活动状态。  
  
 **外部等待**  
 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作线程正在等待外部事件（如扩展存储过程调用或链接服务器查询）完成时，便会发生外部等待。 当诊断有妨碍的问题时，请记住，外部等待不会始终表示工作线程处于空闲状态，因为工作线程可能处于活动状态且正在运行某些外部代码。  
  
 `sys.dm_os_wait_stats` 显示已完成的等待时间。 此动态管理视图不显示当前等待。  
  
 如果出现下列任一情况，则不认为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作线程处于等待状态：  
  
-   资源变得可用。  
  
-   查询非空。  
  
-   外部进程完成。  
  
 尽管线程不再处于等待状态，但是它不必立即开始运行。 这是因为此类线程首先放入可运行工作线程的队列中，并且必须等待量程在计划程序中运行。  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]等待时间计数器**bigint**值，因此不容易，只需计数器滚动更新导致的早期版本中的等效计数器那样[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 执行查询期间的特定等待时间类型可以说明查询中存在瓶颈或失效点。 同样，如果服务器级的等待时间较长或等待计数较多，说明服务器实例内交互查询交互中存在瓶颈或热点。 例如，锁等待指示查询争用数据；页 IO 闩锁等待指示 IO 响应时间较慢；页闩锁更新指示表示文件布局不正确。  
  
 此动态管理视图的内容可通过运行以下命令来重置：  
  
``` t-sql  
DBCC SQLPERF ('sys.dm_os_wait_stats', CLEAR);  
GO  
```  
  
该命令将所有计数器重置为 0。  
  
> [!NOTE]
> 这些统计信息在每次重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时都不能持续存在，并且所有的数据均为自上次重置统计信息或启动服务器以来累积的数据。  
  
 下表列出各任务所遇到的等待类型。  

|类型 |Description| 
|-------------------------- |--------------------------| 
|ABR |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| | 
|AM_INDBUILD_ALLOCATION |TBD <br />**适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|AM_SCHEMAMGR_UNSHARED_CACHE |TBD <br />**适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ASSEMBLY_FILTER_HASHTABLE |TBD <br />**适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ASSEMBLY_LOAD |在以独占的方式访问程序集加载时出现。| 
|ASYNC_DISKPOOL_LOCK |当尝试同步并行的线程（执行创建或初始化文件等任务）时出现。| 
|ASYNC_IO_COMPLETION |当某任务正在等待 I/O 完成时出现。| 
|ASYNC_NETWORK_IO |当任务被阻止在网络之后时出现在网络写入中。 验证客户端是否正在处理来自服务器的数据。| 
|ASYNC_OP_COMPLETION |TBD <br />**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ASYNC_OP_CONTEXT_READ |TBD <br />**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ASYNC_OP_CONTEXT_WRITE |TBD <br />**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ASYNC_SOCKETDUP_IO |TBD <br />**适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|AUDIT_GROUPCACHE_LOCK |当等待控制对某个特殊缓存的访问的锁时出现。 该缓存包含正在使用哪些审核来审核每个审核操作组的相关信息。| 
|AUDIT_LOGINCACHE_LOCK |当等待控制对某个特殊缓存的访问的锁时出现。 该缓存包含正在使用哪些审核来审核登录审核操作组的相关信息。| 
|AUDIT_ON_DEMAND_TARGET_LOCK |当等待用于确保扩展事件目标相关审核的单一初始化的锁时出现。| 
|AUDIT_XE_SESSION_MGR |当等待用于同步扩展事件会话相关审核的启动和停止的锁时出现。| 
|BACKUP |当任务作为备份处理的一部分被阻止时出现。| 
|BACKUP_OPERATOR |当任务正在等待磁带装入时出现。 若要查看磁带状态，请查询 sys.dm_io_backup_tapes。 如果装入操作没有挂起，则该等待类型可能指示磁带机发生硬件问题。| 
|BACKUPBUFFER |在备份任务等待数据或等待用来存储数据的缓冲区时发生。 此类型不常见，只有当任务等待装入磁带时才会出现。| 
|BACKUPIO |在备份任务等待数据或等待用来存储数据的缓冲区时发生。 此类型不常见，只有当任务等待装入磁带时才会出现。| 
|BACKUPTHREAD |当某任务正在等待备份任务完成时出现。 等待时间可能较长，从几分钟到几个小时。 如果被等待的任务正处于 I/O 进程中，则该类型不指示发生问题。| 
|BAD_PAGE_PROCESS |当后台可疑页记录器正在尝试避免每隔五秒以上的时间运行时出现。 过多的可疑页会导致记录器频繁运行。| 
|BLOB_METADATA |TBD <br />**适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BMPALLOCATION |TBD <br />**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BMPBUILD |TBD <br />**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BMPREPARTITION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BMPREPLICATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BPSORT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_CONNECTION_RECEIVE_TASK |在等待访问以便在连接端点上接收消息时出现。 已序列化对端点的接收访问。| 
|BROKER_DISPATCHER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_ENDPOINT_STATE_MUTEX |当存在的争用，访问 Service Broker 连接终结点的状态时发生。 已序列化对更改状态的访问。| 
|BROKER_EVENTHANDLER |当某任务正在等待 Service Broker 主事件处理程序中时发生。 出现时间应该非常短暂。| 
|BROKER_FORWARDER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_INIT |当初始化每个活动数据库中的 Service Broker 时出现。 该状态应当频繁出现。| 
|BROKER_MASTERSTART |当某任务正在等待对以启动 Service broker 主事件处理程序时发生。 出现时间应该非常短暂。| 
|BROKER_RECEIVE_WAITFOR |当 RECEIVE WAITFOR 正在等待时出现。 如果没有准备接收的消息，则通常出现该状态。| 
|BROKER_REGISTERALLENDPOINTS |在 Service Broker 连接终结点的初始化期间出现。 出现时间应该非常短暂。| 
|BROKER_SERVICE |当更新或重新设定优先顺序与目标服务关联的 Service Broker 目标列表时发生。| 
|BROKER_SHUTDOWN |按计划的关闭 Service broker 时出现。 该状态出现的时间应当尽量短暂。| 
|BROKER_START |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TASK_SHUTDOWN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TASK_STOP |当 Service Broker 队列任务处理程序尝试关闭任务时发生。 已序列化状态检查，并且必须预先处于运行状态。| 
|BROKER_TASK_SUBMIT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TO_FLUSH |当 Service Broker 延迟 flusher 刷新中内存传输对象添加到工作表时发生。| 
|BROKER_TRANSMISSION_OBJECT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TRANSMISSION_TABLE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TRANSMISSION_WORK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TRANSMITTER |当 Service Broker 发送器正在等待工作时出现。| 
|BUILTIN_HASHKEY_MUTEX |可能在实例启动之后而在初始化内部数据结构时出现。 数据结构初始化之后将不会再次出现。| 
|CHANGE_TRACKING_WAITFORCHANGES |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CHECK_PRINT_RECORD |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|CHECK_SCANNER_MUTEX |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CHECK_TABLES_INITIALIZATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CHECK_TABLES_SINGLE_SCAN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CHECK_TABLES_THREAD_BARRIER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CHECKPOINT_QUEUE |当检查点任务正在等待下一个检查点请求时出现。| 
|CHKPT |在服务器启动时出现以通知检查点线程可以启动。| 
|CLEAR_DB |在执行会更改数据库状态的操作过程中发生，例如打开或关闭数据库。| 
|CLR_AUTO_EVENT |当某任务当前正在执行公共语言运行时 (CLR) 执行并且正在等待特殊的自动事件启动时出现。 通常会出现长时间等待，这并不意味着出现问题。| 
|CLR_CRST |当某任务当前正在执行 CLR 执行并且正在等待输入当前由另一项任务正在使用的任务的关键部分时出现。| 
|CLR_JOIN |当某任务当前正在执行 CLR 执行并且正在等待另一项任务结束时出现。 当两任务之间具有联接时出现该等待状态。| 
|CLR_MANUAL_EVENT |当某任务当前正在执行 CLR 执行并且正在等待特定手动事件启动时出现。| 
|CLR_MEMORY_SPY |当为用于记录来自 CLR 的所有虚拟内存分配的数据结构等待获取锁时出现。 如果存在并行访问，该数据结构将被锁定以维护其完整性。| 
|CLR_MONITOR |当某任务当前正在执行 CLR 执行并且正在等待获取用于监视器的锁时出现。| 
|CLR_RWLOCK_READER |当某任务当前正在执行 CLR 执行并且正在等待读取器锁时出现。| 
|CLR_RWLOCK_WRITER |当某任务当前正在执行 CLR 执行并且正在等待编写器锁时出现。| 
|CLR_SEMAPHORE |当某任务当前正在执行 CLR 执行并且正在等待信号量时出现。| 
|CLR_TASK_START |在等待 CLR 任务完成启动时出现。| 
|CLRHOST_STATE_ACCESS |当等待获取对 CLR 宿主数据结构的独占访问时出现。 当设置或关闭 CLR 运行时时出现此等待类型。| 
|CMEMPARTITIONED |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CMEMTHREAD |当某任务正在等待线程安全内存对象时出现。 当多项任务尝试分配来自同一个内存对象的内存而导致出现争用时，便可能延长等待时间。| 
|COLUMNSTORE_BUILD_THROTTLE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|COLUMNSTORE_COLUMNDATASET_SESSION_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|COMMIT_TABLE |TBD| 
|CONNECTION_ENDPOINT_LOCK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|COUNTRECOVERYMGR |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CREATE_DATINISERVICE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CXPACKET |当同步查询处理器交换迭代器，并生成和使用行时出现并行查询计划。 如果等待太久，无法通过优化查询（如添加索引）来减少等待时间，请考虑调整并行度的开销阈值或降低并行度。| 
|CXROWSET_SYNC |在并行范围扫描期间出现。| 
|DAC_INIT |当正在初始化专用管理员连接时出现。| 
|DBCC_SCALE_OUT_EXPR_CACHE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DBMIRROR_DBM_EVENT |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|DBMIRROR_DBM_MUTEX |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|DBMIRROR_EVENTS_QUEUE |在数据库镜像等待处理事件时出现。| 
|DBMIRROR_SEND |当某任务正在等待清除网络层的通信积压以便能够发送消息时出现。 指示通信层正在开始重载并影响数据库镜像数据吞吐量。| 
|DBMIRROR_WORKER_QUEUE |指示数据库镜像工作线程任务正在等待更多的工作。| 
|DBMIRRORING_CMD |当某任务正在等待日志记录刷新到磁盘时出现。 该等待状态应当保留较长的时间。| 
|DBSEEDING_FLOWCONTROL |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DBSEEDING_OPERATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DEADLOCK_ENUM_MUTEX |请确保 SQL Server 在同一时间未运行多个死锁搜索时所尝试的死锁监视器和 sys.dm_os_waiting_tasks 时发生。| 
|DEADLOCK_TASK_SEARCH |长时间等待此资源指示服务器正在 sys.dm_os_waiting_tasks 之上执行查询，并且这些查询正在阻止死锁监视器运行死锁搜索。 该等待类型仅供死锁监视器使用。 sys.dm_os_waiting_tasks 之上的查询使用 DEADLOCK_ENUM_MUTEX。| 
|DEBUG |TRANSACT-SQL 和 CLR 调试内部同步期间发生。| 
|DIRECTLOGCONSUMER_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DIRTY_PAGE_POLL |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DIRTY_PAGE_SYNC |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DIRTY_PAGE_TABLE_LOCK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DISABLE_VERSIONING |SQL Server 轮询版本事务管理器，以查看最早的活动事务的时间戳是否晚于状态开始更改的时间戳时发生。 如果是，则所有在 ALTER DATABASE 语句运行之前启动的快照事务都已完成。 SQL Server 使用 ALTER DATABASE 语句禁用版本控制时，将使用该等待状态。| 
|DISKIO_SUSPEND |当某任务正在等待访问文件（外部备份处于活动状态）时出现。 针对每个正在等待的用户进程报告该状态。 每个用户进程大于五的计数可能指示外部备份需要太长时间才能完成。| 
|DISPATCHER_PRIORITY_QUEUE_SEMAPHORE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DISPATCHER_QUEUE_SEMAPHORE |当调度程序池中的线程正在等待更多要处理的工作时出现。 当调度程序处于空闲状态时，此等待类型的等待时间预计要增加。| 
|DLL_LOADING_MUTEX |在等待 XML 分析器 DLL 加载时出现。| 
|DPT_ENTRY_LOCK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DROP_DATABASE_TIMER_TASK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DROPTEMP |在上次尝试删除临时对象失败后再进行下次尝试之前出现。 对于每一次失败的删除尝试，等待持续时间都以指数形式增长。| 
|DTC |当某任务正在等待用于管理状态转换的事件时出现。 恢复 Microsoft 分布式事务处理协调器 (MS DTC) 事务发生 SQL Server 接收 MS DTC 服务已变为不可用的通知之后时此状态控制。| 
|DTC_ABORT_REQUEST |当 MS DTC 工作线程会话正在等待获得 MS DTC 事务的所有权时，在该会话中出现。 当 MS DTC 拥有了事务后，该会话可以回滚事务。 通常，该会话将等待另一个正在使用事务的会话。| 
|DTC_RESOLVE |当恢复任务正在等待跨数据库事务中的 master 数据库以查询该事务的结果时出现。| 
|DTC_STATE |当某任务正在等待对内部 MS DTC 全局状态对象的更改进行保护的事件时出现。 该状态应当保持非常短的时间。| 
|DTC_TMDOWN_REQUEST |在 SQL Server 时接收通知，MS DTC 服务不可用 MS DTC 工作线程会话中出现。 首先，工作线程将等待 MS DTC 恢复进程启动。 然后，工作线程等待获取其正在处理的分布式事务的结果。 此过程可能一直执行，直到重新建立与 MS DTC 服务的连接。| 
|DTC_WAITFOR_OUTCOME |当恢复任务等待 MS DTC 处于活动状态以启用准备好的事务的解决方法时出现。| 
|DTCNEW_ENLIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DTCNEW_PREPARE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DTCNEW_RECOVERY |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DTCNEW_TM |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DTCNEW_TRANSACTION_ENLISTMENT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DTCPNTSYNC |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DUMP_LOG_COORDINATOR |当主任务正在等待子任务生成数据时出现。 该状态通常不会出现。 长时间的等待指示出现意外的阻塞。 应当对子任务进行调查。| 
|DUMP_LOG_COORDINATOR_QUEUE |TBD| 
|DUMPTRIGGER |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|EC |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|EE_PMOLOCK |在语句执行过程中特定的内存分配类型同步期间出现。| 
|EE_SPECPROC_MAP_INIT |在对内部过程哈希表创建进行同步期间发生。 此等待只能发生的初始访问期间哈希表的 SQL Server 实例启动后。| 
|ENABLE_EMPTY_VERSIONING |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ENABLE_VERSIONING |SQL Server 等待声明数据库可以转换到快照隔离允许的状态之前完成此数据库中的所有更新事务时出现。 SQL Server 使用 ALTER DATABASE 语句启用快照隔离时，将使用此状态。| 
|ERROR_REPORTING_MANAGER |在对多个并发错误日志初始化进行同步期间发生。| 
|EXCHANGE |在并行查询过程中查询处理器交换迭代器同步期间出现。| 
|EXECSYNC |在并行查询过程中同步与交换迭代器无关的区域内的查询处理器期间出现。 例如，此类区域包括位图、二进制大型对象 (LOB) 以及假脱机迭代器等。 LOB 可能会经常使用该等待状态。| 
|EXECUTION_PIPE_EVENT_INTERNAL |当同步通过连接上下文提交的批处理执行的创建器和使用者部件期间出现。| 
|EXTERNAL_RG_UPDATE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|EXTERNAL_SCRIPT_NETWORK_IO |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|EXTERNAL_SCRIPT_PREPARE_SERVICE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|EXTERNAL_SCRIPT_SHUTDOWN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|EXTERNAL_WAIT_ON_LAUNCHER， |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_HADR_TRANSPORT_CONNECTION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_REPLICA_CONTROLLER_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_REPLICA_CONTROLLER_STATE_AND_CONFIG |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_REPLICA_PUBLISHER_EVENT_PUBLISH |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_REPLICA_PUBLISHER_SUBSCRIBER_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_WAIT_FOR_BUILD_REPLICA_EVENT_PROCESSING |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FAILPOINT |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|FCB_REPLICA_READ |当同步快照（或 DBCC 创建的临时快照）稀疏文件的读取时出现。| 
|FCB_REPLICA_WRITE |当同步快照（或 DBCC 创建的临时快照）稀疏文件的页推送或页请求时出现。| 
|FEATURE_SWITCHES_UPDATE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_DB_KILL_FLAG |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_DB_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FCB |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FCB_FIND |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FCB_PARENT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FCB_RELEASE_CACHED_ENTRIES |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FCB_STATE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FILEOBJECT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_TABLE_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NTFS_STORE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_RECOVERY |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_RSFX_COMM |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_RSFX_WAIT_FOR_MEMORY |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_STARTUP_SHUTDOWN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_STORE_DB |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_STORE_ROWSET_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_STORE_TABLE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILE_VALIDATION_THREADS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_CACHE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_CHUNKER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_CHUNKER_INIT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_FCB |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_FILE_OBJECT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_WORKITEM_QUEUE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILETABLE_SHUTDOWN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FOREIGN_REDO |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|FORWARDER_TRANSITION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FS_FC_RWLOCK |当 FILESTREAM 垃圾收集器等待执行下列操作之一时出现：| 
|FS_GARBAGE_COLLECTOR_SHUTDOWN |当 FILESTREAM 垃圾收集器等待清除任务完成时出现。| 
|FS_HEADER_RWLOCK |当等待获取对 FILESTREAM 数据容器的 FILESTREAM 标头的访问，以便读取或更新 FILESTREAM 标头文件 (Filestream.hdr) 中的内容时出现。| 
|FS_LOGTRUNC_RWLOCK |当等待获取对 FILESTREAM 日志截断的访问以执行下列操作之一时出现：| 
|FSA_FORCE_OWN_XACT |当 FILESTREAM 文件 I/O 操作需要绑定到关联的事务，但该事务当前由另一个会话拥有时出现。| 
|FSAGENT |当 FILESTREAM 文件 I/O 操作等待的 FILESTREAM 代理资源正由另一个文件 I/O 操作使用时出现。| 
|FSTR_CONFIG_MUTEX |当等待另一个 FILESTREAM 功能重新配置完成时出现。| 
|FSTR_CONFIG_RWLOCK |当等待序列化对 FILESTREAM 配置参数的访问时出现。| 
|FT_COMPROWSET_RWLOCK |全文正在等待片段元数据操作。 记录为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|FT_IFTS_RWLOCK |全文正在等待内部同步。 记录为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|FT_IFTS_SCHEDULER_IDLE_WAIT |全文计划程序睡眠等待类型。 计划程序空闲。| 
|FT_IFTSHC_MUTEX |全文正在等待 fdhost 控制操作。 记录为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|FT_IFTSISM_MUTEX |全文正在等待通信操作。 记录为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|FT_MASTER_MERGE |全文正在等待主合并操作。 记录为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|FT_MASTER_MERGE_COORDINATOR |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FT_METADATA_MUTEX |记录为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|FT_PROPERTYLIST_CACHE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FT_RESTART_CRAWL |在全文爬网需要从上一个已知可用点重新启动以便从暂时故障中恢复时出现。 等待使当前正在此总体中工作的工作线程任务完成或退出当前步骤。| 
|FULLTEXT GATHERER |在同步全文操作期间发生。| 
|GDMA_GET_RESOURCE_OWNER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GHOSTCLEANUP_UPDATE_STATS |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|GHOSTCLEANUPSYNCMGR |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GLOBAL_QUERY_CANCEL |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|GLOBAL_QUERY_CLOSE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GLOBAL_QUERY_CONSUMER |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|GLOBAL_QUERY_PRODUCER |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|GLOBAL_TRAN_CREATE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GLOBAL_TRAN_UCS_SESSION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GUARDIAN |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|HADR_AG_MUTEX |当的 Alwayson DDL 语句或 Windows Server 故障转移群集命令等待独占的读/写访问的可用性组配置时出现。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_AR_CRITICAL_SECTION_ENTRY |Alwayson DDL 语句或 Windows Server 故障转移群集命令等待独占的读/写访问的关联的可用性组的本地副本的运行时状态时发生。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_AR_MANAGER_MUTEX |在可用性副本关闭正在等待完成启动或可用性副本启动正在等待完成关闭时发生。 仅限内部使用。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_AR_UNLOAD_COMPLETED |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_ARCONTROLLER_NOTIFICATIONS_SUBSCRIBER_LIST |可用性副本事件（例如，状态更改或配置更改）的发布服务器正在等待对事件订阅服务器列表的独占的读/写访问。 仅限内部使用。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_BACKUP_BULK_LOCK |Alwayson 主数据库收到来自辅助数据库的备份请求并且正在等待后台线程完成处理上获取或释放 BulkOp 锁的请求。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_BACKUP_QUEUE |Alwayson 主数据库的备份的后台线程正在等待来自辅助数据库的新工作请求。 （通常情况下，此过程发生时主数据库是持有 BulkOp 日志，正在等待辅助数据库，以指示主数据库可以释放锁）。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_CLUSAPI_CALL |SQL Server 线程正在等待从非抢先模式 （SQL server 已计划） 切换到抢先模式 （由操作系统已计划），因此，为了调用 Windows Server 故障转移群集 Api。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_COMPRESSED_CACHE_SYNC |等待对用于避免冗余压缩发送到多个辅助数据库的日志块的压缩的日志块缓存的访问。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_CONNECTIVITY_INFO |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DATABASE_FLOW_CONTROL |在已达到排队消息的最大数目时正在等待消息发送到伙伴。 指示日志扫描的运行运行速度要快于网络发送速度。 这是一个问题，只有网络发送比预期要慢。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DATABASE_VERSIONING_STATE |在版本控制状态更改的 Alwayson 辅助数据库上发生。 此等待是内部数据结构，通常是与不会直接影响对数据访问很短。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DATABASE_WAIT_FOR_RECOVERY |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DATABASE_WAIT_FOR_RESTART |等待要重新启动 Alwayson 可用性组控制下的数据库。 正常情况下，这不是客户问题因为此处应等待。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING |一种查询可读辅助数据库的 Always On 可用性组在等待提交或回滚时，对读取工作负荷启用辅助副本未正在进行的所有事务时阻止在行版本控制中的对象上。 该等待类型可确保行版本是之前执行的查询在快照隔离下可用。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DB_COMMAND |等待响应对话消息 （这需要在另一侧，使用 Always On 会话消息基础结构发出显式响应）。 许多不同的消息类型使用该等待类型。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DB_OP_COMPLETION_SYNC |等待响应对话消息 （这需要在另一侧，使用 Always On 会话消息基础结构发出显式响应）。 许多不同的消息类型使用该等待类型。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DB_OP_START_SYNC |Alwayson DDL 语句或 Windows Server 故障转移群集命令正在等待用于序列化访问的可用性数据库和其运行时状态。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DBR_SUBSCRIBER |可用性副本事件（例如，状态更改或配置更改）的发布服务器正在等待对与某一可用性数据库相对应的事件订阅服务器的运行时状态的独占读/写访问。 仅限内部使用。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DBR_SUBSCRIBER_FILTER_LIST |可用性副本事件（例如，状态更改或配置更改）的发布服务器正在等待对与可用性数据库相对应的事件订阅服务器的列表的独占读/写访问。 仅限内部使用。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DBSEEDING |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DBSEEDING_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DBSTATECHANGE_SYNC |并发控制等待的更新的内部状态的数据库副本。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FABRIC_CALLBACK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_BLOCK_FLUSH |FILESTREAM Always On 传输管理器正在等待完成的日志块的处理之前。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_FILE_CLOSE |FILESTREAM Always On 传输管理器正在等待直到下一步的 FILESTREAM 文件获取处理，并且其句柄获取关闭。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_FILE_REQUEST |始终在辅助副本正在等待主副本以使发送所有请求的 FILESTREAM 文件中撤消。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_IOMGR |FILESTREAM Always On 传输管理器正在等待在启动或关机过程中保护 FILESTREAM 始终在 I/O 管理器的 R/W 锁。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_IOMGR_IOCOMPLETION |FILESTREAM 始终在 I/O 管理器正在等待 I/O 完成。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_MANAGER |FILESTREAM Always On 传输管理器正在等待启动或关机期间保护 FILESTREAM Always On 传输管理器的 R/W 锁。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_PREPROC |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_GROUP_COMMIT |事务提交处理正在等待允许组提交，以便可将多个提交日志记录放置于单个日志块中。 此等待是一个预期的状况，它可优化日志 I/O、 捕获和发送操作。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_LOGCAPTURE_SYNC |在创建或销毁扫描时围绕日志捕获或应用对象的并发控制。 合作伙伴更改状态或连接状态时，这是预期的等待。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_LOGCAPTURE_WAIT |等待日志记录变得可用。 可在等待连接生成新的日志记录时或在读取未处于缓存中的记录时等待 I/O 完成时发生。 如果日志扫描到日志末尾赶上或者是从磁盘中的读取，这是预期的等待。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_LOGPROGRESS_SYNC |并发控制等待更新的数据库副本的日志进度状态时。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_NOTIFICATION_DEQUEUE |处理 Windows Server 故障转移群集通知的后台任务正在等待下一个通知。 仅限内部使用。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_NOTIFICATION_WORKER_EXCLUSIVE_ACCESS |Alwayson 可用性副本管理器正在等待对处理 Windows Server 故障转移群集通知的后台任务的运行时状态的序列化访问。 仅限内部使用。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_NOTIFICATION_WORKER_STARTUP_SYNC |后台任务正在等待处理 Windows Server 故障转移群集通知的后台任务完成启动。 仅限内部使用。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_NOTIFICATION_WORKER_TERMINATION_SYNC |后台任务正在等待处理 Windows Server 故障转移群集通知的后台任务终止。 仅限内部使用。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_PARTNER_SYNC |合作伙伴列表上的并发控制等待。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_READ_ALL_NETWORKS |等待获取对 WSFC 网络列表的读取或写入访问。 仅限内部使用。 请注意： 引擎在动态管理视图 （例如 sys.dm_hadr_cluster_networks) 中保留使用 WSFC 网络的列表，或若要验证始终在 TRANSACT-SQL 语句引用 WSFC 网络信息。 此列表将更新引擎启动时，WSFC 相关通知和内部 Always On 重新启动 （例如，丢失和以重新获取 WSFC 仲裁的）。 在该列表中的更新正在进行时，任务通常会被阻止。 、 <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_RECOVERY_WAIT_FOR_CONNECTION |正在等待辅助数据库在运行恢复之前连接到主数据库。 这是预期的等待，这会延长到主副本连接很慢建立。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_RECOVERY_WAIT_FOR_UNDO |数据库恢复正在等待辅助数据库完成恢复和初始化阶段以便恢复到主数据库的公共日志点。 在故障转移后，这是预期的等待。撤消可以通过 Windows 系统监视器 (perfmon.exe) 和动态管理视图中跟踪进度。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_REPLICAINFO_SYNC |等待并发控制，若要更新的当前副本状态。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_CANCELLATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_FILE_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_LIMIT_BACKUPS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_SYNC_COMPLETION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_TIMEOUT_TASK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_WAIT_FOR_COMPLETION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SYNC_COMMIT |正在等待针对同步辅助数据库的事务提交处理来强制写入日志。 事务延迟性能计数器也会反映这一等待。 该等待类型可用性组和指示发送、 写入和确认到辅助数据库的日志的时间应该的同步。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SYNCHRONIZING_THROTTLE |正在等待事务提交处理允许同步的辅助数据库几乎与日志的主结尾保持同步，以便转换到同步的状态。 这是预期的等待时辅助数据库追赶。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_TDS_LISTENER_SYNC |启动或停止侦听器，将请求内部 Always On 系统或 WSFC 群集。 对此请求的处理始终是异步的，并且存在删除冗余请求的机制。 还存在此进程由于配置更改而挂起的时刻。 与此侦听器同步机制相关的所有等待都使用此等待类型。 仅限内部使用。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_TDS_LISTENER_SYNC_PROCESSING |在需要启动和/或停止 anavailability 组侦听器始终在 TRANSACT-SQL 语句的末尾使用。 启动/停止操作以异步方式完成，因为用户线程将阻止使用该等待类型之前已知的侦听器的情况。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_THROTTLE_LOG_RATE_GOVERNOR |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_THROTTLE_LOG_RATE_LOG_SIZE |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|HADR_THROTTLE_LOG_RATE_SEEDING |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|HADR_THROTTLE_LOG_RATE_SEND_RECV_QUEUE_SIZE |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|HADR_TIMER_TASK |正在等待获取计时器任务对象上的锁，并且还可用于正在执行工作的时间之间的实际等待。 例如，任务运行一个执行示例后，每隔 10 秒 Alwayson 可用性组将等待大约 10 秒对要重新计划任务，并在等待此列出是为了。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_TRANSPORT_DBRLIST |正在等待访问传输层的数据库副本列表。 用于授予对其的访问旋转锁。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_TRANSPORT_FLOW_CONTROL |等待未完成未确认 Always On 消息的数量时通过扩展流控制阈值。 这是根据可用性副本之间 （不基于数据库到数据库）。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_TRANSPORT_SESSION |Alwayson 可用性组正在等待时更改或访问基础传输状态。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_WORK_POOL |Alwayson 可用性组后台工作任务对象上的并发控制等待。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_WORK_QUEUE |Alwayson 可用性组后台辅助线程等待新的工作分配。 等待新的工作，这是正常的状态的准备工作人员时，这是预期的等待。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_XRF_STACK_ACCESS |访问 （查找、 添加和删除） 的扩展的恢复分叉堆栈中的 Alwayson 可用性数据库。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HCCO_CACHE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HK_RESTORE_FILEMAP |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HKCS_PARALLEL_MIGRATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HKCS_PARALLEL_RECOVERY |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTBUILD |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTDELETE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTMEMO |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTREINIT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTREPARTITION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTTP_ENUMERATION |在启动时出现，以枚举 HTTP 端点以启动 HTTP。| 
|HTTP_START |当连接正在等待 HTTP 完成初始化时出现。| 
|HTTP_STORAGE_CONNECTION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|IMPPROV_IOWAIT |SQL Server 等待 bulkload I/O 完成时出现。| 
|INSTANCE_LOG_RATE_GOVERNOR |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|INTERNAL_TESTING |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|IO_AUDIT_MUTEX |在跟踪事件缓冲区同步期间出现。| 
|IO_COMPLETION |在等待 I/O 操作完成时出现。 通常，该等待类型表示非数据页 I/O。 数据页 I/O 完成等待显示为 PAGEIOLATCH\_ \*等待。| 
|IO_QUEUE_LIMIT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|IO_RETRY |当 I/O 操作（例如读取磁盘或写入磁盘）由于资源不足而失败，然后重试时出现。| 
|IOAFF_RANGE_QUEUE |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|KSOURCE_WAKEUP |在等待来自服务控制管理器的请求期间由服务控制任务使用。 可能会出现长时间等待，这并不指示出现问题。| 
|KTM_ENLISTMENT |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|KTM_RECOVERY_MANAGER |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|KTM_RECOVERY_RESOLUTION |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|LATCH_DT |等待 DT（破坏）闩锁时出现。 它不包括缓冲区闩锁或事务标记闩锁。 闩锁的列表\_\*等待位于 sys.dm_os_latch_stats。 请注意，sys.dm_os_latch_stats 将 LATCH_NL、LATCH_SH、LATCH_UP、LATCH_EX 以及 LATCH_DT 等待分到一组。| 
|LATCH_EX |等待 EX（排他）闩锁时出现。 它不包括缓冲区闩锁或事务标记闩锁。 闩锁的列表\_\*等待位于 sys.dm_os_latch_stats。 请注意，sys.dm_os_latch_stats 将 LATCH_NL、LATCH_SH、LATCH_UP、LATCH_EX 以及 LATCH_DT 等待分到一组。| 
|LATCH_KP |等待 KP（保持）闩锁时出现。 它不包括缓冲区闩锁或事务标记闩锁。 闩锁的列表\_\*等待位于 sys.dm_os_latch_stats。 请注意，sys.dm_os_latch_stats 将 LATCH_NL、LATCH_SH、LATCH_UP、LATCH_EX 以及 LATCH_DT 等待分到一组。| 
|LATCH_NL |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|LATCH_SH |等待 SH（共享）闩锁时出现。 它不包括缓冲区闩锁或事务标记闩锁。 闩锁的列表\_\*等待位于 sys.dm_os_latch_stats。 请注意，sys.dm_os_latch_stats 将 LATCH_NL、LATCH_SH、LATCH_UP、LATCH_EX 以及 LATCH_DT 等待分到一组。| 
|LATCH_UP |等待 UP（更新）闩锁时出现。 它不包括缓冲区闩锁或事务标记闩锁。 闩锁的列表\_\*等待位于 sys.dm_os_latch_stats。 请注意，sys.dm_os_latch_stats 将 LATCH_NL、LATCH_SH、LATCH_UP、LATCH_EX 以及 LATCH_DT 等待分到一组。| 
|LAZYWRITER_SLEEP |当惰性编写器被挂起时出现。 正在等待的后台任务所用时间的度量值。 在查找用户阻隔点所时不要考虑该状态。| 
|LCK_M_BU |当某任务正在等待获取大容量更新 (BU) 锁时出现。| 
|LCK_M_BU_ABORT_BLOCKERS |在任务等待获取使用中止阻塞程序的大容量更新 (BU) 锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_BU_LOW_PRIORITY |在任务等待获取低优先级的大容量更新 (BU) 锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IS |当某任务正在等待获取意向共享 (IS) 锁时出现。| 
|LCK_M_IS_ABORT_BLOCKERS |在任务等待获取使用中止阻塞程序的意向共享 (IS) 锁时出现。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IS_LOW_PRIORITY |在任务等待获取低优先级的意向共享 (IS) 锁时出现。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IU |当某任务正在等待获取意向更新 (IU) 锁时出现。| 
|LCK_M_IU_ABORT_BLOCKERS |在任务等待获取使用中止阻塞程序的意向更新 (IU) 锁时出现。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IU_LOW_PRIORITY |在任务等待获取低优先级的意向更新 (IU) 锁时出现。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IX |当某任务正在等待获取意向排他 (IX) 锁时出现。| 
|LCK_M_IX_ABORT_BLOCKERS |在任务等待获取使用中止阻塞程序的意向排他 (IX) 锁时出现。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IX_LOW_PRIORITY |在任务等待获取低优先级的意向排他 (IX) 锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_NL |当某任务正在等待获取当前键值上的 NULL 锁以及当前键和上一个键之间的插入范围锁时出现。 键上的 NULL 锁是指立即释放的锁。| 
|LCK_M_RIn_NL_ABORT_BLOCKERS |在任务等待获取当前键值上使用中止阻塞程序的 NULL 锁以及当前键和上一个键之间使用中止阻塞程序的插入范围锁时发生。 键上的 NULL 锁是指立即释放的锁。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_NL_LOW_PRIORITY |在任务等待获取当前键值上低优先级的 NULL 锁以及当前键和上一个键之间低优先级的插入范围锁时发生。 键上的 NULL 锁是指立即释放的锁。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_S |当某任务正在等待获取当前键值上的共享锁以及当前键和上一个键之间的插入范围锁时出现。| 
|LCK_M_RIn_S_ABORT_BLOCKERS |在任务等待获取当前键值上使用中止阻塞程序的共享锁以及当前键和上一个键之间使用中止阻塞程序的插入范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_S_LOW_PRIORITY |在任务等待获取当前键值上低优先级的共享锁以及当前键和上一个键之间低优先级的插入范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_U |任务正在等待获取当前键值上的更新锁以及当前键和上一个键之间的插入范围锁。| 
|LCK_M_RIn_U_ABORT_BLOCKERS |任务等待获取当前键值上使用中止阻塞程序的更新锁以及当前键和上一个键之间使用中止阻塞程序的插入范围锁。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_U_LOW_PRIORITY |任务等待获取当前键值上低优先级的更新锁以及当前键和上一个键之间低优先级的插入范围锁。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_X |当某任务正在等待获取当前键值上的排他锁以及当前键和上一个键之间的插入范围锁时出现。| 
|LCK_M_RIn_X_ABORT_BLOCKERS |在任务等待获取当前键值上使用中止阻塞程序的排他锁以及当前键和上一个键之间使用中止阻塞程序的插入范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_X_LOW_PRIORITY |在任务等待获取当前键值上低优先级的排他锁以及当前键和上一个键之间低优先级的插入范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RS_S |当某任务正在等待获取当前键值上的共享锁以及当前键和上一个键之间的共享范围锁时出现。| 
|LCK_M_RS_S_ABORT_BLOCKERS |在任务等待获取当前键值上使用中止阻塞程序的共享锁以及当前键和上一个键之间使用中止阻塞程序的共享范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RS_S_LOW_PRIORITY |在任务等待获取当前键值上低优先级的共享锁以及当前键和上一个键之间低优先级的共享范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RS_U |当某任务正在等待获取当前键值上的更新锁以及当前键和上一个键之间的更新范围锁时出现。| 
|LCK_M_RS_U_ABORT_BLOCKERS |在任务等待获取当前键值上使用中止阻塞程序的更新锁以及当前键和上一个键之间使用中止阻塞程序的更新范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RS_U_LOW_PRIORITY |在任务等待获取当前键值上低优先级的更新锁以及当前键和上一个键之间低优先级的更新范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_S |当某任务正在等待获取当前键值上的共享锁以及当前键和上一个键之间的排他范围锁时出现。| 
|LCK_M_RX_S_ABORT_BLOCKERS |在任务等待获取当前键值上使用中止阻塞程序的共享锁以及当前键和上一个键之间使用中止阻塞程序的排他范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_S_LOW_PRIORITY |在任务等待获取当前键值上低优先级的共享锁以及当前键和上一个键之间低优先级的排他范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_U |当某任务正在等待获取当前键值上的更新锁以及当前键和上一个键之间的排他范围锁时出现。| 
|LCK_M_RX_U_ABORT_BLOCKERS |在任务等待获取当前键值上使用中止阻塞程序的更新锁以及当前键和上一个键之间使用中止阻塞程序的排他范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_U_LOW_PRIORITY |在任务等待获取当前键值上低优先级的更新锁以及当前键和上一个键之间低优先级的排他范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_X |当某任务正在等待获取当前键值上的排他锁以及当前键和上一个键之间的排他范围锁时出现。| 
|LCK_M_RX_X_ABORT_BLOCKERS |在任务等待获取当前键值上使用中止阻塞程序的排他锁以及当前键和上一个键之间使用中止阻塞程序的排他范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_X_LOW_PRIORITY |在任务等待获取当前键值上低优先级的排他锁以及当前键和上一个键之间低优先级的排他范围锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_S |当某任务正在等待获取共享锁时出现。| 
|LCK_M_S_ABORT_BLOCKERS |在任务等待获取使用中止阻塞程序的共享锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_S_LOW_PRIORITY |在任务等待获取低优先级的共享锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SCH_M |当某任务正在等待获取架构修改锁时出现。| 
|LCK_M_SCH_M_ABORT_BLOCKERS |在任务等待获取使用中止阻塞程序的架构修改锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SCH_M_LOW_PRIORITY |在任务等待获取低优先级的架构修改锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SCH_S |当某任务正在等待获取架构共享锁时出现。| 
|LCK_M_SCH_S_ABORT_BLOCKERS |在任务等待获取使用中止阻塞程序的架构共享锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SCH_S_LOW_PRIORITY |在任务等待获取低优先级的架构共享锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SIU |当某任务正在等待获取共享意向更新锁时出现。| 
|LCK_M_SIU_ABORT_BLOCKERS |在任务等待获取具有中止阻塞程序的共享意向更新锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SIU_LOW_PRIORITY |在任务等待获取低优先级的共享意向更新锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SIX |当某任务正在等待获取共享意向排他锁时出现。| 
|LCK_M_SIX_ABORT_BLOCKERS |在任务等待获取使用中止阻塞程序的共享意向排他锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SIX_LOW_PRIORITY |在任务等待获取低优先级的意向排他共享锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_U |当某任务正在等待获取更新锁时出现。| 
|LCK_M_U_ABORT_BLOCKERS |在任务等待获取使用中止阻塞程序的更新锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_U_LOW_PRIORITY |在任务等待获取低优先级的更新锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_UIX |当某任务正在等待获取更新意向排他锁时出现。| 
|LCK_M_UIX_ABORT_BLOCKERS |在任务等待获取使用中止阻塞程序的意向排他更新锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_UIX_LOW_PRIORITY |在任务等待获取低优先级的意向排他更新锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_X |当某任务正在等待获取排他锁时出现。| 
|LCK_M_X_ABORT_BLOCKERS |在任务等待获取使用中止阻塞程序的排他锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_X_LOW_PRIORITY |在任务等待获取低优先级的排他锁时发生。 （有关的低优先级服务等待选项的 ALTER TABLE 和 ALTER INDEX。）， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOG_POOL_SCAN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOG_RATE_GOVERNOR |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGBUFFER |当某任务正在等待日志缓冲区的空间以存储日志记录时出现。 连续的高值可能指示日志设备无法跟上服务器生成的日志量。| 
|LOGCAPTURE_LOGPOOLTRUNCPOINT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGGENERATION |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|LOGMGR |在数据库关闭过程中，当某任务正在等待任何未完成的日志 I/O 在关闭日志之前完成时出现。| 
|LOGMGR_FLUSH |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|LOGMGR_PMM_LOG |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGMGR_QUEUE |在日志编写器任务等待工作请求时出现。| 
|LOGMGR_RESERVE_APPEND |当某任务正在等待查看日志截断是否能释放日志空间以使该任务能写入新的日志记录时出现。 请考虑为受影响的数据库增加日志文件的大小以减少该等待时间。| 
|LOGPOOL_CACHESIZE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOL_CONSUMER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOL_CONSUMERSET |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOL_FREEPOOLS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOL_MGRSET |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOL_REPLACEMENTSET |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOLREFCOUNTEDOBJECT_REFDONE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOWFAIL_MEMMGR_QUEUE |在等待可用内存期间出现。| 
|MD_AGENT_YIELD |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|MD_LAZYCACHE_RWLOCK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|MEMORY_ALLOCATION_EXT |从内部 SQL Server 内存池或操作系统分配内存时出现。， <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|MEMORY_GRANT_UPDATE |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|METADATA_LAZYCACHE_RWLOCK |TBD <br /> **适用于**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]仅。 |  
|MIGRATIONBUFFER |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|MISCELLANEOUS |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|MISCELLANEOUS |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|MSQL_DQ |当某任务正在等待分布式查询操作完成时出现。 它用于检测潜在的多个活动的结果集 (MARS) 应用程序死锁。 该等待将在分布式查询调用完成时结束。| 
|MSQL_XACT_MGR_MUTEX |当某任务正在等待获取会话事务管理器的所有权以执行会话级别事务操作时出现。| 
|MSQL_XACT_MUTEX |在事务使用同步期间出现。 请求必须先获取互斥体才可以使用事务。| 
|MSQL_XP |当某任务正在等待扩展存储过程结束时出现。 SQL Server 使用该等待状态检测潜在的 MARS 应用程序死锁。 该等待将在扩展存储过程调用结束时停止。| 
|MSSEARCH |在全文搜索调用期间出现。 该等待在全文操作完成时结束。 它不指示争用，而指示全文操作的持续时间。| 
|NET_WAITFOR_PACKET |在网络读取过程中连接正在等待网络数据包时出现。| 
|NETWORKSXMLMGRLOAD |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|NODE_CACHE_MUTEX |TBD| 
|OLEDB |SQL Server 调用 SQL Server Native Client OLE DB 访问接口时发生。 该等待类型不用于同步。 而是用于指示调用 OLE DB 访问接口的持续时间。| 
|ONDEMAND_TASK_QUEUE |在后台任务等待高优先级系统任务请求时出现。 长时间的等待指示一直没有要处理的高优先级请求，不应引起关注。| 
|PAGEIOLATCH_DT |在任务等待 I/O 请求中缓冲区的闩锁时发生。 闩锁请求处于“破坏”模式。 长时间的等待可能指示磁盘子系统出现问题。| 
|PAGEIOLATCH_EX |在任务等待 I/O 请求中缓冲区的闩锁时发生。 闩锁请求处于“独占”模式。 长时间的等待可能指示磁盘子系统出现问题。| 
|PAGEIOLATCH_KP |在任务等待 I/O 请求中缓冲区的闩锁时发生。 闩锁请求处于“保持”模式。 长时间的等待可能指示磁盘子系统出现问题。| 
|PAGEIOLATCH_NL |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|PAGEIOLATCH_SH |在任务等待 I/O 请求中缓冲区的闩锁时发生。 闩锁请求处于“共享”模式。 长时间的等待可能指示磁盘子系统出现问题。| 
|PAGEIOLATCH_UP |在任务等待 I/O 请求中缓冲区的闩锁时发生。 闩锁请求处于“更新”模式。 长时间的等待可能指示磁盘子系统出现问题。| 
|PAGELATCH_DT |在任务等待不处于 I/O 请求中的缓冲区闩锁时发生。 闩锁请求处于“破坏”模式。| 
|PAGELATCH_EX |在任务等待不处于 I/O 请求中的缓冲区闩锁时发生。 闩锁请求处于“独占”模式。| 
|PAGELATCH_KP |在任务等待不处于 I/O 请求中的缓冲区闩锁时发生。 闩锁请求处于“保持”模式。| 
|PAGELATCH_NL |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|PAGELATCH_SH |在任务等待不处于 I/O 请求中的缓冲区闩锁时发生。 闩锁请求处于“共享”模式。| 
|PAGELATCH_UP |在任务等待不处于 I/O 请求中的缓冲区闩锁时发生。 闩锁请求处于“更新”模式。| 
|PARALLEL_BACKUP_QUEUE |在序列化由 RESTORE HEADERONLY、RESTORE FILELISTONLY 或 RESTORE LABELONLY 生成的输出时出现。| 
|PARALLEL_REDO_DRAIN_WORKER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_FLOW_CONTROL |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_LOG_CACHE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_TRAN_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_TRAN_TURN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_WORKER_SYNC |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_WORKER_WAIT_WORK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PERFORMANCE_COUNTERS_RWLOCK |TBD| 
|PHYSICAL_SEEDING_DMV |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|POOL_LOG_RATE_GOVERNOR |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_ABR |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG |在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 操作系统 (SQLOS) 计划程序切换到抢先模式时发生，以便将审核事件写入 Windows 事件日志。 <br /> **适用于**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]仅。 |  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG |在 SQLOS 计划程序切换到抢先模式时发生，以便将审核事件写入 Windows 安全日志。 <br /> **适用于**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]仅。 |  
|PREEMPTIVE_CLOSEBACKUPMEDIA |在 SQLOS 计划程序切换到抢先模式时发生，以便关闭备份介质。| 
|PREEMPTIVE_CLOSEBACKUPTAPE |在 SQLOS 计划程序切换到抢先模式时发生，以便关闭磁带备份设备。| 
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE |在 SQLOS 计划程序切换到抢先模式时发生，以便关闭虚拟备份设备。| 
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL |在 SQLOS 计划程序切换到抢先模式时发生，以便执行故障转移群集操作。| 
|PREEMPTIVE_COM_COCREATEINSTANCE |在 SQLOS 计划程序切换到抢先模式时发生，以便创建 COM 对象。| 
|PREEMPTIVE_COM_COGETCLASSOBJECT |TBD| 
|PREEMPTIVE_COM_CREATEACCESSOR |TBD| 
|PREEMPTIVE_COM_DELETEROWS |TBD| 
|PREEMPTIVE_COM_GETCOMMANDTEXT |TBD| 
|PREEMPTIVE_COM_GETDATA |TBD| 
|PREEMPTIVE_COM_GETNEXTROWS |TBD| 
|PREEMPTIVE_COM_GETRESULT |TBD| 
|PREEMPTIVE_COM_GETROWSBYBOOKMARK |TBD| 
|PREEMPTIVE_COM_LBFLUSH |TBD| 
|PREEMPTIVE_COM_LBLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBREADAT |TBD| 
|PREEMPTIVE_COM_LBSETSIZE |TBD| 
|PREEMPTIVE_COM_LBSTAT |TBD| 
|PREEMPTIVE_COM_LBUNLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBWRITEAT |TBD| 
|PREEMPTIVE_COM_QUERYINTERFACE |TBD| 
|PREEMPTIVE_COM_RELEASE |TBD| 
|PREEMPTIVE_COM_RELEASEACCESSOR |TBD| 
|PREEMPTIVE_COM_RELEASEROWS |TBD| 
|PREEMPTIVE_COM_RELEASESESSION |TBD| 
|PREEMPTIVE_COM_RESTARTPOSITION |TBD| 
|PREEMPTIVE_COM_SEQSTRMREAD |TBD| 
|PREEMPTIVE_COM_SEQSTRMREADANDWRITE |TBD| 
|PREEMPTIVE_COM_SETDATAFAILURE |TBD| 
|PREEMPTIVE_COM_SETPARAMETERINFO |TBD| 
|PREEMPTIVE_COM_SETPARAMETERPROPERTIES |TBD| 
|PREEMPTIVE_COM_STRMLOCKREGION |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDREAD |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDWRITE |TBD| 
|PREEMPTIVE_COM_STRMSETSIZE |TBD| 
|PREEMPTIVE_COM_STRMSTAT |TBD| 
|PREEMPTIVE_COM_STRMUNLOCKREGION |TBD| 
|PREEMPTIVE_CONSOLEWRITE |TBD| 
|PREEMPTIVE_CREATEPARAM |TBD| 
|PREEMPTIVE_DEBUG |TBD| 
|PREEMPTIVE_DFSADDLINK |TBD| 
|PREEMPTIVE_DFSLINKEXISTCHECK |TBD| 
|PREEMPTIVE_DFSLINKHEALTHCHECK |TBD| 
|PREEMPTIVE_DFSREMOVELINK |TBD| 
|PREEMPTIVE_DFSREMOVEROOT |TBD| 
|PREEMPTIVE_DFSROOTFOLDERCHECK |TBD| 
|PREEMPTIVE_DFSROOTINIT |TBD| 
|PREEMPTIVE_DFSROOTSHARECHECK |TBD| 
|PREEMPTIVE_DTC_ABORT |TBD| 
|PREEMPTIVE_DTC_ABORTREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_BEGINTRANSACTION |TBD| 
|PREEMPTIVE_DTC_COMMITREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_ENLIST |TBD| 
|PREEMPTIVE_DTC_PREPAREREQUESTDONE |TBD| 
|PREEMPTIVE_FILESIZEGET |TBD| 
|PREEMPTIVE_FSAOLEDB_ABORTTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_COMMITTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_STARTTRANSACTION |TBD| 
|PREEMPTIVE_FSRECOVER_UNCONDITIONALUNDO |TBD| 
|PREEMPTIVE_GETRMINFO |TBD| 
|PREEMPTIVE_HADR_LEASE_MECHANISM |针对 CSS 诊断的 alwayson 可用性组租用管理器。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_HTTP_EVENT_WAIT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_HTTP_REQUEST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_LOCKMONITOR |TBD| 
|PREEMPTIVE_MSS_RELEASE |TBD| 
|PREEMPTIVE_ODBCOPS |TBD| 
|PREEMPTIVE_OLE_UNINIT |TBD| 
|PREEMPTIVE_OLEDB_ABORTORCOMMITTRAN |TBD| 
|PREEMPTIVE_OLEDB_ABORTTRAN |TBD| 
|PREEMPTIVE_OLEDB_GETDATASOURCE |TBD| 
|PREEMPTIVE_OLEDB_GETLITERALINFO |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTYINFO |TBD| 
|PREEMPTIVE_OLEDB_GETSCHEMALOCK |TBD| 
|PREEMPTIVE_OLEDB_JOINTRANSACTION |TBD| 
|PREEMPTIVE_OLEDB_RELEASE |TBD| 
|PREEMPTIVE_OLEDB_SETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDBOPS |TBD| 
|PREEMPTIVE_OS_ACCEPTSECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_ACQUIRECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_AUTHENTICATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHORIZATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHZGETINFORMATIONFROMCONTEXT |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZECONTEXTFROMSID |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZERESOURCEMANAGER |TBD| 
|PREEMPTIVE_OS_BACKUPREAD |TBD| 
|PREEMPTIVE_OS_CLOSEHANDLE |TBD| 
|PREEMPTIVE_OS_CLUSTEROPS |TBD| 
|PREEMPTIVE_OS_COMOPS |TBD| 
|PREEMPTIVE_OS_COMPLETEAUTHTOKEN |TBD| 
|PREEMPTIVE_OS_COPYFILE |TBD| 
|PREEMPTIVE_OS_CREATEDIRECTORY |TBD| 
|PREEMPTIVE_OS_CREATEFILE |TBD| 
|PREEMPTIVE_OS_CRYPTACQUIRECONTEXT |TBD| 
|PREEMPTIVE_OS_CRYPTIMPORTKEY |TBD| 
|PREEMPTIVE_OS_CRYPTOPS |TBD| 
|PREEMPTIVE_OS_DECRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_DELETEFILE |TBD| 
|PREEMPTIVE_OS_DELETESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_DEVICEIOCONTROL |TBD| 
|PREEMPTIVE_OS_DEVICEOPS |TBD| 
|PREEMPTIVE_OS_DIRSVC_NETWORKOPS |TBD| 
|PREEMPTIVE_OS_DISCONNECTNAMEDPIPE |TBD| 
|PREEMPTIVE_OS_DOMAINSERVICESOPS |TBD| 
|PREEMPTIVE_OS_DSGETDCNAME |TBD| 
|PREEMPTIVE_OS_DTCOPS |TBD| 
|PREEMPTIVE_OS_ENCRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_FILEOPS |TBD| 
|PREEMPTIVE_OS_FINDFILE |TBD| 
|PREEMPTIVE_OS_FLUSHFILEBUFFERS |TBD| 
|PREEMPTIVE_OS_FORMATMESSAGE |TBD| 
|PREEMPTIVE_OS_FREECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_FREELIBRARY |TBD| 
|PREEMPTIVE_OS_GENERICOPS |TBD| 
|PREEMPTIVE_OS_GETADDRINFO |TBD| 
|PREEMPTIVE_OS_GETCOMPRESSEDFILESIZE |TBD| 
|PREEMPTIVE_OS_GETDISKFREESPACE |TBD| 
|PREEMPTIVE_OS_GETFILEATTRIBUTES |TBD| 
|PREEMPTIVE_OS_GETFILESIZE |TBD| 
|PREEMPTIVE_OS_GETFINALFILEPATHBYHANDLE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_OS_GETLONGPATHNAME |TBD| 
|PREEMPTIVE_OS_GETPROCADDRESS |TBD| 
|PREEMPTIVE_OS_GETVOLUMENAMEFORVOLUMEMOUNTPOINT |TBD| 
|PREEMPTIVE_OS_GETVOLUMEPATHNAME |TBD| 
|PREEMPTIVE_OS_INITIALIZESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_LIBRARYOPS |TBD| 
|PREEMPTIVE_OS_LOADLIBRARY |TBD| 
|PREEMPTIVE_OS_LOGONUSER |TBD| 
|PREEMPTIVE_OS_LOOKUPACCOUNTSID |TBD| 
|PREEMPTIVE_OS_MESSAGEQUEUEOPS |TBD| 
|PREEMPTIVE_OS_MOVEFILE |TBD| 
|PREEMPTIVE_OS_NETGROUPGETUSERS |TBD| 
|PREEMPTIVE_OS_NETLOCALGROUPGETMEMBERS |TBD| 
|PREEMPTIVE_OS_NETUSERGETGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERGETLOCALGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERMODALSGET |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICY |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICYFREE |TBD| 
|PREEMPTIVE_OS_OPENDIRECTORY |TBD| 
|PREEMPTIVE_OS_PDH_WMI_INIT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_OS_PIPEOPS |TBD| 
|PREEMPTIVE_OS_PROCESSOPS |TBD| 
|PREEMPTIVE_OS_QUERYCONTEXTATTRIBUTES |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_OS_QUERYREGISTRY |TBD| 
|PREEMPTIVE_OS_QUERYSECURITYCONTEXTTOKEN |TBD| 
|PREEMPTIVE_OS_REMOVEDIRECTORY |TBD| 
|PREEMPTIVE_OS_REPORTEVENT |TBD| 
|PREEMPTIVE_OS_REVERTTOSELF |TBD| 
|PREEMPTIVE_OS_RSFXDEVICEOPS |TBD| 
|PREEMPTIVE_OS_SECURITYOPS |TBD| 
|PREEMPTIVE_OS_SERVICEOPS |TBD| 
|PREEMPTIVE_OS_SETENDOFFILE |TBD| 
|PREEMPTIVE_OS_SETFILEPOINTER |TBD| 
|PREEMPTIVE_OS_SETFILEVALIDDATA |TBD| 
|PREEMPTIVE_OS_SETNAMEDSECURITYINFO |TBD| 
|PREEMPTIVE_OS_SQLCLROPS |TBD| 
|PREEMPTIVE_OS_SQMLAUNCH |TBD <br /> **适用范围**： [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 到 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]。 |  
|PREEMPTIVE_OS_VERIFYSIGNATURE |TBD| 
|PREEMPTIVE_OS_VERIFYTRUST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_OS_VSSOPS |TBD| 
|PREEMPTIVE_OS_WAITFORSINGLEOBJECT |TBD| 
|PREEMPTIVE_OS_WINSOCKOPS |TBD| 
|PREEMPTIVE_OS_WRITEFILE |TBD| 
|PREEMPTIVE_OS_WRITEFILEGATHER |TBD| 
|PREEMPTIVE_OS_WSASETLASTERROR |TBD| 
|PREEMPTIVE_REENLIST |TBD| 
|PREEMPTIVE_RESIZELOG |TBD| 
|PREEMPTIVE_ROLLFORWARDREDO |TBD| 
|PREEMPTIVE_ROLLFORWARDUNDO |TBD| 
|PREEMPTIVE_SB_STOPENDPOINT |TBD| 
|PREEMPTIVE_SERVER_STARTUP |TBD| 
|PREEMPTIVE_SETRMINFO |TBD| 
|PREEMPTIVE_SHAREDMEM_GETDATA |TBD| 
|PREEMPTIVE_SNIOPEN |TBD| 
|PREEMPTIVE_SOSHOST |TBD| 
|PREEMPTIVE_SOSTESTING |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|PREEMPTIVE_SP_SERVER_DIAGNOSTICS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_STARTRM |TBD| 
|PREEMPTIVE_STREAMFCB_CHECKPOINT |TBD| 
|PREEMPTIVE_STREAMFCB_RECOVER |TBD| 
|PREEMPTIVE_STRESSDRIVER |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|PREEMPTIVE_TESTING |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|PREEMPTIVE_TRANSIMPORT |TBD| 
|PREEMPTIVE_UNMARSHALPROPAGATIONTOKEN |TBD| 
|PREEMPTIVE_VSS_CREATESNAPSHOT |TBD| 
|PREEMPTIVE_VSS_CREATEVOLUMESNAPSHOT |TBD| 
|PREEMPTIVE_XE_CALLBACKEXECUTE |TBD| 
|PREEMPTIVE_XE_CX_FILE_OPEN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_XE_CX_HTTP_CALL |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_XE_DISPATCHER |TBD| 
|PREEMPTIVE_XE_ENGINEINIT |TBD| 
|PREEMPTIVE_XE_GETTARGETSTATE |TBD| 
|PREEMPTIVE_XE_SESSIONCOMMIT |TBD| 
|PREEMPTIVE_XE_TARGETFINALIZE |TBD| 
|PREEMPTIVE_XE_TARGETINIT |TBD| 
|PREEMPTIVE_XE_TIMERRUN |TBD| 
|PREEMPTIVE_XETESTING |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|PRINT_ROLLBACK_PROGRESS |用于等待用户进程在已通过 ALTER DATABASE 终止子句完成转换的数据库中结束。 有关详细信息，请参阅 ALTER DATABASE (Transact SQL)。| 
|PRU_ROLLBACK_DEFERRED |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_ALL_COMPONENTS_INITIALIZED |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_COOP_SCAN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_DIRECTLOGCONSUMER_GETNEXT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_EVENT_SESSION_INIT_MUTEX |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_FABRIC_REPLICA_CONTROLLER_DATA_LOSS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_ACTION_COMPLETED |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC |当后台任务等待终止接收 （通过轮询） 的后台任务时出现 Windows Server 故障转移群集通知。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_CLUSTER_INTEGRATION |追加、 替换和/或删除操作正在等待获取 Alwayson 内部列表 （例如网络、 网络地址或可用性组侦听器的列表） 上的写入锁。 仅限，内部使用 <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_FAILOVER_COMPLETED |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_JOIN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_OFFLINE_COMPLETED |Alwayson 删除可用性组操作正在等待目标可用性组在销毁 Windows Server 故障转移群集对象之前进入脱机状态。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_ONLINE_COMPLETED |Alwayson 创建或故障转移可用性组操作正在等待目标可用性组联机。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_POST_ONLINE_COMPLETED |Alwayson 删除可用性组操作正在等待作为之前命令的一部分计划任何后台任务的终止。 例如，可能有正在将可用性数据库转换为主要角色的后台任务。 DROP AVAILABILITY GROUP DDL 必须等待此后台任务终止，以免争用条件。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_SERVER_READY_CONNECTIONS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_WORKITEM_COMPLETED |正在等待异步工作任务完成，这是线程执行的内部等待。 这是预期的等待，则使用 CSS。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADRSIM |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_LOG_CONSOLIDATION_IO |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_LOG_CONSOLIDATION_POLL |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_MD_LOGIN_STATS |在登录统计信息的元数据内部同步期间出现。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_MD_RELATION_CACHE |在表或索引的元数据内部同步期间出现。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_MD_SERVER_CACHE |在链接服务器的元数据内部同步期间出现。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_MD_UPGRADE_CONFIG |升级服务器范围的配置中的内部同步期间出现。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_PREEMPTIVE_APP_USAGE_TIMER |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|PWAIT_PREEMPTIVE_AUDIT_ACCESS_WINDOWSLOG |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_QRY_BPMEMORY |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_REPLICA_ONLINE_INIT_MUTEX |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_SBS_FILE_OPERATION |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|PWAIT_XTP_FSSTORAGE_MAINTENANCE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_XTP_HOST_STORAGE_WAIT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_ASYNC_CHECK_CONSISTENCY_TASK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_ASYNC_PERSIST_TASK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_ASYNC_PERSIST_TASK_START |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_ASYNC_QUEUE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_BCKG_TASK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_BLOOM_FILTER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_CLEANUP_STALE_QUERIES_TASK_MAIN_LOOP_SLEEP |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_CTXS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_DB_DISK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_DYN_VECTOR |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_EXCLUSIVE_ACCESS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_HOST_INIT |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|QDS_LOADDB |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_PERSIST_TASK_MAIN_LOOP_SLEEP |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_QDS_CAPTURE_INIT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_SHUTDOWN_QUEUE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_STMT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_STMT_DISK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_TASK_SHUTDOWN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_TASK_START |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QE_WARN_LIST_SYNC |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QPJOB_KILL |指示异步统计信息自动更新在开始运行时通过调用 KILL 命令而取消。 终止线程处于挂起状态，等待它开始侦听 KILL 命令。 正常情况下，该值不到一秒钟。| 
|QPJOB_WAITFOR_ABORT |指示异步统计信息自动更新在运行时通过调用 KILL 命令而取消。 目前更新已完成，但是在终止线程消息协调完成之前一直于挂起状态。 这是一个普通而少见的状态，应当非常短暂。 正常情况下，该值不到一秒钟。| 
|QRY_MEM_GRANT_INFO_MUTEX |当查询执行内存管理尝试控制对静态授予信息列表的访问时出现。 该状态列出当前已批准的内存请求以及正在等待的内存请求的有关信息。 该状态是一个简单的访问控制状态。 该状态始终不应当等待较长的时间。 如果未释放互斥体，则所有占用内存的新查询都将停止响应。| 
|QRY_PARALLEL_THREAD_MUTEX |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QRY_PROFILE_LIST_MUTEX |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QUERY_ERRHDL_SERVICE_DONE |标识为仅供参考。 不提供支持。 <br /> **适用于**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]仅。 |  
|QUERY_WAIT_ERRHDL_SERVICE |标识为仅供参考。  不提供支持。 <br /> **适用于**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]仅。  |  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN |当脱机创建索引生成以并行方式运行，并且正在排序的不同工作线程同步访问排序文件时出现。| 
|QUERY_NOTIFICATION_MGR_MUTEX |在查询通知管理器中的垃圾收集队列同步期间出现。| 
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX |在查询通知中事务的状态同步期间出现。| 
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX |在查询通知管理器中的内部同步期间出现。| 
|QUERY_NOTIFICATION_UNITTEST_MUTEX |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|QUERY_OPTIMIZER_PRINT_MUTEX |在查询优化器诊断信息输出生成的同步期间出现。 该等待类型时才会出现下的 Microsoft 产品支持的方向启用了诊断设置。| 
|QUERY_TASK_ENQUEUE_MUTEX |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QUERY_TRACEOUT |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|RBIO_WAIT_VLF |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|RECOVER_CHANGEDB |在备用数据库中同步数据库状态期间出现。| 
|RECOVERY_MGR_LOCK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REDO_THREAD_PENDING_WORK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REDO_THREAD_SYNC |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REMOTE_BLOCK_IO |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|REMOTE_DATA_ARCHIVE_MIGRATION_DMV |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REMOTE_DATA_ARCHIVE_SCHEMA_DMV |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REMOTE_DATA_ARCHIVE_SCHEMA_TASK_QUEUE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REPL_CACHE_ACCESS |在同步复制项目缓存的期间出现。 在这些等待期间，复制日志读取器将停止，已发布表中的数据定义语言 (DDL) 语句也将被阻止。| 
|REPL_HISTORYCACHE_ACCESS |TBD| 
|REPL_SCHEMA_ACCESS |在同步复制架构版本信息的期间出现。 该状态在下列情况下存在：针对复制对象执行 DDL 语句时，以及日志读取器根据 DDL 出现次数生成或使用版本控制架构时。| 
|REPL_TRANFSINFO_ACCESS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REPL_TRANHASHTABLE_ACCESS |TBD| 
|REPL_TRANTEXTINFO_ACCESS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REPLICA_WRITES |在任务等待将页写入数据库快照或 DBCC 副本的操作完成时出现。| 
|REQUEST_DISPENSER_PAUSE |在任务等待所有未完成的 I/O 完成时出现，以便可以为快照备份冻结文件的 I/O。| 
|REQUEST_FOR_DEADLOCK_SEARCH |在死锁监视器等待开始下一次死锁搜索时出现。 在两次死锁检测之间可能出现该等待，长时间等待此资源并不指示出现问题。| 
|RESERVED_MEMORY_ALLOCATION_EXT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|RESMGR_THROTTLED |在有新请求传入并且基于 GROUP_MAX_REQUESTS 设置而中止时出现。| 
|RESOURCE_GOVERNOR_IDLE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|RESOURCE_QUEUE |在同步不同的内部资源队列期间出现。| 
|RESOURCE_SEMAPHORE |当由于存在其他并发查询而无法立即批准查询内存请求时出现。 等待时间较长或等待次数较多可能指示并发查询的数量过多或内存请求的数量过多。| 
|RESOURCE_SEMAPHORE_MUTEX |在查询等待其保留线程的请求完成时出现。 它也在同步查询编译和内存授予请求时出现。| 
|RESOURCE_SEMAPHORE_QUERY_COMPILE |在并发查询编译的数量达到中止限制时出现。 等待时间较长或等待次数较多可能指示编译、重新编辑或不可缓存的计划过多。| 
|RESOURCE_SEMAPHORE_SMALL_QUERY |当由于存在其他并发查询而无法立即批准较小查询的内存请求时出现。 等待时间不应超过几秒钟，因为如果服务器无法在几秒钟内给予请求的内存，则会将请求传输到主查询内存池中。 等待时间较长可能指示当主内存池被等待的查询阻塞时并发小查询的数量过多。 <br /> **适用于**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]仅。 |  
|RESTORE_FILEHANDLECACHE_ENTRYLOCK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|RESTORE_FILEHANDLECACHE_LOCK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|RG_RECONFIG |TBD| 
|ROWGROUP_OP_STATS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ROWGROUP_VERSION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|RTDATA_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SATELLITE_CARGO |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SATELLITE_SERVICE_SETUP |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SATELLITE_TASK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SBS_DISPATCH |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|SBS_RECEIVE_TRANSPORT |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|SBS_TRANSPORT |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|SCAN_CHAR_HASH_ARRAY_INITIALIZATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SEC_DROP_TEMP_KEY |在尝试删除临时安全密钥失败之后并在重试之前出现。| 
|SECURITY_CNG_PROVIDER_MUTEX |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|SECURITY_CRYPTO_CONTEXT_MUTEX |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SECURITY_DBE_STATE_MUTEX |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SECURITY_KEYRING_RWLOCK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SECURITY_MUTEX |当等待互斥体时出现，这些互斥体控制对可扩展的密钥管理 (EKM) 加密提供程序的全局列表以及 EKM 会话的会话作用域列表的访问。| 
|SECURITY_RULETABLE_MUTEX |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SEMPLAT_DSI_BUILD |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SEQUENCE_GENERATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SEQUENTIAL_GUID |当正在获取新的连续 GUID 时出现。| 
|SERVER_IDLE_CHECK |当资源监视器尝试声明为空闲的 SQL Server 实例或尝试唤醒时，SQL Server 实例的空闲状态的同步期间出现。| 
|SERVER_RECONFIGURE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SESSION_WAIT_STATS_CHILDREN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SHARED_DELTASTORE_CREATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SHUTDOWN |在关闭语句等待活动连接退出时出现。| 
|SLEEP_BPOOL_FLUSH |当检查点为了避免磁盘子系统泛滥而中止新 I/O 的发布时出现。| 
|SLEEP_BUFFERPOOL_HELPLW |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_DBSTARTUP |在等待所有数据库恢复时数据库的启动期间出现。| 
|SLEEP_DCOMSTARTUP |在等待 DCOM 初始化完成时的 SQL Server 实例启动过程中最多出现一次。| 
|SLEEP_MASTERDBREADY |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_MASTERMDREADY |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_MASTERUPGRADED |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_MEMORYPOOL_ALLOCATEPAGES |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_MSDBSTARTUP |在 SQL 跟踪等待 msdb 数据库完成启动时出现。| 
|SLEEP_RETRY_VIRTUALALLOC |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_SYSTEMTASK |在等待 tempdb 完成启动时后台任务的启动期间出现。| 
|SLEEP_TASK |当任务在等待一般事件出现期间睡眠时出现。| 
|SLEEP_TEMPDBSTARTUP |在任务等待 tempdb 完成启动时出现。| 
|SLEEP_WORKSPACE_ALLOCATEPAGE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLO_UPDATE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SMSYNC |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SNI_CONN_DUP |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SNI_CRITICAL_SECTION |在 SQL Server 网络组件内的内部同步期间出现。| 
|SNI_HTTP_WAITFOR_0_DISCON |在 SQL Server 关闭，等待未完成 HTTP 连接退出时期间发生。| 
|SNI_LISTENER_ACCESS |当等待非一致性内存访问 (NUMA) 节点更新状态更改时出现。 已序列化对状态更改的访问。| 
|SNI_TASK_COMPLETION |当在 NUMA 节点状态更改期间等待所有任务完成时出现。| 
|SNI_WRITE_ASYNC |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|SOAP_READ |在等待 HTTP 网络读取完成时出现。| 
|SOAP_WRITE |在等待 HTTP 网络写入完成时出现。| 
|SOCKETDUPLICATEQUEUE_CLEANUP |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SOS_CALLBACK_REMOVAL |在为了删除回调而对回调列表执行同步期间出现。 服务器初始化完成之后，此计数器可能不会更改。| 
|SOS_DISPATCHER_MUTEX |在调度程序池进行内部同步期间出现。 包括调整该池时。| 
|SOS_LOCALALLOCATORLIST |在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 内存管理器中进行内部同步期间出现。 <br /> **适用于**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]仅。 |  
|SOS_MEMORY_TOPLEVELBLOCKALLOCATOR |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SOS_MEMORY_USAGE_ADJUSTMENT |在池之间调整内存使用情况时出现。| 
|SOS_OBJECT_STORE_DESTROY_MUTEX |当破坏池中的对象时在内存池中进行内部同步期间出现。| 
|SOS_PHYS_PAGE_CACHE |考虑到线程等待获得互斥体的时间，它必须在分配物理页前或将这些页返回操作系统前获得。 只有在 SQL Server 的实例使用 AWE 内存，才会显示在此类型上的等待。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SOS_PROCESS_AFFINITY_MUTEX |在同步访问进程关联设置期间出现。| 
|SOS_RESERVEDMEMBLOCKLIST |SQL Server 内存管理器中的内部同步期间出现。 <br /> **适用于**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]仅。 |  
|SOS_SCHEDULER_YIELD |在任务自愿为要执行的其他任务生成计划程序时出现。 在该等待期间任务正在等待其量程更新。| 
|SOS_SMALL_PAGE_ALLOC |在分配和释放由某些内存对象管理的内存时出现。| 
|SOS_STACKSTORE_INIT_MUTEX |在内部存储初始化同步期间出现。| 
|SOS_SYNC_TASK_ENQUEUE_EVENT |在任务以同步方式启动时出现。 SQL Server 中的大多数任务以异步方式，在控件返回到启动器任务请求放置在工作队列之后立即启动。| 
|SOS_VIRTUALMEMORY_LOW |在内存分配等待资源管理器释放虚拟内存时出现。| 
|SOSHOST_EVENT |宿主的组件，如 CLR，等待上一个 SQL Server 事件同步对象时发生。| 
|SOSHOST_INTERNAL |在宿主组件（如 CLR）使用的内存管理器回调同步期间出现。| 
|SOSHOST_MUTEX |宿主的组件，如 CLR，等待上一个 SQL Server 互斥体同步对象时发生。| 
|SOSHOST_RWLOCK |宿主的组件，如 CLR，等待上一个 SQL Server 读取器 / 编写器同步对象时发生。| 
|SOSHOST_SEMAPHORE |宿主的组件，如 CLR，等待上一个 SQL Server 信号量同步对象时发生。| 
|SOSHOST_SLEEP |当宿主任务在等待一般事件出现期间睡眠时出现。 宿主任务由宿主组件（如 CLR）使用。| 
|SOSHOST_TRACELOCK |在同步访问跟踪流期间出现。| 
|SOSHOST_WAITFORDONE |在宿主组件（如 CLR）等待任务完成时出现。| 
|SP_PREEMPTIVE_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SP_SERVER_DIAGNOSTICS_BUFFER_ACCESS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SP_SERVER_DIAGNOSTICS_INIT_MUTEX |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SP_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLCLR_APPDOMAIN |在 CLR 等待应用程序域完成启动时出现。| 
|SQLCLR_ASSEMBLY |在等待访问 appdomain 中已加载的程序集列表时出现。| 
|SQLCLR_DEADLOCK_DETECTION |在 CLR 等待死锁检测完成时出现。| 
|SQLCLR_QUANTUM_PUNISHMENT |在 CLR 任务由于已经超过了其执行量程而中止时出现。 此中止已完成，以便减小此大量消耗资源的任务对其他任务的影响。| 
|SQLSORT_NORMMUTEX |在初始化内部排序结构时进行内部同步期间出现。| 
|SQLSORT_SORTMUTEX |在初始化内部排序结构时进行内部同步期间出现。| 
|SQLTRACE_BUFFER_FLUSH |当某任务正在等待后台任务将跟踪缓冲区每隔四秒刷新到磁盘时出现。 <br /> **适用于**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]仅。 |  
|SQLTRACE_FILE_BUFFER |在文件跟踪期间同步跟踪缓冲区期间出现。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLTRACE_FILE_READ_IO_COMPLETION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLTRACE_FILE_WRITE_IO_COMPLETION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLTRACE_INCREMENTAL_FLUSH_SLEEP |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLTRACE_LOCK |TBD <br /> **适用于**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]仅。 |  
|SQLTRACE_PENDING_BUFFER_WRITERS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLTRACE_SHUTDOWN |在跟踪关闭等待未完成的跟踪事件完成时出现。| 
|SQLTRACE_WAIT_ENTRIES |在 SQL 跟踪事件队列等待数据包到达队列时出现。| 
|SRVPROC_SHUTDOWN |在关闭进程等待内部资源释放以完全关闭时出现。| 
|STARTUP_DEPENDENCY_MANAGER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|TDS_BANDWIDTH_STATE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|TDS_INIT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|TDS_PROXY_CONTAINER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|TEMPOBJ |在临时对象删除同步时出现。 该等待很少出现，仅在任务已请求 temp 表的独占访问删除时出现。| 
|TEMPORAL_BACKGROUND_PROCEED_CLEANUP |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|TERMINATE_LISTENER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|THREADPOOL |当某任务正在等待工作线程运行时出现。 这可能指示最大工作线程数设置过低，或批处理执行时间过长，从而减少可满足其他批处理的工作线程数。| 
|TIMEPRIV_TIMEPERIOD |在扩展事件计时器进行内部同步期间出现。| 
|TRACE_EVTNOTIF |TBD| 
|TRACEWRITE |当 SQL 跟踪行集跟踪提供程序等待可用缓冲区或可处理事件的缓冲区时出现。| 
|TRAN_MARKLATCH_DT |在等待事务标记闩锁中的破坏模式闩锁时出现。 事务标记闩锁用于同步提交与标记的事务。| 
|TRAN_MARKLATCH_EX |在等待标记事务中的排他模式闩锁时出现。 事务标记闩锁用于同步提交与标记的事务。| 
|TRAN_MARKLATCH_KP |在等待标记事务中的保持模式闩锁时出现。 事务标记闩锁用于同步提交与标记的事务。| 
|TRAN_MARKLATCH_NL |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|TRAN_MARKLATCH_SH |在等待标记事务中的共享模式闩锁时出现。 事务标记闩锁用于同步提交与标记的事务。| 
|TRAN_MARKLATCH_UP |在等待标记事务中的更新模式闩锁时出现。 事务标记闩锁用于同步提交与标记的事务。| 
|TRANSACTION_MUTEX |在同步多个批处理访问事务期间出现。| 
|UCS_ENDPOINT_CHANGE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UCS_MANAGER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UCS_MEMORY_NOTIFICATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UCS_SESSION_REGISTRATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UCS_TRANSPORT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UCS_TRANSPORT_STREAM_CHANGE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UTIL_PAGE_ALLOC |在内存不足期间事务日志扫描等待可用内存时出现。| 
|VDI_CLIENT_COMPLETECOMMAND |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|VDI_CLIENT_GETCOMMAND |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|VDI_CLIENT_OPERATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|VDI_CLIENT_OTHER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|VERSIONING_COMMITTING |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|VIA_ACCEPT |当在启动过程中完成虚拟接口适配器 (VIA) 提供程序连接时出现。| 
|VIEW_DEFINITION_MUTEX |在同步访问已缓存的视图定义期间出现。| 
|WAIT_FOR_RESULTS |在等待查询通知触发时出现。| 
|WAIT_SCRIPTDEPLOYMENT_REQUEST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_SCRIPTDEPLOYMENT_WORKER |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XLOGREAD_SIGNAL |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|WAIT_XTP_ASYNC_TX_COMPLETION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_CKPT_AGENT_WAKEUP |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_CKPT_CLOSE |等待完成检查点时出现。， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_CKPT_ENABLED |已禁用，并等待进行的检查点，若要启用检查点时将发生。， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_CKPT_STATE_LOCK |当同步检查的检查点状态时发生。， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_COMPILE_WAIT |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|WAIT_XTP_GUEST |数据库内存分配器需要停止接收低内存通知时发生。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_HOST_WAIT |个等待由数据库引擎触发并且由主机实现。， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_OFFLINE_CKPT_BEFORE_REDO |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_OFFLINE_CKPT_LOG_IO |脱机检查点正在等待日志读取 IO 完成时发生。， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_OFFLINE_CKPT_NEW_LOG |脱机检查点正在等待新的日志记录，可供扫描时发生。， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_PROCEDURE_ENTRY |放置过程等待要完成该过程的所有当前执行时发生。， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_RECOVERY |当数据库恢复等待恢复的内存优化对象完成时出现。， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_SERIAL_RECOVERY |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|WAIT_XTP_SWITCH_TO_INACTIVE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_TASK_SHUTDOWN |当等待内存中 OLTP 线程完成时出现。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_TRAN_DEPENDENCY |当等待事务依赖项时出现。， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAITFOR |WAITFOR TRANSACT-SQL 语句，将发生。 等待持续时间由此语句的参数确定。 它是用户启动的等待。| 
|WAITFOR_PER_QUEUE |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAITFOR_TASKSHUTDOWN |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|WAITSTAT_MUTEX |在同步访问用于填充 sys.dm_os_wait_stats 的统计信息集期间出现。| 
|WCC |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|WINDOW_AGGREGATES_MULTIPASS |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WINFAB_API_CALL |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WINFAB_REPLICA_BUILD_OPERATION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WINFAB_REPORT_FAULT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WORKTBL_DROP |在删除出现故障的工作表之后，重试之前的暂停期间出现。| 
|WRITE_COMPLETION |当正在进行写操作时出现。| 
|WRITELOG |等待日志刷新完成时出现。 导致日志刷新的常见操作是检查点和事务提交。| 
|XACT_OWN_TRANSACTION |在等待获取事务的所有权时出现。| 
|XACT_RECLAIM_SESSION |在等待会话的当前所有者释放会话的所有权时出现。| 
|XACTLOCKINFO |在同步访问事务锁列表期间出现。 除事务本身之外，在页拆分过程中死锁检测和锁迁移等操作也可访问锁列表。| 
|XACTWORKSPACE_MUTEX |在同步事务中的脱离以及事务登记成员之间的数据库锁数时出现。| 
|XDB_CONN_DUP_HASH |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XDES_HISTORY |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XDES_OUT_OF_ORDER_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XDES_SNAPSHOT |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XDESTSVERMGR |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XE_BUFFERMGR_ALLPROCESSED_EVENT |在扩展事件会话缓冲区刷新到目标时发生。 此等待在后台线程上发生。| 
|XE_BUFFERMGR_FREEBUF_EVENT |当下列任一条件成立时发生：| 
|XE_CALLBACK_LIST |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XE_CX_FILE_READ |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XE_DISPATCHER_CONFIG_SESSION_LIST |在使用异步目标的扩展事件会话启动或停止时发生。 此等待表明发生了以下某一情况：| 
|XE_DISPATCHER_JOIN |在用于扩展事件会话的后台线程终止时发生。| 
|XE_DISPATCHER_WAIT |在用于扩展事件会话的后台线程等待事件缓冲区进行处理时发生。| 
|XE_FILE_TARGET_TVF |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XE_LIVE_TARGET_TVF |TBD <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XE_MODULEMGR_SYNC |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|XE_OLS_LOCK |标识为仅供参考。 不提供支持。 不保证以后的兼容性。| 
|XE_PACKAGE_LOCK_BACKOFF |标识为仅供参考。 不提供支持。 <br /> **适用于**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]仅。 |  
|XE_SERVICES_EVENTMANUAL |TBD| 
|XE_SERVICES_MUTEX |TBD| 
|XE_SERVICES_RWLOCK |TBD| 
|XE_SESSION_CREATE_SYNC |TBD| 
|XE_SESSION_FLUSH |TBD| 
|XE_SESSION_SYNC |TBD| 
|XE_STM_CREATE |TBD| 
|XE_TIMER_EVENT |TBD| 
|XE_TIMER_MUTEX |TBD| 
|XE_TIMER_TASK_DONE |TBD| 
|XIO_CREDENTIAL_MGR_RWLOCK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XIO_CREDENTIAL_RWLOCK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XIO_EDS_MGR_RWLOCK |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|XIO_EDS_RWLOCK |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|XIO_IOSTATS_BLOBLIST_RWLOCK |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|XIO_IOSTATS_FCBLIST_RWLOCK |TBD <br /> **适用于**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]当前。| 
|XIO_LEASE_RENEW_MGR_RWLOCK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTP_HOST_DB_COLLECTION |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTP_HOST_LOG_ACTIVITY |TBD <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTP_HOST_PARALLEL_RECOVERY |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTP_PREEMPTIVE_TASK |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTP_TRUNCATION_LSN |TBD <br /> **适用范围**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTPPROC_CACHE_ACCESS |进行时访问所有本机编译存储的过程缓存对象。， <br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTPPROC_PARTITIONED_STACK_CREATE |本机分配每个 NUMA 节点为给定的过程中编译存储的过程缓存结构 （必须进行单线程） 时发生。， <br /> **适用范围**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|

  
 以下 Xevent 将与分区**交换机**和联机索引重新生成。 有关语法的信息，请参阅[ALTER TABLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md)和[ALTER 索引 &#40;Transact SQL &#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 有关锁兼容性矩阵，请参阅[sys.dm_tran_locks &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).  
  
## <a name="see-also"></a>另请参阅  
    
 [SQL Server 操作系统相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_session_wait_stats &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)   
 [sys.dm_db_wait_stats &#40;Azure SQL Database &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-wait-stats-azure-sql-database.md)  
  
  


