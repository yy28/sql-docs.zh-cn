---
title: "sys.column_store_segments (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/15/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- column_store_segments
- sys.column_store_segments_TSQL
- sys.column_store_segments
- column_store_segments_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.column_store_segments catalog view
ms.assetid: 1253448c-2ec9-4900-ae9f-461d6b51b2ea
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f73379d3ae23570f95209631444d1335279a5ef5
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="syscolumnstoresegments-transact-sql"></a>sys.column_store_segments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

列存储索引中返回的每个列段的一行。 没有每个每个行的列的一个列段。 例如，具有 10 行组和 34 列的表返回 340 行。 
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|指示分区 ID。 是一个数据库中唯一的。|  
|**hobt_id**|**bigint**|具有此 columnstore 索引的表的堆或 B 树 (hobt) 的 ID。|  
|**column_id**|**int**|列存储列的 ID。|  
|**segment_id**|**int**|Rowgroup 的 ID。 为了向后兼容，列名称将继续调用 segment_id 即使这是行组 id。 你可唯一地标识段使用\<hobt_id，partition_id，column_id >，< segment_id >。|  
|**version**|**int**|列段格式的版本。|  
|**encoding_type**|**int**|为该片段所使用的编码类型：<br /><br /> 1 = VALUE_BASED-非字符串/二进制与没有字典 （非常类似于 4 个，带有一些内部的变体）<br /><br /> 2 = VALUE_HASH_BASED-与字典中的常见值字符串/二进制列<br /><br /> 3 = STRING_HASH_BASED-与字典中的常见值字符串/二进制列<br /><br /> 4 = STORE_BY_VALUE_BASED-非字符串/二进制与没有字典<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED-字符串/二进制没有字典<br /><br /> 所有编码的位装箱和运行长度编码尽可能都利用。|  
|**row_count**|**int**|行组中的行数。|  
|**has_nulls**|**int**|1 如果列段具有 Null 值。|  
|**base_id**|**bigint**|如果编码类型 1 正在使用的基础值 id。  如果编码类型 1 未使用，则将 base_id 设置为-1。|  
|**magnitude**|**float**|如果使用的编码类型 1 的量值。  如果编码类型 1 未使用，则将量值设置为-1。|  
|**primary_dictionary_id**|**int**|值为 0 表示全局字典。 值-1 指示没有为此列创建没有全局字典。|  
|**secondary_dictionary_id**|**int**|一个非零值到本地字典中此列将在当前段 （即行组） 的点。 值-1 指示没有为此段没有本地字典。|  
|**min_data_id**|**bigint**|列段中的最小数据 ID。|  
|**max_data_id**|**bigint**|列段中的最大数据 ID。|  
|**null_value**|**bigint**|用于表示 Null 的值。|  
|**on_disk_size**|**bigint**|段大小（字节）。|  
  
## <a name="remarks"></a>注释  
 以下查询返回有关列存储索引各段的信息。  
  
```sql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 5 OR i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
GO  
```  
  
## <a name="permissions"></a>权限  
 所有列至少都需要**VIEW DEFINITION**对表的权限。 下面的列返回 null，除非用户还必须**选择**权限： has_nulls，base_id，magnitude、 min_data_id、 max_data_id 和 null_value。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询的 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [列存储索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md)    
 [sys.column_store_dictionaries (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
  

