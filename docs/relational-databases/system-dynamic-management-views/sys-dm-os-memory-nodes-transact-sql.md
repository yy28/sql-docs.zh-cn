---
title: sys.dm_os_memory_nodes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_memory_nodes_TSQL
- sys.dm_os_memory_nodes
- sys.dm_os_memory_nodes_TSQL
- dm_os_memory_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_nodes dynamic management view
ms.assetid: bf4032fe-7db1-40e9-a62e-d69cebff4b44
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: af846d310fbe4cc24ceee3f55bb9d854a852f54c
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39554007"
---
# <a name="sysdmosmemorynodes-transact-sql"></a>sys.dm_os_memory_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内部分配使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存管理器。 跟踪从进程内存计数器之间的差异**sys.dm_os_process_memory**内部计数器可以显示来自外部组件中的内存使用和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内存空间。  
  
 针对每个物理 NUMA 内存节点都创建了节点。 这些可能是不同于中的 CPU 节点**sys.dm_os_nodes**。  
  
 对于直接通过 Windows 内存分配例程进行的分配不会进行跟踪。 下表提供了仅通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存管理器接口进行的内存分配的相关信息。  
  
> [!NOTE]  
>  若要调用此项从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_memory_nodes**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**memory_node_id**|**smallint**|指定内存节点的 ID。 与相关**memory_node_id**的**sys.dm_os_memory_clerks**。 不可为 Null。|  
|**virtual_address_space_reserved_kb**|**bigint**|指示既未提交也未映射到物理页的预留虚拟地址数量（以 KB 为单位）。 不可为 Null。|  
|**virtual_address_space_committed_kb**|**bigint**|指定已提交或映射到物理页的虚拟地址数量（以 KB 为单位）。 不可为 Null。|  
|**locked_page_allocations_kb**|**bigint**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 锁定的物理内存数量（以 KB 为单位）。 不可为 Null。|  
|**single_pages_kb**|**bigint**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 通过使用单页分配器并按此节点上运行的线程分配的已提交内存量（以 KB 为单位）。 该内存是从缓冲池分配的。 该值指示的是发生分配请求的节点，而不是满足分配请求的物理位置。|  
|**pages_kb**|**bigint**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指定已提交的内存数量（以 KB 为单位），这是由内存管理器页面分配器从此 NUMA 节点分配的。 不可为 Null。|  
|**multi_pages_kb**|**bigint**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 通过使用多页分配器并按此节点上运行的线程分配的已提交内存量（以 KB 为单位）。 该内存是从缓冲池之外分配的。 此值指示分配请求发生的节点，不满足分配请求的位置的物理位置。|  
|**shared_memory_reserved_kb**|**bigint**|指定从此节点中保留的共享内存数量（以 KB 为单位）。 不可为 Null。|  
|**shared_memory_committed_kb**|**bigint**|指定在此节点上提交的共享内存数量（以 KB 为单位）。 不可为 Null。|  
|**cpu_affinity_mask**|**bigint**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 仅限内部使用。 不可为 Null。|  
|**online_scheduler_mask**|**bigint**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 仅限内部使用。 不可为 Null。|  
|**processor_group**|**smallint**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 仅限内部使用。 不可为 Null。|  
|**foreign_committed_kb**|**bigint**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指定从其他内存节点中提交的内存数量（以 KB 为单位）。 不可为 Null。|  
|**target_kb** |**bigint** |适用范围：[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 指定内存节点的内存目标 （kb）。 |   
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 对于此分布的节点标识符。|  
  
## <a name="permissions"></a>Permissions

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="see-also"></a>请参阅  
  [与 SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


