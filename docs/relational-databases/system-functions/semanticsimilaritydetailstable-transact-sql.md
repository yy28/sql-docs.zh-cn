---
title: semanticsimilaritydetailstable （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semanticsimilaritydetailstable
- semanticsimilaritydetailstable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritydetailstable function
ms.assetid: 038d751a-fca5-4b4c-9129-cba741a4e173
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 34473e6eb173a0aabc5c2067e50aeeec27ce5636
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067740"
---
# <a name="semanticsimilaritydetailstable-transact-sql"></a>semanticsimilaritydetailstable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回一个表，该表包含其内容在语义上相似的两个文档（源文档和匹配的文档）共有的关键短语的零个、一个或多个行。  
  
 此行集函数可在 SELECT 语句的 FROM 子句中引用 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 **数据表**  
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
  
|Column_name|类型|说明|  
|------------------|----------|-----------------|  
|**关键短语**|**NVARCHAR**|在源文档和匹配文档之间促进相似性的关键短语。|  
|**分值**|**real**|一个相对值，用来表示此关键短语与两篇文档间相似的所有其他关键短语的关系。<br /><br /> 该值是范围 [0.0, 1.0] 中的小数值，较高的得分表示较高权重，1.0 是最理想的得分。|  
  
## <a name="general-remarks"></a>一般备注  
 有关详细信息，请参阅[通过语义搜索查找相似和相关文档](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)。  
  
## <a name="metadata"></a>元数据  
 有关语义相似性的提取和填充的信息和状态，请查询以下动态管理视图：  
  
-   [sys.dm_db_fts_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 需要对创建全文和语义搜索所基于的基表具有 SELECT 权限。  
  
## <a name="examples"></a>示例  
 下面的示例检索5个关键短语，该短语在 AdventureWorks2012 示例数据库的**HumanResources humanresources.jobcandidate**表中指定的候选项之间具有最高相似性分数。 @CandidateId和@MatchedID变量表示全文索引的键列中的值。  
  
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
  
  
