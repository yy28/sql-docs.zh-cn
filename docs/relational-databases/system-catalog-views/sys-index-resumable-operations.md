---
title: sys.index_resumable_operations (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 07/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: ''
caps.latest.revision: 1
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 0d68f6e0946f9b5fb781448b2973939831b6cab9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="indexresumableoperations-transact-sql"></a>index_resumable_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**sys.index_resumable_operations**是系统视图，用于监视并检查重建索引时可恢复的当前执行状态。  
**适用于**: SQL Server 自 2017 年和 Azure SQL 数据库 
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|此索引属于 (不可为 null) 的对象 ID。|  
|**index_id**|**int**|(不可为 null) 的索引 ID。 **index_id**仅在对象中是唯一。|
|**名称**|**sysname**|索引的名称。 **名称**仅在对象中是唯一。|  
|**sql_text**|**nvarchar(max)**|DDL T-SQL 的语句文本|
|**last_max_dop**|**int**|上次 MAX_DOP 使用 (默认值 = 0)|
|**partition_number**|**int**|拥有索引或堆中的分区号。 对于未分区表和索引或用例中的所有分区都正在此列的重新生成值为 NULL。|
|**状态**|**tinyint**|可恢复的索引的操作状态：<br /><br />0 = 运行<br /><br />1 = 暂停|
|**state_desc**|**nvarchar(60)**|可恢复的索引 （运行或暂停） 的操作状态的说明|  
|**start_time**|**datetime**|索引操作开始时间 (不可为 null)|
|**last_pause_time**|**datatime**| 索引操作 (可以为 null) 的最后一个暂停时间。 如果操作已运行，而绝不会暂停，则为 NULL。|
|**total_execution_time**|**int**|从以分钟为单位 (不可为 null) 的开始时间的总执行时间|
|**percent_complete**|**real**|索引操作在 %(不可为 null) 的进度自动补全。|
|**page_count**|**bigint**|由新的索引生成操作和映射索引 (不可为 null) 分配的索引页的总数。 

## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
   
## <a name="example"></a>示例  
 列出处于暂停状态的所有可恢复索引重新生成操作。 
  
```  
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```  
  
## <a name="see-also"></a>另请参阅 
 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)    
 [目录视图&#40;TRANSACT-SQL&#41; ](catalog-views-transact-sql.md) [对象目录视图&#40;TRANSACT-SQL&#41; ](object-catalog-views-transact-sql.md) [sys.indexes &#40;TRANSACT-SQL&#41; ](sys-xml-indexes-transact-sql.md) [sys.index_columns &#40;Transact SQL&#41;](sys-index-columns-transact-sql.md)   
 [sys.xml_indexes (Transact-SQL)](sys-xml-indexes-transact-sql.md)   
 [sys.objects (Transact-SQL)](sys-index-columns-transact-sql.md)   
 [sys.key_constraints &#40;Transact SQL&#41;](sys-key-constraints-transact-sql.md)   
 [sys.filegroups (Transact-SQL)](sys-filegroups-transact-sql.md)   
 [sys.partition_schemes (Transact-SQL)](sys-partition-schemes-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](querying-the-sql-server-system-catalog-faq.md)   
  
