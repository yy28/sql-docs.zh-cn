---
title: sys.dm_os_memory_objects (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fc006a940318ba84c3670ed9d10b96f728219668
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800641"
---
# <a name="sysdmosmemoryobjects-transact-sql"></a>sys.dm_os_memory_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回当前由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分配的内存对象。 可以使用**sys.dm_os_memory_objects**来分析内存使用情况并标识可能出现的内存泄漏。  
  
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
|**memory_node_id**|**smallint**|该内存对象所用的内存节点的 ID。 不可为 null。|  
|**creation_time**|**datetime**|仅限内部使用。 可以为 Null。|  
|**max_pages_allocated_count**|**int**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 由该内存对象分配的最大页数。 不可为 null。|  
|**page_size_in_bytes**|**int**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 由该对象分配的页的大小（以字节为单位）。 不可为 null。|  
|**max_pages_in_bytes**|**bigint**|该内存对象曾经使用的最大内存量。 不可为 null。|  
|**page_allocator_address**|**varbinary(8)**|页分配器的内存地址。 不可为 null。 有关详细信息，请参阅[sys.dm_os_memory_clerks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)。|  
|**creation_stack_address**|**varbinary(8)**|仅限内部使用。 可以为 Null。|  
|**sequence_num**|**int**|仅限内部使用。 可以为 Null。|  
|**partition_type**|**int**|分区类型：<br /><br /> 0-非可分区内存对象<br /><br /> 1-可分区内存对象，当前未分区<br /><br /> 2-可分区内存对象，按 NUMA 节点分区。 具有单个 NUMA 节点的环境中这相当于 1。<br /><br /> 3-可分区内存对象，按 CPU 分区。|  
|**contention_factor**|**real**|指定此内存对象，，0 表示无争用的争用的值。 每当指定的数量的内存分配进行了该时间段内的反射争用时，更新的值。 仅适用于线程安全内存对象。|  
|**waiting_tasks_count**|**bigint**|等待该内存对象的个数。 每当从该内存对象分配内存时，此计数器将递增。 增量是当前正在等待对此内存对象的访问的任务数。 仅适用于线程安全内存对象。 这是不正确性保证最佳工作值。|  
|**exclusive_access_count**|**bigint**|指定何种频率以独占方式访问该内存对象了。 仅适用于线程安全内存对象。  这是不正确性保证最佳工作值。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 对于此分布的节点标识符。|  
  
 **partition_type**， **contention_factor**， **waiting_tasks_count**，并且**exclusive_access_count**尚未实现在[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
## <a name="permissions"></a>Permissions

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="remarks"></a>备注  
 内存对象是指多个堆。 它们所提供的分配的粒度比内存分配器所提供的分配的粒度更精细。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件使用内存对象，而不使用内存分配器。 内存对象使用内存分配器的页分配器接口来分配页。 内存对象不使用虚拟内存接口或共享内存接口。 根据分配模式的不同，组件可以创建不同的内存对象类型来分配任意大小的区域。  
  
 内存对象的典型的页面大小为 8 KB。 但是，增量内存对象的页大小的范围可以从 512 字节到 8 KB。  
  
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
  
## <a name="see-also"></a>请参阅  
  [与 SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_memory_clerks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)  
  
  


