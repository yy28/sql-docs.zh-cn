---
title: sys.pdw_nodes_column_store_segments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2018
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
caps.latest.revision: 9
author: hirokib
ms.author: elbutter;barbkess
manager: jrj
ms.workload: Inactive
ms.openlocfilehash: 8e3daa47eea78bb90c736a42e7e541bea62e5ac4
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="syspdwnodescolumnstoresegments-transact-sql"></a>sys.pdw_nodes_column_store_segments (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

对于 columnstore 索引中的每列包括一行。  

| 列名                 | 数据类型  | Description                                                  |
| --------------------------- | ---------- | ------------------------------------------------------------ |
| **partition_id**            | **bigint** | 指示分区 ID。 是一个数据库中唯一的。     |
| **hobt_id**                 | **bigint** | 具有此 columnstore 索引的表的堆或 B 树 (hobt) 的 ID。 |
| **column_id**               | **int**    | 列存储列的 ID。                                |
| **segment_id**              | **int**    | 列段的 ID。 为了向后兼容，列名称将继续调用 segment_id 即使这是行组 id。 你可唯一地标识使用 < hobt_id、 partition_id、 column_id > 段 < segment_id >。 |
| **version**                 | **int**    | 列段格式的版本。                        |
| **encoding_type**           | **int**    | 为该片段所使用的编码类型：<br /><br /> 1 = VALUE_BASED-非字符串/二进制与没有字典 （类似于 4 个，带有一些内部的变体）<br /><br /> 2 = VALUE_HASH_BASED-与字典中的常见值字符串/二进制列<br /><br /> 3 = STRING_HASH_BASED-与字典中的常见值字符串/二进制列<br /><br /> 4 = STORE_BY_VALUE_BASED-非字符串/二进制与没有字典<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED-字符串/二进制没有字典<br /><br /> 所有编码的位装箱和运行长度编码尽可能都利用。 |
| **row_count**               | **int**    | 行组中的行数。                             |
| **has_nulls**               | **int**    | 1 如果列段具有 Null 值。                     |
| **base_id**                 | **bigint** | 如果使用的编码类型 1 的基础值 ID。  如果编码类型 1 未使用，base_id 设置为 1。 |
| **magnitude**               | **float**  | 如果使用的编码类型 1 的量值。  如果编码类型 1 未使用，则将量值设置为 1。 |
| **primary__dictionary_id**  | **int**    | 主要字典的 ID。 一个非零值到本地字典中此列将在当前段 （即行组） 的点。 值-1 指示没有为此段没有本地字典。 |
| **secondary_dictionary_id** | **int**    | 辅助字典中的 ID。 一个非零值到本地字典中此列将在当前段 （即行组） 的点。 值-1 指示没有为此段没有本地字典。 |
| **min_data_id**             | **bigint** | 中的列段的最小数据 ID。                       |
| **max_data_id**             | **bigint** | 中的列段的最大数据 ID。                       |
| **null_value**              | **bigint** | 用于表示 Null 的值。                               |
| **on_disk_size**            | **bigint** | 段大小（字节）。                                    |
| **pdw_node_id**             | **int**    | 唯一标识符[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]节点。 |

## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

加入 sys.pdw_nodes_column_store_segments 与其他系统表来确定的每个逻辑表的列存储段的数目。 

```sql
SELECT  sm.name           as schema_nm
,       tb.name           as table_nm
,       nc.name           as col_nm
,       nc.column_id
,       COUNT(*)          as segment_count
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb                   ON  sm.[schema_id]          = tb.[schema_id]
JOIN    sys.[pdw_table_mappings] mp       ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt         ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[pdw_nodes_partitions] np     ON  np.[object_id]          = nt.[object_id]
                                          AND np.[pdw_node_id]        = nt.[pdw_node_id]
                                          AND np.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_nodes_columns] nc        ON  np.[object_id]          = nc.[object_id]
                                          AND np.[pdw_node_id]        = nc.[pdw_node_id]
                                          AND np.[distribution_id]    = nc.[distribution_id]
JOIN    sys.[pdw_nodes_column_store_segments] rg  ON  rg.[partition_id]         = np.[partition_id]
                                                      AND rg.[pdw_node_id]      = np.[pdw_node_id]
                                                      AND rg.[distribution_id]  = np.[distribution_id]
                                                      AND rg.[column_id]        = nc.[column_id]
GROUP BY    sm.name
,           tb.name
,           nc.name
,           nc.column_id  
ORDER BY    table_nm
,           nc.column_id
,           sm.name
```

## <a name="permissions"></a>权限  
 需要 VIEW SERVER STATE 权限。  

## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [创建列存储索引&#40;Transact SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  

  

