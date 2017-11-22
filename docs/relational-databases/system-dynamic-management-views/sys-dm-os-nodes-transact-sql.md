---
title: "sys.dm_os_nodes (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/19/2017
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
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5cf36f7156f9297231fc232e8fecafee5e77427c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  一个名为 SQLOS 的内部组件可创建模拟硬件处理器位置的节点结构。 可以使用软件 NUMA 来创建自定义节点布局从而对这些结构进行更改。  
  
 下表提供了有关这些节点的信息。  
  
> **注意：**调用从此 DMV[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_nodes**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|node_id|**int**|节点的 ID。|  
|node_state_desc|**nvarchar(256)**|对节点状态的说明。 首先显示互斥的值，后跟可组合的值。 例如：<br /><br /> Online, Thread Resources Low, Lazy Preemptive<br /><br /> 有四个互相排斥的 node_state_desc 值。 它们下面列出了及其说明。<br /><br /> 联机： 节点已联机<br /><br /> 脱机： 节点处于脱机状态<br /><br /> 空闲： 节点没有挂起的工作请求中，并且已进入空闲状态。<br /><br /> IDLE_READY： 节点不具有挂起的工作请求，并已准备好进入空闲状态。<br /><br /> 有五个 combinable node_state_desc 值，下面列出了及其说明。<br /><br /> DAC： 此节点被保留的专用管理连接。<br /><br /> THREAD_RESOURCES_LOW： 没有新线程可以创建在此节点上由于内存不足的情况。<br /><br /> 热添加： 指示在响应中添加了节点热添加 CPU 事件。|  
|memory_object_address|**varbinary （8)**|与此节点关联的内存对象的地址。 与 sys.dm_os_memory_objects.memory_object_address 具有一对一关系。|  
|memory_clerk_address|**varbinary （8)**|与此节点关联的内存分配器的地址。 与 sys.dm_os_memory_clerks.memory_clerk_address 具有一对一关系。|  
|io_completion_worker_address|**varbinary （8)**|分配给此节点的 IO 完成的工作线程的地址。 与 sys.dm_os_workers.worker_address 具有一对一关系。|  
|memory_node_id|**int**|此节点所属的内存节点的 ID。 与 sys.dm_os_memory_nodes.memory_node_id 具有多对一关系。|  
|cpu_affinity_mask|**bigint**|用于标识此节点所关联的 CPU 的位图。|  
|online_scheduler_count|**int**|Online 的计划程序管理的此节点数。|  
|idle_scheduler_count|**int**|没有活动的工作线程的联机计划程序数目。|  
|active_worker_count|**int**|在此节点所管理的所有计划程序上处于活动状态的工作线程数目。|  
|avg_load_balance|**int**|此节点上每个计划程序的平均任务数。|  
|timer_task_affinity_mask|**bigint**|用于标识可为其分配计时器任务的计划程序的位图。|  
|permanent_task_affinity_mask|**bigint**|用于标识可为其分配永久性任务的计划程序的位图。|  
|resource_monitor_state|**bit**|每个节点都分配有一个资源监视器。 资源监视器可以处于运行或空闲状态。 值 1 表示正在运行，值 0 表示处于空闲状态。|  
|online_scheduler_mask|**bigint**|标识此节点的进程关联掩码。|  
|processor_group|**int**|标识此节点的处理器组。|  
|cpu_count |**int** |可用于此节点的 Cpu 数。 |
|pdw_node_id|**int**|此分布的节点标识符。<br /><br /> **适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissions  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层，需要`VIEW DATABASE STATE`数据库中的权限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准版和基本层，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。  
  
## <a name="see-also"></a>另请参阅  
  
 [SQL Server 操作系统相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [软件 NUMA (SQL Server)](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  


