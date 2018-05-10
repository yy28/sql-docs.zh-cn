---
title: sys.dm_db_xtp_hash_index_stats (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_hash_index_stats
- sys.dm_db_xtp_hash_index_stats_TSQL
- dm_db_xtp_hash_index_stats
- dm_db_xtp_hash_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_hash_index_stats (dynamic management view)
ms.assetid: 45969884-cd61-48e8-aee5-c725c78e3e4c
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b1614f16ae94ef1c7fee9719bd0eb0c3bf2ac93d
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmdbxtphashindexstats-transact-sql"></a>sys.dm_db_xtp_hash_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  这些统计信息可用来了解和优化存储桶计数。 它还可用于检测索引键具有许多重复项的情况。  
  
 平均链长度较大指示将许多行哈希处理至同一个存储桶。 之所以出现这种情况，原因可能是：  
  
-   如果空存储桶的数目较少，或平均链长度和最大链长度接近，则存储桶总数可能会过少。 这将导致许多不同的索引键哈希处理至同一个存储桶中。  
  
-   如果空存储桶的数目较高，或最大链长度比平均链长度高，则可能许多行具有重复的索引键值，或者键值存在偏斜。 索引键相同的所有行都将哈希处理至同一个存储桶，因而，该存储桶有较长的链长度。  
  
链长度较长可能会显著影响针对各单独行的所有 DML 操作的性能，包括 SELECT 和 INSERT。 链长度较短以及空存储桶计数较高指示 bucket_count 过高。 这将降低索引扫描的性能。  
  
> [!WARNING]
> **sys.dm_db_xtp_hash_index_stats**扫描整个表。 因此，如果你数据库中有大型表**sys.dm_db_xtp_hash_index_stats**可能需要很长时间运行。  
  
有关详细信息，请参阅[内存优化表的哈希索引](../../relational-databases/sql-server-index-design-guide.md#hash_index)。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|object_id|**int**|父表的对象 ID。|  
|xtp_object_id|**bigint**|内存优化表的 ID。|  
|index_id|**int**|索引 ID。|  
|total_bucket_count|**bigint**|索引中哈希存储桶的总数。|  
|empty_bucket_count|**bigint**|索引中空哈希存储桶的数量。|  
|avg_chain_length|**bigint**|索引中所有哈希存储桶的平均行链长度。|  
|max_chain_length|**bigint**|哈希存储桶中的最大行链长度。|  
|xtp_object_id|**bigint**|对应于内存优化表的内存中 OLTP 对象 ID。|  
  
## <a name="permissions"></a>权限  
 要求对服务器具有 VIEW DATABASE STATE 权限。  

## <a name="examples"></a>示例  
  
### <a name="a-troubleshooting-hash-index-bucket-count"></a>A. 对哈希索引桶计数进行故障排除

以下查询可以用于对现有表的哈希索引桶计数进行故障排除。 查询返回对用户表的空存储桶，并为所有哈希索引的链长度百分比有关的统计信息。

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
``` 

有关如何解释此查询的结果的详细信息，请参阅[内存优化表的故障排除哈希索引](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)。  

### <a name="b-hash-index-statistics-for-internal-tables"></a>B. 内部表的哈希索引统计信息

某些功能使用内部利用哈希索引，例如内存优化表上的列存储索引的表。 下面的查询返回对链接到用户表的内部表的哈希索引的统计信息。

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [user_table],
    ia.type_desc as [internal_table_type],
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type!=1
  ORDER BY [user_table], [internal_table_type], [index]; 
```

请注意，不能更改内部表的索引的 BUCKET_COUNT，因此此查询的输出应视为信息性仅。 不需要执行任何操作。  

此查询不需要返回任何行，除非你使用的功能，可利用内部表上的哈希索引。 以下内存优化表包含列存储索引。 创建此表后，你将在内部表上看到哈希索引。

```sql
  CREATE TABLE dbo.table_columnstore
  (
    c1 INT NOT NULL PRIMARY KEY NONCLUSTERED,
    INDEX ix_columnstore CLUSTERED COLUMNSTORE
  ) WITH (MEMORY_OPTIMIZED=ON)
```

## <a name="see-also"></a>另请参阅  
 [内存优化表的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
