---
title: sys.dm_fts_index_keywords_by_document (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_by_document_TSQL
- dm_fts_index_keywords_by_document_TSQL
- sys.dm_fts_index_keywords_by_document
- dm_fts_index_keywords_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- sys.dm_fts_index_keywords_by_document dynamic management function
- full-text search [SQL Server], viewing keywords
ms.assetid: 793b978b-c8a1-428c-90c2-a3e49d81b5c9
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: a6123e0aa41e3fa7210059897c89afa6dafb2ffa
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39532617"
---
# <a name="sysdmftsindexkeywordsbydocument-transact-sql"></a>sys.dm_fts_index_keywords_by_document (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  返回与指定表关联的全文索引的文档级内容的相关信息。  
  
 sys.dm_fts_index_keywords_by_document 是动态管理函数。  
  
 **若要查看更高级别的全文索引信息**  
  
-   [sys.dm_fts_index_keywords (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
 **若要查看有关属性级内容的信息与文档属性**  
  
-   [sys.dm_fts_index_keywords_by_property (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.dm_fts_index_keywords_by_document  
(   
    DB_ID('database_name'),     OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>参数  
 db_id('*database_name*')  
 调用[db_id （)](../../t-sql/functions/db-id-transact-sql.md)函数。 此函数接受数据库名称并返回数据库 ID，sys.dm_fts_index_keywords_by_document 使用此 ID 来查找指定的数据库。 如果省略 database_name，则返回当前数据库 ID。  
  
 object_id('*table_name*')  
 调用[object_id （)](../../t-sql/functions/object-id-transact-sql.md)函数。 此函数接受表名，并返回包含要检查的全文索引的表的表 ID。  
  
## <a name="table-returned"></a>返回的表  
  
|“列”|数据类型|Description|  
|------------|---------------|-----------------|  
|关键字 (keyword)|**nvarchar(4000)**|存储在全文索引中的关键字的十六进制表示形式。<br /><br /> 注意： OxFF 表示指示文件或数据集的末尾的特殊字符。|  
|display_term|**nvarchar(4000)**|关键字的可读格式。 此格式是从全文索引中存储的内部格式派生的。<br /><br /> 注意： OxFF 表示指示文件或数据集的末尾的特殊字符。|  
|column_id|**int**|从中对当前关键字进行全文索引的列的 ID。|  
|document_id|**int**|从中对当前字词进行全文索引的文档或行的 ID。 此 ID 对应于该文档或行的全文键值。|  
|occurrence_count|**int**|中的文档或所指示的行的当前关键字的次数**document_id**。 当 '*search_property_name*occurrence_count 显示仅当前关键字的匹配项中的指定的搜索属性中的文档或行的指定。|  
  
## <a name="remarks"></a>Remarks  
 sys.dm_fts_index_keywords_by_document 返回的信息有助于确定以下信息（但不仅限于此）：  
  
-   全文索引包含的关键字的总数。  
  
-   关键字是否为给定文档或行的一部分。  
  
-   关键字在整个全文索引中出现了多少次，即：  
  
     ([总和](../../t-sql/functions/sum-transact-sql.md)(**occurrence_count**) 其中**关键字**=*keyword_value* )  
  
-   关键字在给定文档或行中出现了多少次。  
  
-   给定文档或行中包含多少关键字。  
  
 另外，还可以使用 sys.dm_fts_index_keywords_by_document 提供的信息来检索属于给定文档或行的所有关键字。  
  
 如果全文键列是建议的整数数据类型，则 document_id 直接映射到基表中的全文键值。  
  
 相反，如果全文键列使用非整数数据类型，document_id 并不表示基表中的全文键。 在这种情况下，若要标识基表中 dm_fts_index_keywords_by_document 返回的行，您需要将此视图与返回的结果联接[sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)。 在联接它们之前，您必须将存储过程的输出存储在临时表中。 然后，可以将 dm_fts_index_keywords_by_document 的 document_id 列与此存储过程返回的 DocId 列联接在一起。 请注意，**时间戳**列不能在插入时，接收值，因为它们是由自动生成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 因此，**时间戳**列必须转换为**varbinary(8)** 列。 下面的示例说明了这些步骤。 在此示例中， *table_id*是您的表的 ID *database_name*是你的数据库的名称并*table_name*是表的名称。  
  
```  
USE database_name;  
GO  
CREATE TABLE #MyTempTable   
   (  
      docid INT PRIMARY KEY ,  
      [key] INT NOT NULL  
   );  
DECLARE @db_id int = db_id(N'database_name');  
DECLARE @table_id int = OBJECT_ID(N'table_name');  
INSERT INTO #MyTempTable EXEC sp_fulltext_keymappings @table_id;  
SELECT * FROM sys.dm_fts_index_keywords_by_document   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>Permissions  
 要求具有全文索引涵盖的列的 SELECT 权限以及 CREATE FULLTEXT CATALOG 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-displaying-full-text-index-content-at-the-document-level"></a>A. 在文档级别显示全文索引内容  
 下面的示例显示 `HumanResources.JobCandidate` 示例数据库中的 `AdventureWorks2012` 表的文档级全文索引内容。  
  
> [!NOTE]  
>  可以通过执行为提供的示例创建此索引`HumanResources.JobCandidate`表中[CREATE FULLTEXT INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)。  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_by_document(db_id('AdventureWorks'),   
object_id('HumanResources.JobCandidate'));  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [全文搜索和语义搜索动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文搜索](../../relational-databases/search/full-text-search.md)   
 [sys.dm_fts_index_keywords &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [sp_fulltext_keymappings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [改进全文索引的性能](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)  
  
  
