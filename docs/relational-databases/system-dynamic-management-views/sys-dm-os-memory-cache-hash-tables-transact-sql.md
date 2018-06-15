---
title: sys.dm_os_memory_cache_hash_tables (Transact SQL) |Microsoft 文档
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
- sys.dm_os_memory_cache_hash_tables_TSQL
- sys.dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_hash_tables dynamic management view
ms.assetid: 68b94f35-8f80-4d2b-bcde-7a21934219af
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 50e261fb0c53da8caf9f9b41d15d0f96dc7a41e4
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467773"
---
# <a name="sysdmosmemorycachehashtables-transact-sql"></a>sys.dm_os_memory_cache_hash_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的每个活动缓存返回一行。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_memory_cache_hash_tables**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|缓存条目的地址（主键）。 不可为 null。|  
|**名称**|**nvarchar(256)**|缓存的名称。 不可为 null。|  
|**类型**|**nvarchar(60)**|缓存类型。 不可为 null。|  
|**table_level**|**int**|哈希表编号。 某个特定缓存可能有多个对应于不同哈希函数的哈希表。 不可为 null。|  
|**buckets_count**|**int**|哈希表中的存储桶数。 不可为 null。|  
|**buckets_in_use_count**|**int**|当前使用的存储桶数。 不可为 null。|  
|**buckets_min_length**|**int**|存储桶中的最小缓存条目数。 不可为 null。|  
|**buckets_max_length**|**int**|存储桶中的最大缓存条目数。 不可为 null。|  
|**buckets_avg_length**|**int**|每个存储桶中的平均缓存条目数。 不可为 null。|  
|**buckets_max_length_ever**|**int**|自服务器启动以来，哈希存储桶中用于该哈希表的最大已缓存条目数。 不可为 null。|  
|**hits_count**|**bigint**|缓存命中次数。 不可为 null。|  
|**misses_count**|**bigint**|缓存未命中次数。 不可为 null。|  
|**buckets_avg_scan_hit_length**|**int**|在找到搜索项之前，存储桶中已检查条目的平均数。 不可为 null。|  
|**buckets_avg_scan_miss_length**|**int**|在搜索未成功结束之前，存储桶中已检查条目的平均数。 不可为 null。|  
|**pdw_node_id**|**int**|此分布的节点标识符。<br /><br /> **适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>权限 

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="see-also"></a>另请参阅  
 
  [SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


