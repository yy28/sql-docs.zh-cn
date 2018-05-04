---
title: sys.dm_os_workers (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_workers_TSQL
- sys.dm_os_workers_TSQL
- dm_os_workers
- sys.dm_os_workers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_workers dynamic management view
ms.assetid: 4d5d1e52-a574-4bdd-87ae-b932527235e8
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7cc93392fc513088156cb0ea05090f715d7abfed
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmosworkers-transact-sql"></a>sys.dm_os_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  对于系统中的每个工作线程，相应地返回一行。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_workers**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|worker_address|**varbinary(8)**|工作线程的内存地址。|  
|status|**int**|仅限内部使用。|  
|is_preemptive|**bit**|1 = 正在以抢先计划运行工作线程。 任何运行外部代码的工作线程都运行在抢先计划之下。|  
|is_fiber|**bit**|1 = 正在以轻型池运行工作线程。 有关详细信息，请参阅本主题后面的 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)不熟悉的读者。|  
|is_sick|**bit**|1 = 工作线程在尝试获得旋转锁时遇到困难。 如果设置此位，这可能指示发生了对频繁访问对象的争用问题。|  
|is_in_cc_exception|**bit**|1 = 工作线程当前正在处理非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 异常。|  
|is_fatal_exception|**bit**|指定此工作线程是否收到异常。|  
|is_inside_catch|**bit**|1 = 工作线程当前正在处理异常。|  
|is_in_polling_io_completion_routine|**bit**|1 = 工作线程当前正在运行挂起 I/O 的 I/O 完成例程。 有关详细信息，请参阅[sys.dm_io_pending_io_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-pending-io-requests-transact-sql.md)。|  
|context_switch_count|**int**|此工作线程所执行的计划程序上下文切换数。|  
|pending_io_count|**int**|此工作线程执行的物理 I/O 数。|  
|pending_io_byte_count|**bigint**|此工作线程的所有挂起的物理 I/O 的字节总数。|  
|pending_io_byte_average|**int**|此工作线程的物理 I/O 的平均字节数。|  
|wait_started_ms_ticks|**bigint**|中的时间，点[ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)，当此辅助进程已进入 SUSPENDED 状态。 减去此值在 ms_ticks [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)返回等待工作线程的毫秒数。|  
|wait_resumed_ms_ticks|**bigint**|中的时间，点[ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)，当此辅助进程已进入可运行的状态。 减去此值在 ms_ticks [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)返回的工作线程已可运行的队列中的毫秒数。|  
|task_bound_ms_ticks|**bigint**|中的时间，点[ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)，当一项任务绑定到此辅助进程。|  
|worker_created_ms_ticks|**bigint**|中的时间，点[ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)，当创建工作线程。|  
|exception_num|**int**|此工作线程遇到的上一个异常的错误号。|  
|exception_severity|**int**|此工作线程遇到的上一个异常的严重性。|  
|exception_address|**varbinary(8)**|出现异常的代码地址|  
|affinity|**bigint**|工作线程的线程关联。 匹配的中的线程的相关性[sys.dm_os_threads &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)。|  
|state|**nvarchar(60)**|工作线程的状态。 可以是以下值之一：<br /><br /> INIT = 工作线程当前正在初始化。<br /><br /> RUNNING = 工作线程当前正在以非抢先或抢先方式运行。<br /><br /> RUNNABLE = 工作线程准备运行在计划程序上。<br /><br /> SUSPENDED = 工作线程当前正在延迟，以等待事件向它发送信号。|  
|start_quantum|**bigint**|此工作线程的当前运行开始时的时间（以毫秒为单位）。|  
|end_quantum|**bigint**|此工作线程的当前运行结束时的时间（以毫秒为单位）。|  
|last_wait_type|**nvarchar(60)**|最后一个等待的类型。 等待类型的列表，请参阅[sys.dm_os_wait_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。|  
|return_code|**int**|从最后一个等待返回值。 可以是以下值之一：<br /><br /> 0 =SUCCESS<br /><br /> 3 = DEADLOCK<br /><br /> 4 = PREMATURE_WAKEUP<br /><br /> 258 = TIMEOUT|  
|quantum_used|**bigint**|仅限内部使用。|  
|max_quantum|**bigint**|仅限内部使用。|  
|boost_count|**int**|仅限内部使用。|  
|tasks_processed_count|**int**|此工作线程所处理的任务数。|  
|fiber_address|**varbinary(8)**|此工作线程所关联的纤程的内存地址。<br /><br /> NULL = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 没有为轻型池进行配置。|  
|task_address|**varbinary(8)**|当前任务的内存地址。 有关详细信息，请参阅[sys.dm_os_tasks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)。|  
|memory_object_address|**varbinary(8)**|工作线程内存对象的内存地址。 有关详细信息，请参阅[sys.dm_os_memory_objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)。|  
|thread_address|**varbinary(8)**|与此工作线程关联的线程的内存地址。 有关详细信息，请参阅[sys.dm_os_threads &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)。|  
|signal_worker_address|**varbinary(8)**|最后一个向此对象发出信号的工作线程的内存地址。 有关详细信息，请参阅[sys.dm_os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)。|  
|scheduler_address|**varbinary(8)**|计划程序的内存地址。 有关详细信息，请参阅[sys.dm_os_schedulers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)。|  
|processor_group|**int**|存储分配给此线程的处理器组 ID。|  
|pdw_node_id|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="remarks"></a>注释  
 如果工作线程的状态是 RUNNING 并且工作线程正在以非抢先方式运行，则工作线程地址将与 sys.dm_os_schedulers 中的 active_worker_address 进行匹配。  
  
 当等待事件的工作线程得到信号时，工作线程将被放在可运行队列的开头。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许这种情况在行中发生一千次，在此之后工作线程将被放在队列的末尾。 将工作线程移动到队列末尾会对性能有某些潜在影响。  
  
## <a name="permissions"></a>权限

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="examples"></a>示例  
 您可以使用下面的查询找出工作线程已在 SUSPENDED 或 RUNNABLE 状态下运行的时间。  
  
```sql
SELECT   
    t1.session_id,  
    CONVERT(varchar(10), t1.status) AS status,  
    CONVERT(varchar(15), t1.command) AS command,  
    CONVERT(varchar(10), t2.state) AS worker_state,  
    w_suspended =   
      CASE t2.wait_started_ms_ticks  
        WHEN 0 THEN 0  
        ELSE   
          t3.ms_ticks - t2.wait_started_ms_ticks  
      END,  
    w_runnable =   
      CASE t2.wait_resumed_ms_ticks  
        WHEN 0 THEN 0  
        ELSE   
          t3.ms_ticks - t2.wait_resumed_ms_ticks  
      END  
  FROM sys.dm_exec_requests AS t1  
  INNER JOIN sys.dm_os_workers AS t2  
    ON t2.task_address = t1.task_address  
  CROSS JOIN sys.dm_os_sys_info AS t3  
  WHERE t1.scheduler_id IS NOT NULL;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
 session_id status     command         worker_state w_suspended w_runnable  
 ---------- ---------- --------------- ------------ ----------- --------------------  
 4          background LAZY WRITER     SUSPENDED    688         688  
 6          background LOCK MONITOR    SUSPENDED    4657        4657
 19         background BRKR TASK       SUSPENDED    603820344   603820344  
 14         background BRKR EVENT HNDL SUSPENDED    63583641    63583641  
 51         running    SELECT          RUNNING      0           0  
 2          background RESOURCE MONITO RUNNING      0           603825954  
 3          background LAZY WRITER     SUSPENDED    422         422  
 7          background SIGNAL HANDLER  SUSPENDED    603820485   603820485  
 13         background TASK MANAGER    SUSPENDED    603824704   603824704  
 18         background BRKR TASK       SUSPENDED    603820407   603820407  
 9          background TRACE QUEUE TAS SUSPENDED    454         454  
 52         suspended  SELECT          SUSPENDED    35094       35094  
 1          background RESOURCE MONITO RUNNING      0           603825954  
```

 在输出中，当 `w_runnable` 和 `w_suspended` 相等时，它代表工作线程处于 SUSPENDED 状态下的时间。 否则，`w_runnable` 代表工作线程处于 RUNNABLE 状态下的时间。 在输出中，会话 `52` 处于 `SUSPENDED` 状态下的时间为 `35,094` 毫秒。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


