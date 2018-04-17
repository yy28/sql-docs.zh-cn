---
title: semanticsimilaritydetailstable (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- semanticsimilaritydetailstable
- semanticsimilaritydetailstable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritydetailstable function
ms.assetid: 038d751a-fca5-4b4c-9129-cba741a4e173
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 376c644ebeab414cc9f3cf93a56b449f2669be5b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="semanticsimilaritydetailstable-transact-sql"></a>semanticsimilaritydetailstable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回一个表，该表包含其内容在语义上相似的两个文档（源文档和匹配的文档）共有的关键短语的零个、一个或多个行。  
  
 可以在 SELECT 语句的 FROM 子句中引用此行集函数 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
SEMANTICSIMILARITYDETAILSTABLE  
    (  
    table,  
    source_column,  
    source_key,  
    matched_column,  
    matched_key  
    )  
```  
  
##  <a name="Arguments"></a> 参数  
 **table**  
 启用全文和语义索引的表的名称。  
  
 此名称可由 1 到 4 个部分组成，但不允许使用远程服务器名称。  
  
 **source_column**  
 源行中包含要比较相似性的内容的列的名称。  
  
 **source_key**  
 表示源文档的行的唯一键。  
  
 此键将尽可能隐式转换为源表中的全文唯一键的类型。 可以将此键指定为一个常量或变量，但不能是表达式或标量子查询的结果。 如果指定了无效键，则不返回任何行。  
  
 **matched_column**  
 匹配的行中包含要比较相似性的内容的列的名称。  
  
 **matched_key**  
 表示匹配文档的行的唯一键。  
  
 此键将尽可能隐式转换为源表中的全文唯一键的类型。 可以将此键指定为一个常量或变量，但不能是表达式或标量子查询的结果。  
  
## <a name="table-returned"></a>返回的表  
 下表介绍此行集函数返回的关键短语的信息。  
  
|Column_name|类型|Description|  
|------------------|----------|-----------------|  
|**keyphrase**|**NVARCHAR**|在源文档和匹配文档之间促进相似性的关键短语。|  
|**score**|**REAL**|一个相对值，用来表示此关键短语与两篇文档间相似的所有其他关键短语的关系。<br /><br /> 该值是范围 [0.0, 1.0] 中的小数值，较高的得分表示较高权重，1.0 是最理想的得分。|  
  
## <a name="general-remarks"></a>一般备注  
 有关详细信息，请参阅[查找相似和相关文档使用语义搜索](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)。  
  
## <a name="metadata"></a>元数据  
 有关语义相似性的提取和填充的信息和状态，请查询以下动态管理视图：  
  
-   [sys.dm_db_fts_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 需要对创建全文和语义搜索所基于的基表具有 SELECT 权限。  
  
## <a name="examples"></a>示例  
 下面的示例检索 5 个关键短语具有最高的相似性得分中指定的候选人间**HumanResources.JobCandidate** AdventureWorks2012 示例数据库的表。 @CandidateId和@MatchedID变量表示全文索引的键列的值。  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROMSEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
