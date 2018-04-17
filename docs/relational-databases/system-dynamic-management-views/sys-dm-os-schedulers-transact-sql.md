---
title: sys.dm_os_schedulers (Transact SQL) |Microsoft 文档
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
- dm_os_schedulers
- sys.dm_os_schedulers_TSQL
- sys.dm_os_schedulers
- dm_os_schedulers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_schedulers dynamic management view
ms.assetid: 3a09d81b-55d5-416f-9cda-1a3a5492abe0
caps.latest.revision: 55
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 355b762dc24fe6cd63fb1620c23fb03c7be0a6bd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmosschedulers-transact-sql"></a>sys.dm_os_schedulers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（每个计划程序都映射到其中的单个处理器）中的每个计划程序，相应地返回一行。 使用此视图可以监视计划程序的情况或标识失控任务。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_schedulers**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|scheduler_address|**varbinary(8)**|计划程序的内存地址。 不可为 null。|  
|parent_node_id|**int**|计划程序所属的节点的 ID，也称为父节点。 它代表非一致性内存访问 (NUMA) 节点。 不可为 null。|  
|scheduler_id|**int**|计划的 ID。 用来运行定期查询的所有计划程序都有小于 1048576 的 ID 号。 那些 ID 大于或等于 1048576 的计划程序（例如，专用管理员连接计划程序）则供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部使用。 不可为 null。|  
|cpu_id|**int**|分配给计划程序的 CPU ID。<br /><br /> 不可为 null。<br /><br /> **注意：** 255 不指示无关联，就象在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 请参阅[sys.dm_os_threads &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)为其他相关性信息。|  
|status|**nvarchar(60)**|指示计划程序的状态。 可以是以下值之一：<br /><br /> 隐藏联机<br />隐藏脱机<br />可见联机<br />可见脱机<br />可见联机 (DAC)<br />-HOT_ADDED<br /><br /> 不可为 null。<br /><br /> HIDDEN 计划程序用于处理[!INCLUDE[ssDE](../../includes/ssde-md.md)]的内部请求。 VISIBLE 计划程序用于处理用户请求。<br /><br /> OFFLINE 计划程序在关联掩码中映射到处于脱机状态的处理器，因此不用于处理任何请求。 ONLINE 计划程序在关联掩码中映射到处于联机状态的处理器，并且可用于处理线程。<br /><br /> DAC 指示计划程序正在专用管理员连接下运行。<br /><br /> HOT ADDED 指示已添加了计划程序以响应一个热添加 CPU 事件。|  
|is_online|**bit**|如果将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为只使用服务器中某些可用的处理器，那么此配置可以表示某些计划程序被映射到不在关联掩码中的处理器。 如果情况是这样，则此列将返回 0。 此值表示此计划程序不会用来处理查询或批。<br /><br /> 不可为 null。|  
|is_idle|**bit**|1 = 计划程序空闲。 当前未运行工作线程。 不可为 null。|  
|preemptive_switches_count|**int**|此计划程序的工作线程已切换到抢先模式的次数。<br /><br /> 若要执行在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外的代码（例如，扩展存储过程和分布式查询），则必须在非抢先计划程序的控制范围以外执行该线程。 若要这样做，工作线程将切换到抢先模式。|  
|context_switches_count|**int**|此计划程序已经发生的上下文切换数。 不可为 null。<br /><br /> 若要允许其他工作线程运行，当前正在运行的工作线程必须放弃对计划程序或切换上下文的控制权。<br /><br /> **注意：**如果辅助进程生成计划程序并将自身放入可运行的队列，然后查找未其他辅助角色，该工作人员将选择本身。 在这种情况下，context_switches_count 不会更新，但是 yield_count 会更新。|  
|idle_switches_count|**int**|计划程序在空闲时已等待事件的次数。 此列类似于 context_switches_count。 不可为 null。|  
|current_tasks_count|**int**|与此计划程序关联的当前任务数。 此计数包括：<br /><br /> -等待执行它们的辅助角色的任务。<br />-当前正在等待或 （在已挂起或可运行状态） 下运行的任务。<br /><br /> 完成任务时，此计数将减少。 不可为 null。|  
|runnable_tasks_count|**int**|已分配任务并且正在可运行队列中等待被调度的工作线程数。 不可为 null。|  
|current_workers_count|**int**|与此计划程序关联的工作线程数。 此计数包括未分配任何任务的工作线程。 不可为 null。|  
|active_workers_count|**int**|处于活动状态的工作线程数。 活动工作线程始终不是优先的，它们必须有关联的任务，并且必须处于正在运行、可运行或挂起状态之一。 不可为 null。|  
|work_queue_count|**bigint**|挂起队列中的任务数。 这些任务正在等待工作线程选取它们。 不可为 null。|  
|pending_disk_io_count|**int**|等待完成的挂起 I/O 数。 每个计划程序都有一个挂起 I/O 的列表，通过检查该列表，可以确定每次有上下文切换时它们是否已经完成。 插入请求时，计数将增加。 请求完成时此计数将减少。 此数字不指示 I/O 状态。 不可为 null。|  
|load_factor|**int**|内部值，用于指示此计划程序感觉到的负载。 此值用来确定新任务是应当放在此计划程序上，还是应当放在另一个计划程序上。 如果计划程序的负载可能不均衡，则可以使用此值进行调试。 路由决策是基于计划程序的负载来做出的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还使用节点和计划程序的加载因子来帮助确定获得资源的最佳位置。 任务排队时，加载因子将增加。 任务完成时，加载因子将减少。 使用加载因子，可以帮助 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作系统更好地平衡工作负载。 不可为 null。|  
|yield_count|**int**|用来指示此计划程序上的进度的内部值。 计划程序监视器使用此值来确定计划程序的工作线程是否正在按时产生其他工作线程。 此值不指示工作线程或任务是否转换到新的工作线程。 不可为 null。|  
|last_timer_activity|**bigint**|在 CPU 时钟周期中，计划程序上次检查计划程序计时器队列的时间。 不可为 null。|  
|failed_to_create_worker|**bit**|如果在此计划程序上无法创建新的工作线程，则设置为 1。 通常因为内存约束会发生这种情况。 可以为 Null。|  
|active_worker_address|**varbinary(8)**|工作线程的内存地址当前是活动的。 可以为 Null。 有关详细信息，请参阅[sys.dm_os_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)。|  
|memory_object_address|**varbinary(8)**|计划程序内存对象的内存地址。 不可为 NULL。|  
|task_memory_object_address|**varbinary(8)**|任务内存对象的内存地址。 不可为 null。 有关详细信息，请参阅[sys.dm_os_memory_objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)。|  
|quantum_length_us|**bigint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]公开 SQLOS 使用的计划程序量程。|  
|pdw_node_id|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>权限

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="examples"></a>示例  
  
