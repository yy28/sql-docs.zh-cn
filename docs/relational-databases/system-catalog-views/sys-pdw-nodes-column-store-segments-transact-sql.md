---
title: sys.pdw_nodes_column_store_segments (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/28/2018
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
author: hirokib
ms.author: elbutter
manager: jrj
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c98898560d4b2f523974065831f0d316a390f7b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682525"
---
# <a name="syspdwnodescolumnstoresegments-transact-sql"></a>sys.pdw_nodes_column_store_segments (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

对于 columnstore 索引中的每列包括一行。  

| 列名                 | 数据类型  | Description                                                  |
| --------------------------- | ---------- | ------------------------------------------------------------ |
| **partition_id**            | **bigint** | 指示分区 ID。 是在数据库中唯一。     |
| **hobt_id**                 | **bigint** | 具有此 columnstore 索引的表的堆或 B 树 (hobt) 的 ID。 |
| **column_id**               | **int**    | 列存储列的 ID。                                |
| **segment_id**              | **int**    | 列段的 ID。 对于向后兼容性，列名称会继续调用 segment_id 即使这是行组 id。 可唯一地标识段使用 < hobt_id、 partition_id、 column_id >，< segment_id >。 |
| **version**                 | **int**    | 列段格式的版本。                        |
| **encoding_type**           | **int**    | 使用该时间段的编码类型：<br /><br /> 1 = VALUE_BASED-非字符串/二进制与没有字典 （类似于具有某些内部变体 4）<br /><br /> 2 = VALUE_HASH_BASED-包含字典中的常见值字符串/二进制列<br /><br /> 3 = STRING_HASH_BASED-与字典中的常见值字符串/二进制列<br /><br /> 4 = STORE_BY_VALUE_BASED-非字符串/二进制与没有字典<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED-带有没有字典字符串/二进制文件<br /><br /> 所有编码都充分利用位打包和运行长度编码在可能的情况。 |
| **row_count**               | **int**    | 行组中的行数。                             |
| **has_nulls**               | **int**    | 1 如果列段具有 Null 值。                     |
| **base_id**                 | **bigint** | 如果使用的编码类型 1 的基值 ID。  如果未正在使用的编码类型 1，则 base_id 设置为 1。 |
| **量值**               | **float**  | 如果使用的编码类型 1 的量值。  如果未正在使用的编码类型 1，则将量值设置为 1。 |
| **primary__dictionary_id**  | **int**    | 主字典的 ID。 一个非零值将指向此列将在当前段 （即行组） 的本地字典。 值为-1 指示存在此段没有本地字典。 |
| **secondary_dictionary_id** | **int**    | 辅助字典的 ID。 一个非零值将指向此列将在当前段 （即行组） 的本地字典。 值为-1 指示存在此段没有本地字典。 |
| **min_data_id**             | **bigint** | 列段中的最小数据 ID。                       |
| **max_data_id**             | **bigint** | 列段中的最大数据 ID。                       |
| **null_value**              | **bigint** | 用于表示 Null 的值。                               |
| **on_disk_size**            | **bigint** | 段大小（字节）。                                    |
| **pdw_node_id**             | **int**    | 唯一标识符[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]节点。 |

## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

加入 sys.pdw_nodes_column_store_segments 和其他系统表来确定每个逻辑表的列存储段的数目。 

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

## <a name="permissions"></a>Permissions  
 需要 VIEW SERVER STATE 权限。  

## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [创建列存储索引&#40;Transact SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  

  

