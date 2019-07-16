---
title: sys.hash_indexes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.hash_indexes_TSQL
- hash_indexes
- sys.hash_indexes
- hash_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.hash_indexes catalog view
ms.assetid: d9e230fb-d3ff-486f-86ef-44898f0a703e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 99e3a647c55380e1731b97c267eb754a1f3c6a32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122744"
---
# <a name="syshashindexes-transact-sql"></a>sys.hash_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示当前哈希索引和哈希索引属性。 仅对支持哈希索引[内存中 OLTP&#40;内存中优化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
 Sys.hash_indexes 视图包含与 sys.indexes 视图相同的列和名为的其他列**bucket_count**。 有关在 sys.hash_indexes 视图中的其他列的详细信息，请参阅[sys.indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**||继承中的列[sys.indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。|  
|**bucket_count**|**int**|哈希索引的哈希存储桶计数。<br /><br /> 有关 bucket_count 值，包括指导原则设置值，请参阅[CREATE TABLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>示例  
  
```  
SELECT object_name([object_id]) AS 'table_name', [object_id],  
     [name] AS 'index_name', [type_desc], [bucket_count]   
FROM sys.hash_indexes   
WHERE OBJECT_NAME([object_id]) = 'T1';  
```  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
