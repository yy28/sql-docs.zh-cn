---
title: "管理和监视语义搜索 | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- semantic search [SQL Server], managing
- semantic search [SQL Server], monitoring
ms.assetid: eb5c3b29-da70-42aa-aa97-7d35a3f1eb98
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b01af634ed2681c49bdb444cd4a468b45be3ab03
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="manage-and-monitor-semantic-search"></a>管理和监视语义搜索
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]说明语义索引编制过程以及与管理和监视索引相关的任务。  
  
##  <a name="HowToMonitorStatus"></a> 检查语义索引编制的状态  
### <a name="is-the-first-phase-of-semantic-indexing-complete"></a>语义索引编制的第一阶段是否已完成？
 查询动态管理视图 [sys.dm_fts_index_population (Transact SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)，并检查 **status** 和 **status_description** 列。  
  
 索引编制的第一阶段包括填充全文关键字索引和语义关键短语索引，以及提取文档相似性数据。  
  
```tsql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_index_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="is-the-second-phase-of-semantic-indexing-complete"></a>语义索引编制的第二阶段是否已完成？
 查询动态管理视图 [sys.dm_fts_semantic_similarity_population (Transact SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)，并检查 **status** 和 **status_description** 列。  
  
 索引编制的第二阶段包括填充语义文档相似性索引。  
  
```wql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_semantic_similarity_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
##  <a name="HowToCheckSize"></a> 检查语义索引的大小  
### <a name="what-is-the-logical-size-of-a-semantic-key-phrase-index-or-a-semantic-document-similarity-index"></a>语义关键短语索引或语义文档相似性索引的逻辑大小是多少？
 查询动态管理视图 [sys.dm_db_fts_index_physical_stats (Transact SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)。  
  
 以索引页数显示该逻辑大小。  
  
```tsql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_db_fts_index_physical_stats WHERE object_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="what-is-the-total-size-of-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>全文目录的全文索引和语义索引的总大小是多少？  
 查询 [FULLTEXTCATALOGPROPERTY (Transact SQL)](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md) 元数据函数的 **IndexSize** 属性 。  
  
```tsql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'IndexSize')  
GO  
```  
  
### <a name="how-many-items-are-indexed-in-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>有多少项编入全文目录的全文索引和语义索引？  
 查询 [FULLTEXTCATALOGPROPERTY (Transact SQL)](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md) 元数据函数的 **ItemCount** 属性 。  
  
```tsql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'ItemCount')  
GO  
```  
  
##  <a name="HowToForcePopulation"></a> 强制填充语义索引  
 可以使用 START/STOP/PAUSE 或 RESUME POPULATION 子句以及针对全文索引而描述的相同语法和行为，强制填充全文索引和语义索引。 更多详细信息，请参阅 [ALTER FULLTEXT INDEX (Transact-SQL )](../../t-sql/statements/alter-fulltext-index-transact-sql.md) 和[填充全文索引](../../relational-databases/search/populate-full-text-indexes.md)。  
  
 由于语义索引编制依赖于全文索引编制，因此仅在填充关联的全文索引后填充语义索引。  
  
 **示例：启动全文索引和语义索引的完全填充**  
  
 以下示例通过更改 AdventureWorks2012 示例数据库的 **Production.Document** 表的现有全文索引，启动全文索引和语义索引的完全填充。  
  
```vb  
USE AdventureWorks2012  
GO  
  
ALTER FULLTEXT INDEX ON Production.Document  
    START FULL POPULATION  
GO  
```  
  
##  <a name="HowToDisableIndexing"></a> 禁用或重新启用语义索引编制  
 可以使用 ENABLE/DISABLE 子句以及针对全文索引而描述的相同语法和行为，启用或禁用全文索引编制或语义索引编制。 有关详细信息，请参阅 [ALTER FULLTEXT INDEX (Transact-SQL )](../../t-sql/statements/alter-fulltext-index-transact-sql.md)。  
  
 禁用和挂起语义索引编制时，可以继续成功进行针对语义数据的查询并返回以前的索引数据。 此行为与全文搜索的行为不一致。  
  
```tsql  
-- To disable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name DISABLE  
GO  
  
-- To re-enable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name ENABLE  
GO  
```  
  
##  <a name="SemanticIndexing"></a> 关于语义索引编制的阶段  
 语义搜索对于启用它的每个列将两种类型的数据编入索引：  
  
1.  **关键短语**  
  
2.  **文档相似性**  
  
 语义索引编制在两个阶段中发生，与全文索引编制一起进行：  
  
1.  **阶段 1**。 同时并行填充全文关键字索引和语义关键短语索引。 还在此时提取编制文档相似性索引所需的数据。  
  
2.  **阶段 2**： 然后填充语义文档相似性索引。 此索引依赖于在前一阶段填充的两个索引。  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="ProblemNotPopulated"></a> 问题：未填充语义索引  
### <a name="are-the-associated-full-text-indexes-populated"></a>是否已填充关联的全文索引？  
 由于语义索引编制依赖于全文索引编制，因此仅在填充关联的全文索引后填充语义索引。  
  
### <a name="are-full-text-search-and-semantic-search-properly-installed-and-configured"></a>是否正确安装和配置了全文搜索和语义搜索？  
 有关详细信息，请参阅 [安装和配置语义搜索](../../relational-databases/search/install-and-configure-semantic-search.md)。  
  
### <a name="is-the-fdhost-service-not-available-or-is-there-another-condition-that-would-cause-full-text-indexing-to-fail"></a>FDHOST 服务是否不可用或存在导致全文索引编制失败的其他情况？  
 有关详细信息，请参阅 [全文索引疑难解答](../../relational-databases/search/troubleshoot-full-text-indexing.md)。  
  
  
