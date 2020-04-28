---
title: sys. column_store_segments （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 01/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_store_segments
- sys.column_store_segments_TSQL
- sys.column_store_segments
- column_store_segments_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_segments catalog view
ms.assetid: 1253448c-2ec9-4900-ae9f-461d6b51b2ea
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b8d476e2f21693254eac5fc4712d53ac854e74ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68140004"
---
# <a name="syscolumn_store_segments-transact-sql"></a>sys.column_store_segments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

为列存储索引中的每个列段返回一行。 每个行组的每个列都有一个列段。 例如，具有10行组和34列的表将返回340行。 
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|指示分区 ID。 在数据库中是唯一的。|  
|**hobt_id**|**bigint**|具有此 columnstore 索引的表的堆或 B 树 (hobt) 的 ID。|  
|**column_id**|**int**|列存储列的 ID。|  
|**segment_id**|**int**|行组的 ID。 为实现向后兼容性，即使这是行组 ID，列名仍将继续 segment_id 调用。 您可以使用\<hobt_id、partition_id、column_id> <segment_id> 来唯一标识段。|  
|**version**|**int**|列段格式的版本。|  
|**encoding_type**|**int**|用于该段的编码类型：<br /><br /> 1 = 不带字典的 VALUE_BASED 非字符串/二进制（与4具有一些内部变体）<br /><br /> 2 = 在字典中具有通用值的 VALUE_HASH_BASED 非字符串/二进制列<br /><br /> 3 = STRING_HASH_BASED 字典中包含通用值的字符串/二进制列<br /><br /> 4 = 不带字典的 STORE_BY_VALUE_BASED 非字符串/二进制<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED 字符串/二进制，无字典<br /><br /> 如果可能，所有编码都利用位打包和长度为长度的编码。|  
|**row_count**|**int**|行组中的行数。|  
|**has_nulls**|**int**|1 如果列段具有 Null 值。|  
|**base_id**|**bigint**|如果正在使用编码类型1，则为基值 id。  如果未使用编码类型1，则 base_id 设置为-1。|  
|**magnitude**|**float**|如果正在使用编码类型1，则为数量级。  如果未使用编码类型1，则数量级设置为-1。|  
|**primary_dictionary_id**|**int**|值0表示全局字典。 值-1 指示没有为此列创建全局字典。|  
|**secondary_dictionary_id**|**int**|如果为非零值，则指向当前段（即行组）中此列的本地字典。 值-1 指示此段没有本地字典。|  
|**min_data_id**|**bigint**|列段中的最小数据 ID。|  
|**max_data_id**|**bigint**|列段中的最大数据 ID。|  
|**null_value**|**bigint**|用于表示 Null 的值。|  
|**on_disk_size**|**bigint**|段大小（字节）。|  
  
## <a name="remarks"></a>备注  
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
 所有列都要求至少对表具有**VIEW DEFINITION**权限。 以下各列将返回 null，除非用户也具有**SELECT**权限： has_nulls、base_id、数量级、min_data_id、max_data_id 和 null_value。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;的对象目录视图](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. all_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys. computed_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [列存储索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md)    
 [sys.column_store_dictionaries (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
  

