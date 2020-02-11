---
title: sys. dm_os_process_memory （Transact-sql） |Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fcbab4d5dc1bbc86fe9083e9c3407749040a0023
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68265696"
---
# <a name="sysdm_os_process_memory-transact-sql"></a>sys.dm_os_process_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  大多数因 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程空间导致的内存分配都是通过可跟踪和核算这些分配的接口控制的。 但是，内存分配可能会绕过内部内存管理例程在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 地址空间中进行。 值是通过调用基本操作系统获取的。 它们不是由内部的方法操作[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的，除非它是为锁定或大页面分配进行调整。  
  
 所有指示内存大小的返回值均以千字节 (KB) 表示。 列**total_virtual_address_space_reserved_kb**是从**dm_os_sys_info sys.databases** **virtual_memory_in_bytes**的副本。  
  
 下表对进程地址空间作了完整的说明。  
  
> [!NOTE]  
>  若要从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]调用此，请使用名称**dm_pdw_nodes_os_process_memory**。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|指示以 KB 表示的进程工作集（由操作系统报告），以及使用大型页 API 完成的跟踪分配。 不可为 Null。|  
|**large_page_allocations_kb**|**bigint**|指定通过使用大型页 API 分配的物理内存。 不可为 Null。|  
|**locked_page_allocations_kb**|**bigint**|指定内存中锁定的内存页面。 不可为 Null。|  
|**total_virtual_address_space_kb**|**bigint**|指示虚拟地址空间的用户模式部分的总大小。 不可为 Null。|  
|**virtual_address_space_reserved_kb**|**bigint**|指示进程保留的虚拟地址空间的总量。 不可为 Null。|  
|**virtual_address_space_committed_kb**|**bigint**|指示已提交或已映射到物理页的已保留虚拟地址空间量。 不可为 Null。|  
|**virtual_address_space_available_kb**|**bigint**|指示当前可用的虚拟地址空间量。 不可为 Null。<br /><br /> **注意：** 可以存在小于分配粒度的可用区域。 这些区域不可进行分配。|  
|**page_fault_count**|**bigint**|指示由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程引发的页错误数。 不可为 Null。|  
|**memory_utilization_percentage**|**int**|指定工作集中的已提交内存所占的百分比。 不可为 Null。|  
|**available_commit_limit_kb**|**bigint**|指示可供进程提交的内存量。 不可为 Null。|  
|**process_physical_memory_low**|**bit**|指示进程正在响应物理内存不足的通知。 不可为 Null。|  
|**process_virtual_memory_low**|**bit**|指示检测到虚拟内存不足的情况。 不可为 Null。|  
|pdw_node_id |**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
  
## <a name="permissions"></a>权限  
 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，要求具有服务器上的 VIEW SERVER STATE 权限。  
  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要权限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层上，需要`VIEW DATABASE STATE`具有数据库中的权限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准层和基本层上，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。   
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [&#40;Transact-sql 的与操作系统相关的动态管理视图 SQL Server&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


