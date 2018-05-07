---
title: sys.fulltext_stoplists (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fulltext_stoplists
- sys.fulltext_stoplists_TSQL
- fulltext_stoplists_TSQL
- fulltext_stoplists
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- sys.fulltext_stoplists catalog view
- stopwords [full-text search]
ms.assetid: eb69fb8f-f6d9-446e-83c0-67afd05dfba0
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2ab58541738654f6ffd8aedada56b31f9817cc1b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysfulltextstoplists-transact-sql"></a>sys.fulltext_stoplists (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  对于数据库中的每个全文非索引字表，均存在对应的一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**stoplist_id**|**int**|非索引字表的 ID；在数据库中唯一。|  
|**名称**|**sysname**|非索引字表的名称。|  
|**create_date**|**datetime**|非索引字表的创建日期。|  
|**modify_date**|**datetime**|上次使用任意 ALTER 语句修改非索引字表的日期。|  
|**Principal_id**|**int**|拥有此非索引字表的数据库主体的 ID。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.fulltext_system_stopwords &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-system-stopwords-transact-sql.md)   
 [sys.fulltext_stopwords (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [为配置和管理非索引字和非索引字表的全文搜索](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [创建全文非索引字表 & #40;Transact SQL & #41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [ALTER FULLTEXT STOPLIST & #40;Transact SQL & #41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST (Transact-SQL)](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)  
  
  
