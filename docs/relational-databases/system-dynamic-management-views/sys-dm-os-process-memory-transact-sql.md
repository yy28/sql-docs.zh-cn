---
title: sys.dm_os_process_memory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 03830b00df02332069383e496c0b22d198b95d7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63013019"
---
# <a name="sysdmosprocessmemory-transact-sql"></a>sys.dm_os_process_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  大多数因 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程空间导致的内存分配都是通过可跟踪和核算这些分配的接口控制的。 但是，内存分配可能会绕过内部内存管理例程在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 地址空间中进行。 值是通过调用基本操作系统获取的。 它们不操作方法的内部[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但当它将调整为锁定或大型页分配除外。  
  
 所有指示内存大小的返回值均以千字节 (KB) 表示。 该列**total_virtual_address_space_reserved_kb**是相同的副本**virtual_memory_in_bytes**从**sys.dm_os_sys_info**。  
  
 下表对进程地址空间作了完整的说明。  
  
> [!NOTE]  
>  若要调用此项从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_process_memory**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|指示以 KB 表示的进程工作集（由操作系统报告），以及使用大型页 API 完成的跟踪分配。 不可为 Null。|  
|**large_page_allocations_kb**|**bigint**|指定通过使用大型页 API 分配的物理内存。 不可为 Null。|  
|**locked_page_allocations_kb**|**bigint**|指定内存中锁定的内存页面。 不可为 Null。|  
|**total_virtual_address_space_kb**|**bigint**|指示虚拟地址空间的用户模式部分的总大小。 不可为 Null。|  
|**virtual_address_space_reserved_kb**|**bigint**|指示进程保留的虚拟地址空间的总量。 不可为 Null。|  
|**virtual_address_space_committed_kb**|**bigint**|指示已提交或已映射到物理页的已保留虚拟地址空间量。 不可为 Null。|  
|**virtual_address_space_available_kb**|**bigint**|指示当前可用的虚拟地址空间量。 不可为 Null。<br /><br /> **注意：** 小于分配粒度较小的可用区域可以存在。 这些区域不可进行分配。|  
|**page_fault_count**|**bigint**|指示由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程引发的页错误数。 不可为 Null。|  
|**memory_utilization_percentage**|**int**|指定工作集中的已提交内存所占的百分比。 不可为 Null。|  
|**available_commit_limit_kb**|**bigint**|指示可供进程提交的内存量。 不可为 Null。|  
|**process_physical_memory_low**|**bit**|指示进程正在响应物理内存不足的通知。 不可为 Null。|  
|**process_virtual_memory_low**|**bit**|指示检测到虚拟内存不足的情况。 不可为 Null。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 对于此分布的节点标识符。|  
  
## <a name="permissions"></a>权限  
 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，要求具有服务器上的 VIEW SERVER STATE 权限。  
  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与 SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


