---
title: sys.fulltext_indexes (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fulltext_indexes
- fulltext_indexes_TSQL
- sys.fulltext_indexes_TSQL
- sys.fulltext_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_indexes catalog view
- full-text indexes [SQL Server], properties
ms.assetid: 7fc10fdc-370f-4927-bba0-b76108a7508e
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 50f7333cd6bce024b4b85c9068c413c17719cd21
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysfulltextindexes-transact-sql"></a>sys.fulltext_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  表对象的每个全文索引各占一行。  

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|此全文索引所属的对象的 ID。|  
|**unique_index_id**|**int**|对应的唯一非全文索引的 ID，该索引用于将全文索引与行关联。|  
|**fulltext_catalog_id**|**int**|全文索引所在的全文目录的 ID。|  
|**is_enabled**|**bit**|1 = 当前已启用全文索引。|  
|**change_tracking_state**|**char(1)**|更改跟踪的状态。<br /><br /> M = 手动<br /><br /> A = 自动<br /><br /> O = 关闭|  
|**change_tracking_state_desc**|**nvarchar(60)**|对更改跟踪状态的说明。<br /><br /> MANUAL<br /><br /> AUTO<br /><br /> OFF|  
|**has_crawl_completed**|**bit**|全文索引完成的上一次爬网（填充）。|  
|**crawl_type**|**char(1)**|当前或上一次爬网的类型。<br /><br /> F = 完全爬网<br /><br /> I = 增量时间戳爬网<br /><br /> U = 基于通知的更新爬网<br /><br /> P = 完全爬网已暂停。|  
|**crawl_type_desc**|**nvarchar(60)**|对当前或上一次爬网类型的说明。<br /><br /> FULL_CRAWL<br /><br /> INCREMENTAL_CRAWL<br /><br /> UPDATE_CRAWL<br /><br /> PAUSED_FULL_CRAWL|  
|**crawl_start_date**|**datetime**|当前或上一次爬网的开始日期。<br /><br /> NULL = 无。|  
|**crawl_end_date**|**datetime**|当前或上一次爬网的结束日期。<br /><br /> NULL = 无。|  
|**incremental_timestamp**|**binary(8)**|要用于下一次增量爬网的时间戳值。<br /><br /> NULL = 无。|  
|**stoplist_id**|**int**|ID[非索引字表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)此全文索引与该键相关联。|  
|**data_space_id**|**int**|此全文索引所在的文件组。|  
|**property_list_id**|**int**|与此全文索引关联的搜索属性列表的 ID。 NULL 表示没有与全文索引关联的搜索属性列表。 若要获取有关此搜索属性列表的详细信息，请使用[sys.registered_search_property_lists &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)目录视图。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="examples"></a>示例  
 以下示例在 `HumanResources.JobCandidate` 示例数据库的 `AdventureWorks2012` 表中使用全文索引。 该示例返回表的对象 ID、搜索属性列表 ID 以及全文索引使用的非索引字表的非索引字表 ID。  
  
> [!NOTE]  
>  创建此全文索引中的代码示例，请参阅"示例"一节的[CREATE FULLTEXT INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT object_id, property_list_id, stoplist_id FROM sys.fulltext_indexes  
    where object_id = object_id('HumanResources.JobCandidate');   
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.fulltext_index_fragments &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)   
 [sys.fulltext_index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [sys.fulltext_index_catalog_usages &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)   
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [创建和管理全文索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [DROP FULLTEXT INDEX & #40;Transact SQL & #41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