### <a name="a-monitoring-hidden-and-nonhidden-schedulers"></a>A. 监视隐藏和非隐藏计划程序  
 下面的查询跨所有计划程序输出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的工作线程和任务的状态。 执行此查询的计算机系统应具有：  
  
-   两个处理器 (CPU)  
  
-   两个 (NUMA) 节点  
  
-   每个 NUMA 节点一个 CPU  
  
-   设置为 `0x03` 的关联掩码。  
  
```  
SELECT  
    scheduler_id,  
    cpu_id,  
    parent_node_id,  
    current_tasks_count,  
    runnable_tasks_count,  
    current_workers_count,  
    active_workers_count,  
    work_queue_count  
  FROM sys.dm_os_schedulers;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
scheduler_id cpu_id parent_node_id current_tasks_count  
------------ ------ -------------- -------------------  
0            1      0              9                    
257          255    0              1                    
1            0      1              10                   
258          255    1              1                    
255          255    32             2                    
  
runnable_tasks_count current_workers_count  
-------------------- ---------------------  
0                    11                     
0                    1                      
0                    18                     
0                    1                      
0                    3                      
  
active_workers_count work_queue_count  
-------------------- --------------------  
6                    0  
1                    0  
8                    0  
1                    0  
1                    0  
```  
  
 输出提供下列信息：  
  
-   有五个计划。 两个计划程序的 ID 值 < 1048576。 ID >= 1048576 的计划程序称为隐藏计划程序。 计划程序 `255` 代表专用管理员连接 (DAC)。 每个实例都有一个 DAC 计划程序。 协调内存压力的资源监视器为两个 NUMA 节点分别使用计划程序 `257` 和计划程序 `258`。  
  
-   输出中有 23 个当前任务。 除了已由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动的资源管理任务之外，这些任务还包括用户请求。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 任务的示例为 RESOURCE MONITOR（每个 NUMA 节点一个）、LAZY WRITER（每个 NUMA 节点一个）、LOCK MONITOR、CHECKPOINT 和 LOG WRITER。  
  
-   NUMA 节点 `0` 映射到 CPU `1`，NUMA 节点 `1` 映射到 CPU `0`。 通常，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在节点 0 之外的另一个 NUMA 节点中启动。  
  
-   当 `runnable_tasks_count` 返回 `0` 时，表示没有正在运行的当前任务。 但是，可能存在活动会话。  
  
-   计划程序 `255` 表示 DAC 有 `3` 个与其关联的工作线程。 这些工作线程在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动时分配并且不会更改。 这些工作线程仅用于处理 DAC 查询。 此计划程序中的两个任务代表一个连接管理器和一个空闲工作线程。  
  
-   `active_workers_count` 表示具有关联的任务并在非抢先模式下运行的所有辅助进程。 某些任务（例如，网络侦听器）在抢先计划下运行。  
  
-   隐藏计划程序不会处理典型用户请求。 DAC 计划程序例外。 此 DAC 计划程序有一个处理请求的线程。  
  
### <a name="b-monitoring-nonhidden-schedulers-in-a-busy-system"></a>B. 在繁忙系统中监视非隐藏计划程序  
 下面的查询显示了高负荷非隐藏计划程序（其中存在的请求多于可用工作线程可以处理的请求）的状态。 在此示例中，256 个工作线程分配有任务。 某些任务正在等待分配给工作线程。 较低的可运行计数表示有多个任务正在等待资源。  
  
> [!NOTE]  
>  您可以通过查询 sys.dm_os_workers 查找工作线程的状态。 有关详细信息，请参阅[sys.dm_os_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)。  
  
 下面是查询：  
  
```  
SELECT  
    scheduler_id,  
    cpu_id,  
    current_tasks_count,  
    runnable_tasks_count,  
    current_workers_count,  
    active_workers_count,  
    work_queue_count  
  FROM sys.dm_os_schedulers  
  WHERE scheduler_id < 255;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
scheduler_id current_tasks_count runnable_tasks_count  
------------ ------------------- --------------------  
0            144                 0                     
1            147                 1                     
  
current_workers_count active_workers_count work_queue_count  
--------------------- -------------------- --------------------  
128                   125                  16  
128                   126                  19  
```  
  
 通过比较，下面的结果显示多个可运行的任务，其中没有等待获取工作线程的任务。 对于两个计划程序，`work_queue_count` 均为 `0`。  
  
```  
scheduler_id current_tasks_count runnable_tasks_count  
------------ ------------------- --------------------  
0            107                 98                    
1            110                 100                   
  
current_workers_count active_workers_count work_queue_count  
--------------------- -------------------- --------------------  
128                   104                  0  
128                   108                  0  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


