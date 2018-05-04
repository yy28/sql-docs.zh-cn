---
title: sys.dm_column_store_object_pool (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fecf0703bad0ae0d039848d15ed0bd9a5fae1a70
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmcolumnstoreobjectpool-transact-sql"></a>sys.dm_column_store_object_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 返回对列存储索引对象的对象内存池使用情况的不同类型的计数。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|数据库 ID。 这是唯一的 SQL Server 数据库或 Azure SQL 数据库服务器实例中。 |  
|`object_id`|`int`|对象的 ID。 对象是 object_types 之一。 | 
|`index_id`|`int`|columnstore 索引的 ID。|  
|`partition_number`|`bigint`|索引或堆中从 1 开始的分区号。 每个表或视图具有至少一个分区。| 
|`column_id`|`int`|列存储列的 ID。 这是对于 DELETE_BITMAP 为 NULL。| 
|`row_group_id`|`int`|Rowgroup 的 ID。|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT – 列段。 `object_id` 为段 id。 段存储在一个行组中的某一列的所有值。 例如，如果表具有 10 列，有 10 每个行的列段。 <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY – 一个包含查找表中的列段的所有信息的全局字典。<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY-本地字典与一个列相关联。<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY – 全局字典中的另一种表示。 这提供了对 dictionary_id 有价值的反向查找。 用于创建压缩的段作为元组发动机或大容量加载的一部分。<br /><br /> 删除 COLUMN_SEGMENT_DELETE_BITMAP – 跟踪段的位图。 没有每个分区一个删除位图。|  
|`access_count`|`int`|读取或写入此对象的访问的数。|  
|`memory_used_in_bytes`|`bigint`|对象池在此对象使用的内存。|  
|`object_load_time`|`datetime`|当已 object_id 置于对象池的时钟时间。|  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
 
## <a name="see-also"></a>另请参阅  
  
 [与索引相关的动态管理视图和函数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
