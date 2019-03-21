---
title: 使用语义搜索在文档中查找关键短语 | Microsoft Docs
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], key phrase queries
ms.assetid: 6ee3676e-ed5d-43ec-aeca-1eed78967111
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 851ba91f833edb76227945a4b84fd5eed9f8ab51
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "57973926"
---
# <a name="find-key-phrases-in-documents-with-semantic-search"></a>使用语义搜索查找文档中的关键短语
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  介绍如何在为统计语义索引配置的文档或文本列中查找关键短语。  

##  <a name="howtofind"></a> 使用 SEMANTICKEYPHRASETABLE 在文档中查找关键短语  
 若要确定特定文档中的关键短语或确定包含特定关键短语的文档，可以查询函数 [semantickeyphrasetable (Transact-SQL)](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)。  
  
 SEMANTICKEYPHRASETABLE 为与指定表中的列关联的那些关键短语返回包含零行、一行或多行的表。 可以在 SELECT 语句的 FROM 子句中像引用常规表名那样引用此行集函数。  
  
> [!NOTE]  
>  在此版本中，对于语义搜索只将单个单词编入索引，多词短语 (ngrams) 未编入索引。 此外，相同单词的各种形式单独编入索引，例如，“computer”和“computers”单独编入索引。  
  
 有关 SEMANTICKEYPHRASETABLE 函数所需的参数和它返回的结果表的详细信息，请参阅 [semantickeyphrasetable (Transact-SQL)](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)。  
  
> [!IMPORTANT]  
>  针对的列必须启用了全文索引和语义索引。  
  
###  <a name="HowToTopPhrases"></a> 示例 1：查找特定文档中的最重要关键短语  
 以下示例从通过 @DocumentId 变量指定的文档中检索前 10 个关键短语，该变量位于 AdventureWorks 示例数据库的 Production.Document 表的 Document 列中。 @DocumentId 变量表示全文检索的键列的一个值。  
  
```sql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
GO  
```  
  
 **SEMANTICKEYPHRASETABLE** 函数使用索引查找替代表扫描高效检索这些结果。  
  
###  <a name="HowToTopDocuments"></a> 示例 2：查找包含特定关键短语的最相关文档  
 以下示例从 AdventureWorks 示例数据库的 Production.Document 表的 Document 列中检索包含关键短语“Bracket”的前 25 个文档。  
  
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
GO  
```  
  
  
