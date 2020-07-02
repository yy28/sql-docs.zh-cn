---
title: sys. column_store_dictionaries （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.column_store_dictionaries_TSQL
- column_store_dictionaries
- column_store_dictionaries_TSQL
- sys.column_store_dictionaries
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_dictionaries catalog view
ms.assetid: 56efd563-2f72-4caf-94e3-8a182385c173
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e7ccd7c93d42cb30eeb2fc24b79c358d519579b6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764764"
---
# <a name="syscolumn_store_dictionaries-transact-sql"></a>sys.column_store_dictionaries (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  xVelocity 内存优化的列存储索引中使用的每个字典各占一行。 字典用于对某些而非全部数据类型进行编码，因此并非列存储索引中的所有列都有字典。 字典可以作为主字典存在（对于所有段），也可能作为用于部分列段的其他辅助字典存在。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**hobt_id**|**bigint**|具有此列存储索引的表的堆或B 树索引（HoBT）的 ID。|  
|**column_id**|**int**|以1开头的列存储列的 ID。 第一列的 ID 为1，第二列的 ID = 2，等等。|  
|**dictionary_id**|**int**|可以有两种类型的字典：全局和本地，与列段关联。 Dictionary_id 为0表示在所有列段之间共享的全局字典（每个行组对应一个行组）。|  
|**version**|**int**|字典格式的版本。|  
|**type**|**int**|字典类型：<br /><br /> 1-包含**int**值的哈希字典<br /><br /> 2-未使用<br /><br /> 3-包含字符串值的哈希字典<br /><br /> 包含**浮点**值的4哈希字典<br /><br /> 有关字典的详细信息，请参阅[列存储索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md)。|  
|**last_id**|**int**|字典中的最后一个数据 ID。|  
|**entry_count**|**bigint**|字典中的条目数。|  
|**on_disk_size**|**bigint**|字典大小（以字节为单位）。|  
|**partition_id**|**bigint**|指示分区 ID。 在数据库中是唯一的。|  
  
## <a name="permissions"></a>权限  
要求对表具有 `VIEW DEFINITION` 权限。 以下各列将返回 null，除非用户也具有 `SELECT` 权限： last_id、entry_count data_ptr。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;的对象目录视图](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. all_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys. computed_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [列存储索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [列存储索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_segments (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

