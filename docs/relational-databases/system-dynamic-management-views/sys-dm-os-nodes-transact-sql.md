---
title: sys.dm_os_nodes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dec718bfea5748db1baa4bb5d9be8c01b85ace26
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643485"
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

一个名为 SQLOS 的内部组件可创建模拟硬件处理器位置的节点结构。 可以使用更改这些结构[软 NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md)创建自定义节点布局。  

> [!NOTE]
> 从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，则[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]将自动使用的特定硬件配置软件 NUMA。 有关详细信息，请参阅[自动软件 NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa)。
  
下表提供了有关这些节点的信息。  
  
> [!NOTE]
> 若要调用来自此 DMV[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_nodes**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|节点的 ID。|  
|node_state_desc|**nvarchar(256)**|对节点状态的说明。 首先显示互斥的值，后跟可组合的值。 例如：<br /> Online, Thread Resources Low, Lazy Preemptive<br /><br />有四个互斥的 node_state_desc 值。 它们是下面列出了及其说明。<br /><ul><li>联机： 节点处于联机状态<li>脱机： 节点处于脱机状态<li>空闲： 节点没有挂起的工作请求，并且已进入空闲状态。<li>IDLE_READY： 节点没有挂起的工作请求，并已准备好进入空闲状态。</li></ul><br />有三个可组合的 node_state_desc 值，下面列出了及其说明。<br /><ul><li>DAC： 此节点保留供[专用管理连接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)。<li>THREAD_RESOURCES_LOW： 没有新的线程可以创建在此节点上由于内存不足的情况。<li>热添加： 指示节点已添加以响应一个热添加 CPU 事件。</li></ul>|  
|memory_object_address|**varbinary(8)**|与此节点关联的内存对象的地址。 与一对一关系[sys.dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).memory_object_address。|  
|memory_clerk_address|**varbinary(8)**|与此节点关联的内存分配器的地址。 与一对一关系[sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).memory_clerk_address。|  
|io_completion_worker_address|**varbinary(8)**|分配给此节点的 IO 完成的工作线程的地址。 与一对一关系[sys.dm_os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).worker_address。|  
|memory_node_id|**smallint**|此节点所属的内存节点的 ID。 为多对一关系[sys.dm_os_memory_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md).memory_node_id。|  
|cpu_affinity_mask|**bigint**|用于标识此节点所关联的 CPU 的位图。|  
|online_scheduler_count|**smallint**|此节点由管理的联机计划程序数。|  
|idle_scheduler_count|**smallint**|没有活动的工作线程的联机计划程序数目。|  
|active_worker_count|**int**|在此节点所管理的所有计划程序上处于活动状态的工作线程数目。|  
|avg_load_balance|**int**|此节点上每个计划程序的平均任务数。|  
|timer_task_affinity_mask|**bigint**|用于标识可为其分配计时器任务的计划程序的位图。|  
|permanent_task_affinity_mask|**bigint**|用于标识可为其分配永久性任务的计划程序的位图。|  
|resource_monitor_state|**bit**|每个节点都分配有一个资源监视器。 资源监视器可以处于运行或空闲状态。 值 1 表示正在运行，值 0 表示处于空闲状态。|  
|online_scheduler_mask|**bigint**|标识此节点的进程关联掩码。|  
|processor_group|**smallint**|标识此节点的处理器组。|  
|cpu_count |**int** |此节点可用的 Cpu 数。 |
|pdw_node_id|**int**|对于此分布的节点标识符。<br /><br /> **适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissions

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="see-also"></a>请参阅    
 [与 SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [软件 NUMA (SQL Server)](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
