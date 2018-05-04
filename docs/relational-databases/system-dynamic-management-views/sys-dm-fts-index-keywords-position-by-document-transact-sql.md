---
title: sys.dm_fts_index_keywords_position_by_document (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document
- sys.dm_fts_index_keywords_position_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords_position_by_document dynamic management view
ms.assetid: 0d70184f-baa2-411b-a32d-a4c5af890edd
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4d840c039684b544e5e892b1251af7c185c701ef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmftsindexkeywordspositionbydocument-transact-sql"></a>sys.dm_fts_index_keywords_position_by_document (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回在索引文档中的关键字的位置信息。  
  
## <a name="syntax"></a>语法  
  
```  
sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>参数  
 db_id('*database_name*')  
 调用[db_id （)](../../t-sql/functions/db-id-transact-sql.md)函数。 此函数接受的数据库名称，并返回哪些 sys.dm_fts_index_keywords_position_by_document 用于查找指定的数据库的数据库 ID。  
  
 object_id('*table_name*')  
 调用[OBJECT_ID()](../../t-sql/functions/object-id-transact-sql.md)函数。 此函数接受表名，并返回包含要检查的全文索引的表的表 ID。  
  
## <a name="table-returned"></a>返回的表  
  
|列|数据类型|Description|  
|------------|---------------|-----------------|  
|关键字 (keyword)|**varbinary(128)**|二进制字符串，表示关键字。|  
|display_term|**nvarchar(4000)**|关键字的可读格式。 此格式是从全文索引中存储的内部格式派生的。|  
|column_id|**int**|从中对当前关键字进行全文索引的列的 ID。|  
|document_id|**bigint**|从中对当前字词进行全文索引的文档或行的 ID。 此 ID 对应于该文档或行的全文键值。|  
|position|**int**|关键字的文档中的位置。|  
  
## <a name="remarks"></a>注释  
 使用 DMV 来确定在索引文档中的索引字的位置。 此 DMV 可以用于排除问题时**sys.dm_fts_index_keywords_by_document**指示的单词是在全文索引中，但当你运行一个查询使用这些词，则不返回文档。  
  
## <a name="permissions"></a>权限  
 要求具有全文索引涵盖的列的 SELECT 权限以及 CREATE FULLTEXT CATALOG 权限。  
  
## <a name="examples"></a>示例  
 下面的示例返回的全文索引中的关键字`Production.Document`表`AdventureWorks`示例数据库。  
  
```  
USE AdventureWorks2012;  
GO   
  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
);   
GO  
```  
  
 你可以在其他 columns_id 如下面的示例查询，若要进一步隔离位置中添加谓词。  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
)  
WHERE document_id = 7 AND display_term = 'performance';  
```  
  
## <a name="see-also"></a>另请参阅  
 [全文搜索](../../relational-databases/search/full-text-search.md)   
 [改进全文索引的性能](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [全文搜索和语义搜索函数&#40;Transact SQL&#41;](../../relational-databases/system-functions/full-text-search-and-semantic-search-functions-transact-sql.md)   
 [全文搜索和语义搜索动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文搜索和语义搜索存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [使用搜索属性列表搜索文档属性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.dm_fts_index_keywords_by_document (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
