---
title: sys.dm_os_memory_cache_counters (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 19beaafe3e73265eb12f825190ee8aafcdf59897
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63047351"
---
# <a name="sysdmosmemorycachecounters-transact-sql"></a>sys.dm_os_memory_cache_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中缓存运行状况的快照。 **sys.dm_os_memory_cache_counters**提供分配的缓存项的运行时信息的使用情况，以及内存源的缓存项。  
  
> **注意**：若要调用此项从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_memory_cache_counters**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|指示与特定缓存关联的计数器的地址（主键）。 不可为 null。|  
|**名称**|**nvarchar(256)**|指定缓存的名称。 不可为 null。|  
|**类型**|**nvarchar(60)**|指示与该项关联的缓存的类型。 不可为 null。|  
|**single_pages_kb**|**bigint**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 已分配的单页内存量（千字节）。 这是通过单页分配器分配的内存量。 它指的是从此缓存的缓冲池中直接获取的 8 KB 页。 不可为 null。|  
|**pages_kb**|**bigint**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指定缓存中分配的内存量 (KB)。 不可为 null。|  
|**multi_pages_kb**|**bigint**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 已分配的多页内存的容量（千字节）。 这是使用内存节点的多页分配器分配的内存量。 此内存在缓冲池外面分配，利用了内存节点虚拟分配器的优势。 不可为 null。|  
|**pages_in_use_kb**|**bigint**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指定缓存中分配并使用的内存量 (KB)。 可以为 Null。  不跟踪类型为 `USERSTORE_<*>` 的对象的值。  将针对其报告 NULL。|  
|**single_pages_in_use_kb**|**bigint**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 正在使用的单页内存量（千字节）。 可以为 Null。 此信息不会对 USERSTORE_ 类型的对象跟踪\<* > 并且这些值将为 NULL。|  
|**multi_pages_in_use_kb**|**bigint**|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 正在使用的多页内存量（千字节）。 可以为 NULL。 此信息不会对 USERSTORE_ 类型的对象跟踪\<* >，并且这些值将为 NULL。|  
|**entries_count**|**bigint**|指示缓存中的条目数。 不可为 null。|  
|**entries_in_use_count**|**bigint**|指示缓存中正在使用的条目数。 不可为 null。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 对于此分布的节点标识符。|  
  
## <a name="permissions"></a>权限 

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="see-also"></a>请参阅  
  [与 SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


