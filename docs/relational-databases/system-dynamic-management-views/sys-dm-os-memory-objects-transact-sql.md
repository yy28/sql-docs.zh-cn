---
title: sys.dm_os_memory_objects (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_memory_objects
- sys.dm_os_memory_objects
- sys.dm_os_memory_objects_TSQL
- dm_os_memory_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_objects dynamic management view
ms.assetid: 5688bcf8-5da9-4ff9-960b-742b671d7096
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0a468001a048f627996e65a5743d3f136e96909
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmosmemoryobjects-transact-sql"></a>sys.dm_os_memory_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回当前由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分配的内存对象。 你可以使用**sys.dm_os_memory_objects**以分析内存使用情况和来标识可能的内存泄漏。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**memory_object_address**|**varbinary(8)**|内存对象的地址。 不可为 null。|  
|**parent_address**|**varbinary(8)**|父内存对象的地址。 可以为 Null。|  
|**pages_allocated_count**|**int**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 由该对象分配的页数。 不可为 null。|  
|**pages_in_bytes**|**bigint**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 此内存对象实例分配的内存量（以字节为单位）。 不可为 null。|  
|**creation_options**|**int**|仅限内部使用。 可以为 Null。|  
|**bytes_used**|**bigint**|仅限内部使用。 可以为 Null。|  
|**类型**|**nvarchar(60)**|内存对象的类型。<br /><br /> 它指示该内存对象所属的特定组件，或指示内存对象的函数。 可以为 Null。|  
|**名称**|**varchar(128)**|仅限内部使用。 可以为 NULL。|  
|**memory_node_id**|**int**|该内存对象所用的内存节点的 ID。 不可为 null。|  
|**creation_time**|**datetime**|仅限内部使用。 可以为 Null。|  
|**max_pages_allocated_count**|**int**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 由该内存对象分配的最大页数。 不可为 null。|  
|**page_size_in_bytes**|**int**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 由该对象分配的页的大小（以字节为单位）。 不可为 null。|  
|**max_pages_in_bytes**|**bigint**|该内存对象曾经使用的最大内存量。 不可为 null。|  
|**page_allocator_address**|**varbinary(8)**|页分配器的内存地址。 不可为 null。 有关详细信息，请参阅[sys.dm_os_memory_clerks &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**creation_stack_address**|**varbinary(8)**|仅限内部使用。 可以为 Null。|  
|**sequence_num**|**int**|仅限内部使用。 可以为 Null。|  
|**partition_type**|**int**|分区的类型：<br /><br /> 0-非可分区内存对象<br /><br /> 1-可分区内存对象，当前未分区<br /><br /> 2-可分区内存对象，NUMA 节点的分区。 具有单个 NUMA 节点的环境中这相当于 1。<br /><br /> 3-可分区内存对象，按 CPU 分区。|  
|**contention_factor**|**real**|使用 0 表示没有任何争用对此内存对象，指定争用的值。 每当指定的数量的内存分配进行反射的争用，该时间段内，更新的值。 仅适用于线程安全内存对象。|  
|**waiting_tasks_count**|**bigint**|此内存对象等待数。 每当从这个内存对象分配内存时，此计数器即会递增。 增量是当前等待对此内存对象的访问的任务数。 仅适用于线程安全内存对象。 这是最佳的工作量值，而无需正确性保证。|  
|**exclusive_access_count**|**bigint**|指定以独占方式访问此内存对象的频率。 仅适用于线程安全内存对象。  这是最佳的工作量值，而无需正确性保证。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
 **partition_type**， **contention_factor**， **waiting_tasks_count**，和**exclusive_access_count**尚未实现在[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
## <a name="permissions"></a>权限  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层，需要`VIEW DATABASE STATE`数据库中的权限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准版和基本层，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。  
  
## <a name="remarks"></a>注释  
 内存对象是指多个堆。 它们所提供的分配的粒度比内存分配器所提供的分配的粒度更精细。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件使用内存对象，而不使用内存分配器。 内存对象使用内存分配器的页分配器接口来分配页。 内存对象不使用虚拟内存接口或共享内存接口。 根据分配模式的不同，组件可以创建不同的内存对象类型来分配任意大小的区域。  
  
 为内存对象的典型的页大小为 8KB。 但是，增量内存对象的页大小的范围可以从 512 字节到 8 KB。  
  
> [!NOTE]  
>  页大小不是最大分配。 相反，页大小是受页分配器支持，并且由内存分配器实现的分配粒度。 可从内存对象中请求大于 8 KB 的分配。  
  
## <a name="examples"></a>示例  
 以下示例返回由每种内存对象类型分配的内存量。  
  
```  
SELECT SUM (pages_in_bytes) as 'Bytes Used', type   
FROM sys.dm_os_memory_objects  
GROUP BY type   
ORDER BY 'Bytes Used' DESC;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
  [SQL Server 操作系统相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)  
  
  


