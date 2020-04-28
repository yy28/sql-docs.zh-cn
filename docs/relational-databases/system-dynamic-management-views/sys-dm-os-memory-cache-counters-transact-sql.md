---
title: sys. dm_os_memory_cache_counters （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_counters_TSQL
- dm_os_memory_cache_counters_TSQL
- sys.dm_os_memory_cache_counters
- dm_os_memory_cache_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_counters dynamic management view
ms.assetid: ca7bd036-d661-4c17-b00a-e1a975bd8932
author: stevestein
ms.author: sstein
ms.openlocfilehash: 755e0cdbf5bff5bcd9c048a2f77918dc9a6eb2a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "73982530"
---
# <a name="sysdm_os_memory_cache_counters-transact-sql"></a>sys.dm_os_memory_cache_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中缓存运行状况的快照。 **dm_os_memory_cache_counters**提供有关已分配缓存项的运行时信息、其使用情况以及缓存项的内存源。  
  
> **注意：** 若要从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]调用此，请使用名称**dm_pdw_nodes_os_memory_cache_counters**。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|指示与特定缓存关联的计数器的地址（主键）。 不可为 null。|  
|**name**|**nvarchar(256)**|指定缓存的名称。 不可为 null。|  
|**type**|**nvarchar(60)**|指示与该项关联的缓存的类型。 不可为 null。|  
|**single_pages_kb**|**bigint**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 已分配的单页内存量（千字节）。 这是通过单页分配器分配的内存量。 它指的是从此缓存的缓冲池中直接获取的 8 KB 页。 不可为 null。|  
|**pages_kb**|**bigint**|**适用于**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更高版本。<br /><br /> 指定缓存中分配的内存量 (KB)。 不可为 null。|  
|**multi_pages_kb**|**bigint**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 已分配的多页内存的容量（千字节）。 这是使用内存节点的多页分配器分配的内存量。 此内存在缓冲池外面分配，利用了内存节点虚拟分配器的优势。 不可为 null。|  
|**pages_in_use_kb**|**bigint**|**适用于**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更高版本。<br /><br /> 指定缓存中分配并使用的内存量 (KB)。 可以为 Null。  不跟踪类型为 `USERSTORE_<*>` 的对象的值。  将针对其报告 NULL。|  
|**single_pages_in_use_kb**|**bigint**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 正在使用的单页内存量（千字节）。 可以为 Null。 不会为 USERSTORE_\<* > 类型的对象跟踪此信息，这些值将为 NULL。|  
|**multi_pages_in_use_kb**|**bigint**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 正在使用的多页内存量（千字节）。 可以为 null. 不会为 USERSTORE_\<* > 类型的对象跟踪此信息，这些值将为 NULL。|  
|**entries_count**|**bigint**|指示缓存中的条目数。 不可为 null。|  
|**entries_in_use_count**|**bigint**|指示缓存中正在使用的条目数。 不可为 null。|  
|**pdw_node_id**|**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
  
## <a name="permissions"></a>权限 

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要权限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层上，需要`VIEW DATABASE STATE`具有数据库中的权限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准层和基本层上，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。   

## <a name="see-also"></a>另请参阅  
  [&#40;Transact-sql 的与操作系统相关的动态管理视图 SQL Server&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


