---
title: sys.pdw_nodes_column_store_row_groups (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 17a4c925-d4b5-46ee-9cd6-044f714e6f0e
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 458fd50e6387a2929e660deb81400fc79271ff20
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2018
ms.locfileid: "36874995"
---
# <a name="syspdwnodescolumnstorerowgroups-transact-sql"></a>sys.pdw_nodes_column_store_row_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  若要帮助管理员作出系统管理决策中的每个段基础上提供聚集列存储索引信息[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 **sys.pdw_nodes_column_store_row_groups**包含列 （包括那些已标记为已删除） 以物理方式存储的行的总数和标记为已删除的行数的列。 使用**sys.pdw_nodes_column_store_row_groups**来确定哪些行组具有较高百分比的已删除的行和应重新生成。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|基础表的 ID。 这是在计算节点上，不控制节点上的逻辑表的 object_id 的物理表。 例如，object_id 不会与在 sys.tables object_id 不匹配。<br /><br /> 若要加入 sys.tables，使用 sys.pdw_index_mappings。|  
|**index_id**|**int**|在聚集列存储索引的 ID *object_id*表。|  
|**partition_number**|**int**|包含行组的表分区的 ID *row_group_id*。 可以使用*partition_number*若要将此 DMV 联接到 sys.partitions。|  
|**row_group_id**|**int**|此行组的 ID。 这在分区中是唯一的。|  
|**dellta_store_hobt_id**|**bigint**|delta 行组的 hobt_id；或如果行组类型不是 delta，则为 NULL。 delta 行组是正在接受新记录的读/写行组。 Delta 行组具有**打开**状态。 delta 行组仍采用行存储格式，并且尚未压缩成列存储格式。|  
|State|**tinyint**|与 state_description 关联的 ID 号。<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED|  
|**state_desccription**|**nvarchar(60)**|行组的持久状态的说明：<br /><br /> OPEN – 正在接受新记录的读/写行组。 开放的行组仍采用行存储格式，并且尚未压缩成列存储格式。<br /><br /> CLOSED – 一个已填充的行组，但尚未由元组搬运者进程压缩。<br /><br /> COMPRESSED – 已填充和压缩的行组。|  
|**total_rows**|**bigint**|行组中物理存储的总行数。 一些行可能已删除，但它们仍被存储。 一个行组中的最大行数为 1,048,576（十六进制 FFFFF）。|  
|**deleted_rows**|**bigint**|以物理方式存储在行组标记为删除的行数。<br /><br /> 始终 0 表示增量行组。|  
|**size_in_bytes**|**int**|组合的大小 （字节），是此行组中的所有页。 此大小不包括所需存储元数据和共享的字典的大小。|  
|**pdw_node_id**|**int**|唯一 id[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]节点。|  
|**distribution_id**|**int**|分发的唯一 id。|
  
## <a name="remarks"></a>Remarks  
 针对每个表中具有聚合或非聚合列存储索引的每个列存储行组返回一行。  
  
 使用**sys.pdw_nodes_column_store_row_groups**以确定包含在行组和行组的大小的行数。  
  
 当行组中的已删除行数量增长到占总行数的较大百分比时，该表的效率将下降。 重新生成列存储索引以减少表的大小，同时减少读取该表所需的磁盘 I/O。 若要重新生成列存储索引使用**重新生成**的选项**ALTER INDEX**语句。  
  
 可更新列存储首先将新数据插入**打开**行组，这是采用行存储格式，有时也称为 delta 表。  一旦打开的行组已满，其状态更改为**已关闭**。 已关闭行组将由元组搬运者进程压缩为列存储格式和状态将变为**压缩**。  元组搬运者是一个后台进程，它定期唤醒并检查是否有任何关闭的行组正准备要压缩成列存储行组。  元组搬运者还取消分配其中已删除每个行的行组。 已解除分配的行组标记为**停用**。 若要立即运行元组搬运者进程，请使用**REORGANIZE**的选项**ALTER INDEX**语句。  
  
 如果列存储行组已填充，它将进行压缩并停止接受新行。 当从压缩组中删除行时，这些行将保留但标记为已删除。 对压缩组的更新将实现为压缩组中的删除以及对打开组的插入。  
  
## <a name="permissions"></a>权限  
 需要 VIEW SERVER STATE 权限。  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例联接**sys.pdw_nodes_column_store_row_groups**表与其他系统表，以返回有关特定表的信息。 计算的 `PercentFull` 列是对行组效率的估计。 若要查找有关单个表删除 WHERE 子句的前面的注释连字符，并提供表名。  
  
```  
SELECT IndexMap.object_id,   
  object_name(IndexMap.object_id) AS LogicalTableName,   
  i.name AS LogicalIndexName, IndexMap.index_id, NI.type_desc,   
  IndexMap.physical_name AS PhyIndexNameFromIMap,   
  CSRowGroups.*,  
  100*(ISNULL(deleted_rows,0))/total_rows AS PercentDeletedRows   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.pdw_index_mappings AS IndexMap  
    ON i.object_id = IndexMap.object_id  
    AND i.index_id = IndexMap.index_id  
JOIN sys.pdw_nodes_indexes AS NI  
    ON IndexMap.physical_name = NI.name  
    AND IndexMap.index_id = NI.index_id  
JOIN sys.pdw_nodes_column_store_row_groups AS CSRowGroups  
    ON CSRowGroups.object_id = NI.object_id   
    AND CSRowGroups.pdw_node_id = NI.pdw_node_id  
AND CSRowGroups.index_id = NI.index_id      
--WHERE t.name = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, IndexMap.physical_name, pdw_node_id;  
```  

以下[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]的示例计算每个分区的行，对于聚集的列存储以及如何打开、 已关闭或压缩行组有很多行：  

```
SELECT
    s.name AS [Schema Name]
    ,t.name AS [Table Name]
    ,rg.partition_number AS [Partition Number]
    ,SUM(rg.total_rows) AS [Total Rows]
    ,SUM(CASE WHEN rg.State = 1 THEN rg.Total_rows Else 0 END) AS [Rows in OPEN Row Groups]
    ,SUM(CASE WHEN rg.State = 2 THEN rg.Total_Rows ELSE 0 END) AS [Rows in Closed Row Groups]
    ,SUM(CASE WHEN rg.State = 3 THEN rg.Total_Rows ELSE 0 END) AS [Rows in COMPRESSED Row Groups]
FROM sys.pdw_nodes_column_store_row_groups rg
JOIN sys.pdw_nodes_tables pt
ON rg.object_id = pt.object_id AND rg.pdw_node_id = pt.pdw_node_id AND pt.distribution_id = rg.distribution_id
JOIN sys.pdw_table_mappings tm
ON pt.name = tm.physical_name
INNER JOIN sys.tables t
ON tm.object_id = t.object_id
INNER JOIN sys.schemas s
ON t.schema_id = s.schema_id
GROUP BY s.name, t.name, rg.partition_number
ORDER BY 1, 2
```
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [创建列存储索引&#40;Transact SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_segments &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  
