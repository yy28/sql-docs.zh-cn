---
title: "sys.pdw_nodes_column_store_segments (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79944f54d12681ab7a430362ec0204a8d54bf477
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwnodescolumnstoresegments-transact-sql"></a>sys.pdw_nodes_column_store_segments (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  对于 columnstore 索引中的每列包括一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|指示分区 ID。 是一个数据库中唯一的。|  
|**hobt_id**|**bigint**|具有此 columnstore 索引的表的堆或 B 树 (hobt) 的 ID。|  
|**column_id**|**int**|列存储列的 ID。|  
|**segment_id**|**int**|列段的 ID。|  
|**version**|**int**|列段格式的版本。|  
|**encoding_type**|**int**|该段使用的编码类型。|  
|**row_count**|**int**|行组中的行数。|  
|**has_nulls**|**int**|1 如果列段具有 Null 值。|  
|**base_id**|**bigint**|如果编码类型 1 正在使用的基础值 id。  如果编码类型 1 未使用，base_id 设置为 1。|  
|**量值**|**float**|如果使用的编码类型 1 的量值。  如果编码类型 1 未使用，则将量值设置为 1。|  
|**primary__dictionary_id**|**int**|主字典的 ID。|  
|**secondary_dictionary_id**|**int**|辅助字典的 ID。 如果没有辅助字典，则返回 -1。|  
|**min_data_id**|**bigint**|列段中的最小数据 ID。|  
|**max_data_id**|**bigint**|列段中的最大数据 ID。|  
|**null_value**|**bigint**|用于表示 Null 的值。|  
|**on_disk_size**|**bigint**|段大小（字节）。|  
|**pdw_node_id**|**int**|唯一标识符[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]注意。|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下查询返回有关列存储索引各段的信息。  
  
```tsql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
```  
  
 加入 sys.pdw_nodes_column_store_segments 与其他系统表来确定的行计数和磁盘上的段大小。  
  
```  
SELECT o.name, css.hobt_id, css. column_id, css.pdw_node_id, css.row_count, css.on_disk_size  
FROM sys.pdw_nodes_column_store_segments AS css  
JOIN sys.pdw_nodes_partitions AS pnp  
    ON css.partition_id = pnp.partition_id  
JOIN sys.pdw_nodes_tables AS part  
    ON pnp.object_id = part.object_id   
    AND pnp.pdw_node_id = part.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON part.name = TMap.physical_name  
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
ORDER BY css.hobt_id, css.column_id;  
```  
  
## <a name="permissions"></a>Permissions  
 需要**VIEW SERVER STATE**权限。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [创建列存储索引 &#40;Transact SQL &#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  

