---
title: sys.pdw_nodes_column_store_row_groups (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 17a4c925-d4b5-46ee-9cd6-044f714e6f0e
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 75e4229fde3cae66cdd2172c0f2bea0cbf63bf10
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwnodescolumnstorerowgroups-transact-sql"></a>sys.pdw_nodes_column_store_row_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  提供有关用于帮助管理员决定系统管理中的每个段基础聚集列存储索引信息[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 **sys.pdw_nodes_column_store_row_groups**具有以物理方式存储 （包括那些已标记为已删除） 的行的总数的列和标记为已删除的行数的列。 使用**sys.pdw_nodes_column_store_row_groups**若要确定哪些行组具有较高百分比的已删除的行，并应重新生成。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|基础表的 ID。 这是在计算节点上，不控制节点上的逻辑表的 object_id 的物理表。 与在 sys.tables object_id，例如，object_id 不匹配。<br /><br /> 若要使用 sys.tables 加入，请使用 sys.pdw_index_mappings。|  
|**index_id**|**int**|上的聚集列存储索引 ID *object_id*表。|  
|**partition_number**|**int**|包含行组的表分区 ID *row_group_id*。 你可以使用*partition_number* sys.partitions 中加入此 DMV。|  
|**row_group_id**|**int**|此行组 ID。 这在分区中是唯一的。|  
|**dellta_store_hobt_id**|**bigint**|delta 行组的 hobt_id；或如果行组类型不是 delta，则为 NULL。 delta 行组是正在接受新记录的读/写行组。 增量行组具有**打开**状态。 delta 行组仍采用行存储格式，并且尚未压缩成列存储格式。|  
|**状态**|**tinyint**|与 state_description 关联的 ID 号。<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED|  
|**state_desccription**|**nvarchar(60)**|行组的持久状态的说明：<br /><br /> OPEN – 正在接受新记录的读/写行组。 开放的行组仍采用行存储格式，并且尚未压缩成列存储格式。<br /><br /> CLOSED – 一个已填充的行组，但尚未由元组搬运者进程压缩。<br /><br /> COMPRESSED – 已填充和压缩的行组。|  
|**total_rows**|**bigint**|行组中物理存储的总行数。 一些行可能已删除，但它们仍被存储。 一个行组中的最大行数为 1,048,576（十六进制 FFFFF）。|  
|**deleted_rows**|**bigint**|以物理方式存储在行组标记为删除的行数。<br /><br /> 始终 0 增量行组。|  
|**size_in_bytes**|**int**|组合的大小 （字节），此行组中的所有页面。 此大小不包括存储元数据或共享的字典所需的大小。|  
|**pdw_node_id**|**int**|唯一 id[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]节点。|  
|**distribution_id**|**int**|分发的唯一 id。|
  
## <a name="remarks"></a>注释  
 针对每个表中具有聚合或非聚合列存储索引的每个列存储行组返回一行。  
  
 使用**sys.pdw_nodes_column_store_row_groups**来确定的行组和行组的大小中所含的行数。  
  
 当行组中的已删除行数量增长到占总行数的较大百分比时，该表的效率将下降。 重新生成列存储索引以减少表的大小，同时减少读取该表所需的磁盘 I/O。 若要重新生成列存储索引使用**重新生成**选项**ALTER INDEX**语句。  
  
 可更新列存储第一次将新数据插入**打开**行组，这是在行存储格式，并且有时也称为增量表。  一旦打开行组已满，其状态更改为**已关闭**。 元组发动机已关闭行组压缩到列存储格式和状态更改为**COMPRESSED**。  元组搬运者是一个后台进程，它定期唤醒并检查是否有任何关闭的行组正准备要压缩成列存储行组。  元组搬运者还取消分配其中已删除每个行的行组。 释放行组标记为**已停用**。 若要立即运行元组发动机，使用**重新组织**选项**ALTER INDEX**语句。  
  
 如果列存储行组已填充，它将进行压缩并停止接受新行。 当从压缩组中删除行时，这些行将保留但标记为已删除。 对压缩组的更新将实现为压缩组中的删除以及对打开组的插入。  
  
## <a name="permissions"></a>权限  
 需要**VIEW SERVER STATE**权限。  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例联接**sys.pdw_nodes_column_store_row_groups**表添加到其他系统表，以返回有关特定表的信息。 计算的 `PercentFull` 列是对行组效率的估计。 若要找到 WHERE 子句的前面的注释连字符的信息在单个表中删除，并提供一个表名。  
  
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

以下[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]示例计数的每个分区的行的聚集的列存储以及如何打开、 已关闭或 Compressed 行组中是多行：  

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
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [创建列存储索引 &#40;Transact SQL &#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  
