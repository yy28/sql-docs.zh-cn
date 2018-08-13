---
title: sys.dm_db_column_store_row_group_physical_stats (TRANSACT-SQL) |Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: a6eaa2759ac911f748da143dbd592abc5de066b9
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39533847"
---
# <a name="sysdmdbcolumnstorerowgroupphysicalstats-transact-sql"></a>sys.dm_db_column_store_row_group_physical_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  提供有关当前数据库中的列存储索引的所有当前行组级信息。  
  
 这可以扩展目录视图[sys.column_store_row_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|基础表的 ID。|  
|**index_id**|**int**|在此列存储索引的 ID *object_id*表。|  
|**partition_number**|**int**|保存的表分区的 ID *row_group_id*。 您可以使用 partition_number 将此 DMV 联接到 sys.partitions。|  
|**row_group_id**|**int**|此行组的 ID。 对于已分区表，这是在分区中是唯一的。<br /><br /> 对于内存中结尾为-1。|  
|**delta_store_hobt_id**|**bigint**|增量存储中的行组的 hobt_id。<br /><br /> 如果在增量存储行组不为 NULL。<br /><br /> 对于内存中表的结尾为 NULL。|  
|State|**tinyint**|关联的 ID 号*state_description*。<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = 逻辑删除<br /><br /> 压缩是适用于内存中表的唯一状态。|  
|**state_desc**|**nvarchar(60)**|行组状态的说明：<br /><br /> 正在生成不可见 – A 行组。 例如： <br />列存储中的行组是不可见，而在压缩数据。 完成压缩后的元数据开关更改列存储行的状态的组中不可见压缩，并从已关闭的增量存储行组的逻辑删除状态。<br /><br /> OPEN – 正在接受新行的增量存储行组。 开放的行组仍采用行存储格式，并且尚未压缩成列存储格式。<br /><br /> CLOSED – 包含的最大行数和正在等待元组搬运者进程压缩到列存储的增量存储区中的行组。<br /><br /> COMPRESSED – 已使用列存储压缩压缩并且存储在列存储中的行组。<br /><br /> TOMBSTONE – 的行组之前为增量存储中，不能使用。|  
|**total_rows**|**bigint**|存储在行组中的物理行数。 对于压缩的行组，这包括标记为删除的行。|  
|**deleted_rows**|**bigint**|以物理方式存储在压缩的行组标记为删除的行数。<br /><br /> 增量存储区中的行组为 0。|  
|**size_in_bytes**|**bigint**|组合的大小 （字节），是此行组中的所有页。 此大小不包括所需存储元数据和共享的字典的大小。|  
|**trim_reason**|**tinyint**|触发 COMPRESSED 行组具有的原因小于最大行数。<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1-NO_TRIM<br /><br /> 2-BULKLOAD<br /><br /> 3 – REORG<br /><br /> 4 – DICTIONARY_SIZE<br /><br /> 5 – MEMORY_LIMITATION<br /><br /> 6 – RESIDUAL_ROW_GROUP<br /><br /> 7-STATS_MISMATCH<br /><br /> 8-溢出|  
|**trim_reason_desc**|**nvarchar(60)**|说明*trim_reason*。<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION： 从以前版本的升级时出现[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br /> 1-NO_TRIM： 不剪裁行组。 最多 1,048,476 行进行压缩行组。  如果已关闭增量行组后，已删除的行 subsset 的行数可能小于<br /><br /> 2 – BULKLOAD： 大容量加载批次大小受限制行的数。<br /><br /> 3 – REORG： 强制压缩 REORG 命令的一部分。<br /><br /> 4 – DICTIONARY_SIZE： 字典大小增长过大而无法一起压缩所有行。<br /><br /> 5 – MEMORY_LIMITATION： 没有足够可用内存来一起压缩所有行。<br /><br /> 6 – RESIDUAL_ROW_GROUP： 作为最后一个行组的一部分行 < 1 万个期间关闭索引生成操作<br /><br /> STATS_MISMATCH： 仅对内存中表的列存储。 如果错误地指示统计信息 > = 1 百万个符合条件的行在生成后半部分中，但我们发现更少、 压缩行组将具有 < 1 百万个行<br /><br /> 溢出： 仅对内存中表的列存储。 如果尾部具有 > 1 百万个符合条件的行，最后一个批处理剩余行被压缩文件如果计数 100 k 和 1 百万个之间|  
|**transition_to_compressed_state**|TINYINT|演示如何此行移动了增量存储到列存储压缩状态。<br /><br /> 1-NOT_APPLICABLE<br /><br /> 2 – INDEX_BUILD<br /><br /> 3 – TUPLE_MOVER<br /><br /> 4 – REORG_NORMAL<br /><br /> 5 – REORG_FORCED<br /><br /> 6-BULKLOAD<br /><br /> 7-合并|  
|**transition_to_compressed_state_desc**|nvarchar(60)|NOT_APPLICABLE – 操作不适用于增量存储。 或者，在升级到之前已压缩行组[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]这种情况下不会保留在历史记录。<br /><br /> INDEX_BUILD – 索引创建或重新生成索引压缩行组。<br /><br /> TUPLE_MOVER – 在后台运行元组发动机压缩行组。 行组会开放状态更改为已关闭后，将发生这种情况。<br /><br /> REORG_NORMAL – 重组操作，ALTER INDEX... 执行目录重组，已关闭行组从增量存储移到列存储。 元组发动机来得及移动行组之前，将出现此错误。<br /><br /> REORG_FORCED – 此行组已在增量存储中打开并已强制到列存储中以前必须完整行数。<br /><br /> BULKLOAD – 大容量加载操作不使用增量存储而直接压缩行组。<br /><br /> 合并 – 合并操作合并到此行组的一个或多个行组，然后执行列存储压缩。|  
|**has_vertipaq_optimization**|bit|Vertipaq 优化通过重新排列来实现更高的压缩行组中的行的顺序来提高列存储压缩。 在大多数情况下，这种优化自动发生。 有两种情况下不使用 Vertipaq 优化：<br/>  A. 增量行组移到列存储和列存储索引-上有一个或多个非聚集索引时这种情况下 Vertipaq 优化会跳过以最大程度减少对映射索引中; 的更改<br/> B. 对于内存优化表的列存储索引。 <br /><br /> 0 = 否<br /><br /> 1 = 是|  
|**生成**|BIGINT|与此行组相关联的行组生成。|  
|**created_time**|datetime2|创建此行组时的时钟时间。<br /><br /> NULL – 表示内存中表的列存储索引。|  
|**closed_time**|datetime2|此行已关闭时的时钟时间。<br /><br /> NULL – 表示内存中表的列存储索引。|  
  
## <a name="results"></a>结果  
 返回当前数据库中的每个行组的一行。  
  
## <a name="permissions"></a>Permissions  
 需要以下权限：  
  
-   表具有 CONTROL 权限。  
  
-   对数据库的 VIEW DATABASE STATE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-calculate-fragmentaton-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>A. 计算 fragmentaton 决定何时重新组织或重新生成列存储索引。  
 对于列存储索引的已删除的行的百分比是行组中的碎片的良好度量值。 当碎片是 20%或更多建议删除已删除的行。  有关示例，请参阅[列存储索引碎片整理](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)。  
  
 此示例联接**sys.dm_db_column_store_row_group_physical_stats**与其他系统表，然后计算`Fragmentation`列作为当前数据库中每个行组效率的估计值。     若要查找有关单个表删除的注释连字符的前面**其中**子句，并提供表名称。  
  
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
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [列存储索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_dictionaries &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
