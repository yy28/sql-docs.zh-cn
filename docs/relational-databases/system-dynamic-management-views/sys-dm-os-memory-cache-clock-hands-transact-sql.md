---
title: sys.dm_os_memory_cache_clock_hands (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_clock_hands_TSQL
- dm_os_memory_cache_clock_hands
- dm_os_memory_cache_clock_hands_TSQL
- sys.dm_os_memory_cache_clock_hands
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_clock_hands dynamic management view
ms.assetid: 0660eddc-691c-425f-9d43-71151d644de7
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2983aa6c054b462f20382457fe66a364dac6ec88
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmosmemorycacheclockhands-transact-sql"></a>sys.dm_os_memory_cache_clock_hands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回特定缓存时钟的每个指针的状态。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_memory_cache_clock_hands**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|与时钟关联的缓存的地址。 不可为 null。|  
|**名称**|**nvarchar(256)**|缓存的名称。 不可为 null。|  
|**类型**|**nvarchar(60)**|缓存存储的类型。 可存在相同类型的多个缓存。 不可为 null。|  
|**clock_hand**|**nvarchar(60)**|现有的类型。 这是以下之一：<br /><br /> External<br /><br /> 内部<br /><br /> 不可为 null。|  
|**clock_status**|**nvarchar(60)**|时钟的状态。 这是以下之一：<br /><br /> 已挂起<br /><br /> 正在运行<br /><br /> 不可为 null。|  
|**rounds_count**|**bigint**|通过缓存执行的、旨在删除项的清扫数。 不可为 null。|  
|**removed_all_rounds_count**|**bigint**|所有清扫删除的项数。 不可为 null。|  
|**updated_last_round_count**|**bigint**|上次清扫中更新的项数。 不可为 null。|  
|**removed_last_round_count**|**bigint**|上次清扫中删除的项数。 不可为 null。|  
|**last_tick_time**|**bigint**|移动时钟指针的最后时间，以毫秒表示。 不可为 null。|  
|**round_start_time**|**bigint**|上一次清扫的时间，以毫秒表示。 不可为 null。|  
|**last_round_start_time**|**bigint**|时钟完成上一往返花费的总时间，以毫秒表示。 不可为 null。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将信息存储在内存中一个称为内存缓存的结构中。 缓存中的信息可以是数据、索引条目、编译的过程计划以及其他各种类型的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 信息。 若要避免重新创建信息，尽可能将信息保留在内存缓存中，通常当信息太旧而失去用处或新信息需要使用内存空间时，会将旧信息从缓存中删除。 删除旧信息的过程称为内存清扫。 内存清扫是经常执行的操作，但不是连续执行的操作。 时钟算法控制内存缓存的清扫。 每个时钟能够控制几个内存清扫，称为指针。 内存缓存时钟指针是指一个内存清扫指针的当前位置。  

## <a name="see-also"></a>另请参阅  
 [SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
 [sys.dm_os_memory_cache_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)
  

