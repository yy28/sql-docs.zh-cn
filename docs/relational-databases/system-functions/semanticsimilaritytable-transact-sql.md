---
title: semanticsimilaritytable (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- semanticsimilaritytable
- semanticsimilaritytable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritytable function
ms.assetid: b49d40ab-7552-438b-ad67-6237dcccb75b
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8b6b4b36580c35aead16780f4ada0f461dd58754
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="semanticsimilaritytable-transact-sql"></a>semanticsimilaritytable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为指定列中其内容在语义上类似于指定文档的那些文档返回具有零个、一个或多个行的表。  
  
 可以在 SELECT 语句的 FROM 子句中像引用常规表名那样引用此行集函数。  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
SEMANTICSIMILARITYTABLE  
    (  
    table,  
    { column | (column_list) | * },  
    source_key  
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
  
 在使用密钥隐式转换为尽可能与源表中的全文唯一键的类型。 可以将此键指定为一个常量或变量，但不能是表达式或标量子查询的结果。  
  
## <a name="table-returned"></a>返回的表  
 下表介绍此行集函数返回的相似或相关文档的信息。  
  
 如果从多个列请求结果，则基于每个列返回匹配的文档。  
  
|Column_name|类型|Description|  
|------------------|----------|-----------------|  
|**source_column_id**|**int**|源文档中用于查找相似文档的列的 ID。<br /><br /> 有关如何在列名称和 column_id 之间相互检索对方的详细信息，请参阅 COL_NAME 和 COLUMNPROPERTY 函数。|  
|**matched_column_id**|**int**|从中找到相似文档的列的 ID。<br /><br /> 有关如何在列名称和 column_id 之间相互检索对方的详细信息，请参阅 COL_NAME 和 COLUMNPROPERTY 函数。|  
|**matched_document_key**|**\***<br /><br /> 此键与源表中的唯一键的类型相匹配。|与查询中的指定文档相似的文档或行的全文和语义提取唯一键值。|  
|**score**|**REAL**|一个相对值，用来表示此文档与所有其他相似文档的相似程度。<br /><br /> 该值是范围 [0.0, 1.0] 中的小数值，较高的得分表示非常匹配，1.0 是最理想的得分。|  
  
## <a name="general-remarks"></a>一般备注  
 有关详细信息，请参阅[查找相似和相关文档使用语义搜索](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 不能跨列查询相似的文档。 **SEMANTICSIMILARITYTABLE**函数仅从同一源列中，由标识列中检索相似的文档**source_key**自变量。  
  
## <a name="metadata"></a>元数据  
 有关语义相似性的提取和填充的信息和状态，请查询以下动态管理视图：  
  
-   [sys.dm_db_fts_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 需要对创建全文和语义搜索所基于的基表具有 SELECT 权限。  
  
## <a name="examples"></a>示例  
 以下示例从 AdventureWorks2012 示例数据库的 HumanResources.JobCandidate 表中检索与指定的候选人最相似的 10 个候选人。  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROMSEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
