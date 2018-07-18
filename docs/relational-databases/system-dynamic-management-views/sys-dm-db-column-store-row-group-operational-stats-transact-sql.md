---
title: sys.dm_db_column_store_row_group_operational_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 655f5838456fd72566405c453cecfd8858d7d6dd
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38048825"
---
# <a name="sysdmdbcolumnstorerowgroupoperationalstats-transact-sql"></a>sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返回当前行级锁定，I/O 和访问方法活动为列存储索引中压缩行组。 使用**sys.dm_db_column_store_row_group_operational_stats**若要跟踪的时间长度用户查询必须等待读取或写入到压缩行组或分区中的列存储索引，并标识时遇到的行组大量 I/O 活动或热点。  
  
 在此 DMV 不会显示内存中列存储索引。  
 
 
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|具有列存储索引的表的 ID。|  
|**index_id**|**int**|columnstore 索引的 ID。|  
|**partition_number**|**int**|索引或堆中从 1 开始的分区号。|  
|**row_group_id**|**int**|列存储索引中的 rowgroup 的 ID。 这是在一个分区中是唯一的。|  
|**scan_count**|**int**|通过自上次 SQL 重新启动行组的扫描数。|  
|**delete_buffer_scan_count**|**int**|用于确定此行组中删除的行的删除缓冲区次数。 这包括访问内存中哈希表和基础的 b 树。|  
|**index_scan_count**|**int**|列存储索引分区已扫描次数。 这是相同的分区中的所有行组。|  
|**rowgroup_lock_count**|**bigint**|自上次 SQL 重新启动此行组的锁请求的累积计数。|  
|**rowgroup_lock_wait_count**|**bigint**|累积次数数据库引擎上等待此行组锁自上次 SQL 重新启动。|  
|**rowgroup_lock_wait_in_ms**|**bigint**|累积毫秒数的数据库引擎上等待此行组锁自上次 SQL 重新启动。|  
  
## <a name="permissions"></a>权限  
 需要下列权限：  
  
-   指定的 object_id 的表具有 CONTROL 权限。  
  
-   VIEW DATABASE STATE 权限，以返回有关在数据库中的所有对象的信息通过使用对象通配符 @*object_id* = NULL  
  
 授予 VIEW DATABASE STATE 权限允许返回数据库中的所有对象，而不考虑对特定对象拒绝的任何 CONTROL 权限。  
  
 拒绝 VIEW DATABASE STATE 将禁止返回数据库中的所有对象，而不管对特定对象授予的任何 CONTROL 权限。 此外，当数据库通配符 @*database_id*= 指定了 NULL，则省略数据库。  
  
 有关详细信息，请参阅[动态管理视图和函数&#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与索引相关的动态管理视图和函数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

