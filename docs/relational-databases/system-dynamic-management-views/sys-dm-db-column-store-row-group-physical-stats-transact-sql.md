---
title: sys.dm_db_column_store_row_group_physical_stats (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_column_store_row_group_physical_stats_TSQL
- sys.dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_column_store_row_group_physical_stats
- sys.dm_db_column_store_row_group_physical_stats dynamic management view
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9f48268c800345ed66f065e444a8d7cfe09a6a30
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdbcolumnstorerowgroupphysicalstats-transact-sql"></a>sys.dm_db_column_store_row_group_physical_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  提供有关当前数据库中的列存储索引的所有当前行组级信息。  
  
 这将扩展目录视图[sys.column_store_row_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|基础表的 ID。|  
|**index_id**|**int**|在此列存储索引的 ID *object_id*表。|  
|**partition_number**|**int**|包含的表分区 ID *row_group_id*。 您可以使用 partition_number 将此 DMV 联接到 sys.partitions。|  
|**row_group_id**|**int**|此行组 ID。 用于已分区表，这是在分区中是唯一的。<br /><br /> 内存中结尾-1。|  
|**delta_store_hobt_id**|**bigint**|有关增量存储中的行组 hobt_id。<br /><br /> 如果行组不在增量存储，则为 NULL。<br /><br /> 生成内存中表后半部分为空。|  
|**状态**|**tinyint**|关联的 ID 号*state_description*。<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = 逻辑删除<br /><br /> 压缩是适用于内存中表的唯一状态。|  
|**state_desc**|**nvarchar(60)**|行组状态的说明：<br /><br /> 正在生成不可见 – 行组。 例如： <br />列存储中的行组时压缩数据后，将不可见的。 完成压缩后的元数据交换机更改列存储行的状态发件人分组不可见 COMPRESSED、 和到逻辑删除从已关闭的增量存储行组的状态。<br /><br /> 打开 – 将会接受新行的增量存储行组。 开放的行组仍采用行存储格式，并且尚未压缩成列存储格式。<br /><br /> 关闭-包含最大行数并等待继续压缩到列存储元组发动机增量存储中的行组。<br /><br /> 压缩 – 使用列存储压缩进行压缩并且存储在列存储行组。<br /><br /> TOMBSTONE – 行组，先前增量存储中不再使用。|  
|**total_rows**|**bigint**|存储在行组中的物理行数。 对于压缩的行组，这包括标记为删除的行。|  
|**deleted_rows**|**bigint**|以物理方式存储在压缩的行组标记为删除的行数。<br /><br /> 0 表示的增量存储中的行组。|  
|**size_in_bytes**|**bigint**|组合的大小 （字节），此行组中的所有页面。 此大小不包括存储元数据或共享的字典所需的大小。|  
|**trim_reason**|**tinyint**|触发 COMPRESSED 行组拥有的原因小于最大行数。<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1-NO_TRIM<br /><br /> 2-BULKLOAD<br /><br /> 3 – REORG<br /><br /> 4 – DICTIONARY_SIZE<br /><br /> 5 – MEMORY_LIMITATION<br /><br /> 6 – RESIDUAL_ROW_GROUP<br /><br /> 7-STATS_MISMATCH<br /><br /> 8-溢出|  
|**trim_reason_desc**|**nvarchar(60)**|说明*trim_reason*。<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION： 从以前版本的升级时出现[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br /> 1-NO_TRIM： 不裁剪行组。 与 1,048,476 行的最大已压缩行组。  如果关闭增量行组后，已删除的行 subsset 的行数可能小于<br /><br /> 2 – BULKLOAD： 大容量负载批处理大小受限制行的数。<br /><br /> 3 – REORG： 强制压缩为 REORG 命令的一部分。<br /><br /> 4 – DICTIONARY_SIZE： 字典大小增长过大而无法压缩的所有行在一起。<br /><br /> 5 – MEMORY_LIMITATION： 不内存不足，无法压缩的所有行在一起。<br /><br /> 6 – RESIDUAL_ROW_GROUP： 最后一个行组的一部分行 < 1 万个操作期间关闭索引生成<br /><br /> STATS_MISMATCH： 仅对内存中表的列存储。 如果统计信息不正确地指示 > = 100 万个符合条件的行生成后半部分中，但我们找到较少，压缩行组将具有 < 1 百万行<br /><br /> 溢出： 仅对内存中表的列存储。 如果计数之间 100k 到 100 万次结尾具有 > 1 百万个符合条件的行，如果压缩的最后一个的批处理剩余行|  
|**transition_to_compressed_state**|tinyint|演示如何此行组移动了增量存储到列存储中的压缩状态。<br /><br /> 1-NOT_APPLICABLE<br /><br /> 2 – INDEX_BUILD<br /><br /> 3 – TUPLE_MOVER<br /><br /> 4 – REORG_NORMAL<br /><br /> 5 – REORG_FORCED<br /><br /> 6 个 BULKLOAD<br /><br /> 7-合并|  
|**transition_to_compressed_state_desc**|nvarchar(60)|NOT_APPLICABLE – 操作不适用于增量存储。 或者，然后再升级到压缩行组已[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]在这种情况下不保留的历史记录。<br /><br /> INDEX_BUILD – 索引创建或重新生成索引压缩行组。<br /><br /> TUPLE_MOVER – 在后台运行元组发动机压缩行组。 行组会从打开状态更改为已关闭后，将发生这种情况。<br /><br /> REORG_NORMAL – 重组操作，ALTER INDEX... 执行目录重组，已关闭行组从增量存储移到列存储。 元组发动机来得及移动行组之前，将出现此错误。<br /><br /> REORG_FORCED – 此行组的增量存储中打开和到列存储被迫，具有完整的行数。<br /><br /> BULKLOAD – 大容量加载操作不使用增量存储而直接压缩行组。<br /><br /> 合并 – 合并操作合并到此行组的一个或多个行组，然后执行列存储压缩。|  
|**has_vertipaq_optimization**|bit|通过重新排列的行组中的行的顺序，以实现更高的压缩，Vertipaq 优化改进了列存储压缩。 在大多数情况下，此优化自动发生。 有两种情况下不使用 Vertipaq 优化：<br/>  a. 增量行组将移到列存储和列存储索引中的上有一个或多个非聚集索引时这种情况下 Vertipaq 优化是已跳过要最大程度减少对映射索引中; 的更改<br/> b. 对于内存优化表的列存储索引。 <br /><br /> 0 = 否<br /><br /> 1 = 是|  
|**生成**|bigint|与此行组关联的行组生成。|  
|**created_time**|datetime2|创建此行组时的时钟时间。<br /><br /> NULL – 表示内存中表的列存储索引。|  
|**closed_time**|datetime2|此行组已关闭时的时钟时间。<br /><br /> NULL – 表示内存中表的列存储索引。|  
  
## <a name="results"></a>结果  
 返回当前数据库中的每个行组的一行。  
  
## <a name="permissions"></a>权限  
 需要以下权限：  
  
-   对表的 CONTROL 权限。  
  
-   对数据库拥有 VIEW DATABASE STATE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-calculate-fragmentaton-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>A. 计算 fragmentaton 来确定何时重新组织或重新生成列存储索引。  
 对于列存储索引，已删除的行的百分比是行组中的碎片很好地衡量。 当碎片是 20%或更多建议删除已删除的行。  有关示例，请参阅[列存储索引碎片整理](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)。  
  
 此示例将联接**sys.dm_db_column_store_row_group_physical_stats**与其他系统表，然后计算`Fragmentation`值作为当前数据库中每个行组的效率的估计值的列。     若要查找有关注释连字符前端中的单个表删除**其中**子句，并提供表名。  
  
```sql  
SELECT i.object_id,   
    object_name(i.object_id) AS TableName,   
    i.name AS IndexName,   
    i.index_id,   
    i.type_desc,   
    CSRowGroups.*,  
    100*(ISNULL(deleted_rows,0))/total_rows AS 'Fragmentation'  
FROM sys.indexes AS i  
JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id AND i.index_id = CSRowGroups.index_id   
-- WHERE object_name(i.object_id) = 'table_name'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询的 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [列存储索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_dictionaries &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
