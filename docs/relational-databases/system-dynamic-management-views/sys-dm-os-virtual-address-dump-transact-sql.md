---
title: "sys.dm_os_virtual_address_dump (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_virtual_address_dump
- sys.dm_os_virtual_address_dump_TSQL
- sys.dm_os_virtual_address_dump
- dm_os_virtual_address_dump_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_virtual_address_dump dynamic management view
ms.assetid: 7b24ea55-3873-42fd-a86c-441c92eb6175
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7088f19776027b7e71d2a0519797c655d7632110
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosvirtualaddressdump-transact-sql"></a>sys.dm_os_virtual_address_dump (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  返回有关调用进程的虚拟地址空间中的页范围的信息。  
  
> [!NOTE]  
>  此信息也会返回**VirtualQuery** Windows API。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_virtual_address_dump**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**region_base_address**|**varbinary （8)**|页区域的基址指针。 不可为 null。|  
|**region_allocation_base_address**|**varbinary （8)**|由 VirtualAlloc Windows API 函数分配的页范围的基址指针。 由 BaseAddress 成员指向的页包含在该分配范围中。 不可为 null。|  
|**region_allocation_protection**|**varbinary （8)**|首次分配区域时的保护属性。 值为下列其中一项：<br /><br /> -PAGE_READONLY<br />-PAGE_READWRITE<br />-PAGE_NOACCESS<br />-PAGE_WRITECOPY<br />-PAGE_EXECUTE<br />-PAGE_EXECUTE_READ<br />-PAGE_EXECUTE_READWRITE<br />-PAGE_EXECUTE_WRITECOPY<br />-PAGE_GUARD<br />-PAGE_NOCACHE<br /><br /> 不可为 null。|  
|**region_size_in_bytes**|**bigint**|起始于基址的区域大小（字节），该区域中的所有页均具有相同的属性。 不可为 null。|  
|**region_state**|**varbinary （8)**|区域的当前状态。 这是以下之一：<br /><br /> -MEM_COMMIT<br />-MEM_RESERVE<br />-MEM_FREE<br /><br /> 不可为 null。|  
|**region_current_protection**|**varbinary （8)**|保护属性。 值为下列其中一项：<br /><br /> -PAGE_READONLY<br />-PAGE_READWRITE<br />-PAGE_NOACCESS<br />-PAGE_WRITECOPY<br />-PAGE_EXECUTE<br />-PAGE_EXECUTE_READ<br />-PAGE_EXECUTE_READWRITE<br />-PAGE_EXECUTE_WRITECOPY<br />-PAGE_GUARD<br />-PAGE_NOCACHE<br /><br /> 不可为 null。|  
|**region_type**|**varbinary （8)**|标识区域中的页类型。 该值可以是下列值之一：<br /><br /> -MEM_PRIVATE<br />-MEM_MAPPED<br />-MEM_IMAGE<br /><br /> 不可为 null。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>Permissions  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server 操作系统相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


