---
title: semantickeyphrasetable (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semantickeyphrasetable
- semantickeyphrasetable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semantickeyphrasetable function
ms.assetid: d33b973a-2724-4d4b-aaf7-67675929c392
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1ac666af5ed24d526953dd8aa57c76871d2064f6
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52414484"
---
# <a name="semantickeyphrasetable-transact-sql"></a>semantickeyphrasetable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为与指定表中的指定列关联的关键短语返回包含零行、一行或多行的表。  
  
 可以在 SELECT 语句的 FROM 子句中像引用常规表名那样引用此行集函数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
SEMANTICKEYPHRASETABLE  
    (  
    table,  
    { column | (column_list) | * }  
     [ , source_key ]  
    )  
```  
  
##  <a name="Arguments"></a> 参数  
 **table**  
 启用全文和语义索引的表的名称。  
  
 此名称可由 1 到 4 个部分组成，但不允许使用远程服务器名称。  
  
 **column**  
 应为其返回结果的索引列的名称。 列必须启用语义索引。  
  
 **column_list**  
 指示由逗号分隔并括在括号中的多个列。 所有列都必须启用语义索引。  
  
 **\***  
 指示已启用语义索引的所有列都均包括在内。  
  
 **source_key**  
 请求特定行的结果的行的唯一键。  
  
 键隐式转换为尽可能与源表中的全文唯一键的类型。 可以将此键指定为一个常量或变量，但不能是表达式或标量子查询的结果。 如果省略 source_key，则返回所有行的结果。  
  
## <a name="table-returned"></a>返回的表  
 下表介绍此行集函数返回的关键短语的信息。  
  
|Column_name|类型|Description|  
|------------------|----------|-----------------|  
|**column_id**|**int**|从中对当前关键短语提取并编制索引的列的 ID。<br /><br /> 有关如何在列名称和 column_id 之间相互检索对方的详细信息，请参阅 COL_NAME 和 COLUMNPROPERTY 函数。|  
|**document_key**|**\***<br /><br /> 此键与源表中的唯一键的类型相匹配。|从中对当前关键短语进行索引的文档或行的唯一键值。|  
|**keyphrase**|**NVARCHAR**|在由 column_id 表示的列中找到的关键短语，与 document_key 指定的文档关联。|  
|**score**|**REAL**|一个相对值，用来表示此关键短语与索引列中同一文档的所有其他关键短语的关系。<br /><br /> 该值是范围 [0.0, 1.0] 中的小数值，较高的得分表示较高权重，1.0 是最理想的得分。|  
  
## <a name="general-remarks"></a>一般备注  
 有关详细信息，请参阅[使用语义搜索在文档中查找关键短语](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)。  
  
## <a name="metadata"></a>元数据  
 有关语义关键短语的提取和填充的信息和状态，请查询以下动态管理视图：  
  
-   [sys.dm_db_fts_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_index_population (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 需要对创建全文和语义搜索所基于的基表具有 SELECT 权限。  
  
## <a name="examples"></a>示例  
  
###  <a name="HowToTopPhrases"></a> 示例 1:查找特定文档中的最重要关键短语  
 以下示例从通过 @DocumentId 变量指定的文档中检索前 10 个关键短语，该变量位于 AdventureWorks 示例数据库的 Production.Document 表的 Document 列中。 @DocumentId 变量表示全文检索的键列的一个值。 **SEMANTICKEYPHRASETABLE** 函数使用索引查找替代表扫描高效检索这些结果。 此示例假定列已配置为进行全文和语义索引。  
  
```sql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
  
```  
  
###  <a name="HowToTopDocuments"></a> 示例 2:查找包含特定关键短语的最相关文档  
 以下示例从 AdventureWorks 示例数据库的 Production.Document 表的 Document 列中检索包含关键短语“Bracket”的前 25 个文档。 此示例假定列已配置为进行全文和语义索引。  
  
```sql  
SELECT TOP (25) DOC_TBL.DocumentID, DOC_TBL.DocumentSummary  
FROM Production.Document AS DOC_TBL  
    INNER JOIN SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document  
    ) AS KEYP_TBL  
ON DOC_TBL.DocumentID = KEYP_TBL.document_key  
WHERE KEYP_TBL.keyphrase = 'Bracket'  
ORDER BY KEYP_TBL.Score DESC;  
  
```  
  
  
