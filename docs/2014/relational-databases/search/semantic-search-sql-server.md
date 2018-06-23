---
title: 语义搜索 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- semantic search [SQL Server]
- semantic search [SQL Server], overview
- statistical semantic search [SQL Server]
- statistical semantic search [SQL Server], overview
ms.assetid: cd8faa9d-07db-420d-93f4-a2ea7c974b97
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8746a7f7a7fb8c1dfc84f3f50a09476f77b3c78a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128942"
---
# <a name="semantic-search-sql-server"></a>语义搜索 (SQL Server)
  统计语义搜索通过提取统计上相关的“关键短语” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*并对其进行索引，提供对*中存储的非结构化文档的更深层次剖析。 然后，它还使用这些关键短语标识“相似或相关文档” 并对其进行索引。  
  
 您通过使用三个 Transact-SQL 行集函数将结果作为结构化数据检索，查询这些语义索引。  
  
##  <a name="whatcanido"></a> 使用语义搜索可以做什么？  
 语义搜索以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中现有的全文搜索功能为基础，但允许超出关键字搜索范畴的新方案。 全文搜索允许你查询文档中的“词”，语义搜索则允许你查询文档的“含义”。 现有的可能解决方案包括自动标记提取、相关内容发现以及相似内容中层次结构导航。 例如，您可以查询关键短语的索引来建立一个组织或文档集的分类索引。 或者，您可以查询文档相似性索引来标识匹配某一工作描述的简历。  
  
 下面的示例演示了语义搜索的功能。  
  
###  <a name="find1"></a> 在文档中查找关键短语  
 下面的查询获取在示例文档中已标识的关键短语。 该查询按照对每个关键短语的统计重要性进行排名的分数以降序方式展示结果。 此查询调用 [semantickeyphrasetable (Transact-SQL)](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql) 函数。  
  
```tsql  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS Title, keyphrase, score  
    FROM SEMANTICKEYPHRASETABLE(Documents, *, @DocID)  
    ORDER BY score DESC  
  
```  
  
  
  
###  <a name="find2"></a> 查找相似或相关文档  
 以下查询获取已标识为与示例文档相似或相关的文档。 该查询按照对这两个文档的相似性进行排名的分数以降序方式展示结果。 此查询调用 [semanticsimilaritytable (Transact-SQL)](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql) 函数。  
  
```vb  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS SourceTitle, DocumentTitle AS MatchedTitle,  
        DocumentID, score  
    FROM SEMANTICSIMILARITYTABLE(Documents, *, @DocID)  
    INNER JOIN Documents ON DocumentID = matched_document_key  
    ORDER BY score DESC  
  
```  
  
  
  
###  <a name="find3"></a> 查找使文档相似或相关的关键短语  
 以下查询获取使两个示例文档彼此相似或相关的关键短语。 该查询按照对每个关键短语的权重进行排名的分数以降序方式展示结果。 此查询调用 [semanticsimilaritydetailstable (Transact-SQL)](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql) 函数。  
  
```tsql  
SET @SourceTitle = 'first.docx'  
SET @MatchedTitle = 'second.docx'  
  
SELECT @SourceDocID = DocumentID FROM Documents WHERE DocumentTitle = @SourceTitle  
SELECT @MatchedDocID = DocumentID FROM Documents WHERE DocumentTitle = @MatchedTitle  
  
SELECT @SourceTitle AS SourceTitle, @MatchedTitle AS MatchedTitle, keyphrase, score  
    FROM semanticsimilaritydetailstable(Documents, DocumentContent,  
        @SourceDocID, DocumentContent, @MatchedDocID)  
    ORDER BY score DESC  
  
```  
  
  
  
##  <a name="store"></a> 在 SQL Server 中存储文档  
 在您可以使用语义搜索对文档建立索引之前，必须在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中存储文档。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的 FileTable 功能使非结构化的文件和文档能够很好地通过关系数据库处理。 这样，数据库开发人员在 Transact-SQL 基于集的操作中可以将文档与结构化数据一起处理。  
  
 有关 FileTable 功能的详细信息，请参阅 [FileTable (SQL Server)](../blob/filetables-sql-server.md)。 有关 FILESTREAM 功能（这是用于在数据库中存储文档的另一个选项）的信息，请参阅 [FILESTREAM (SQL Server)](../blob/filestream-sql-server.md)。  
  
  
  
##  <a name="reltasks"></a> 相关任务  
 [安装和配置语义搜索](install-and-configure-semantic-search.md)  
 说明统计语义搜索的必备组件以及如何安装或检查它们。  
  
 [对表和列启用语义搜索](enable-semantic-search-on-tables-and-columns.md)  
 介绍如何启用或禁用包含文档或文本的选定列上的统计语义索引。  
  
 [使用语义搜索查找文档中的关键短语](find-key-phrases-in-documents-with-semantic-search.md)  
 介绍如何在为统计语义索引配置的文档或文本列中查找关键短语。  
  
 [使用语义搜索来查找相似和相关文档](find-similar-and-related-documents-with-semantic-search.md)  
 说明在为统计语义索引配置的列上如何查找相似或相关的文档或文本值，以及如何查找其相似或相关程度的信息。  
  
 [管理和监视语义搜索](manage-and-monitor-semantic-search.md)  
 说明语义索引编制的进度以及与监视和管理索引有关的任务。  
  
##  <a name="relcontent"></a> 相关内容  
 [语义搜索 DDL、函数、存储过程和视图](../views/views.md)  
 列出用于支持统计语义搜索的新增或更改的 Transact-SQL 语句和 SQL Server 数据库对象。  
  
  
