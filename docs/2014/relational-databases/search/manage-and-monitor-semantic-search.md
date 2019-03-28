---
title: 管理和监视语义搜索 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], managing
- semantic search [SQL Server], monitoring
ms.assetid: eb5c3b29-da70-42aa-aa97-7d35a3f1eb98
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1d68b9452a03c127fe39018c19abab1073dae7c5
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534979"
---
# <a name="manage-and-monitor-semantic-search"></a>管理和监视语义搜索
  说明语义索引编制过程以及与管理和监视索引相关的任务。  
  
##  <a name="HowToMonitorStatus"></a> 如何：检查语义索引编制的状态  
 **语义索引编制的第一阶段已完成？**  
 查询动态管理视图 [sys.dm_fts_index_population (Transact SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)，并检查 **status** 和 **status_description** 列。  
  
 索引编制的第一阶段包括填充全文关键字索引和语义关键短语索引，以及提取文档相似性数据。  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_index_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
 **语义索引编制的第二个阶段已完成？**  
 查询动态管理视图 [sys.dm_fts_semantic_similarity_population (Transact SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql)，并检查 **status** 和 **status_description** 列。  
  
 索引编制的第二阶段包括填充语义文档相似性索引。  
  
```wql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_semantic_similarity_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
##  <a name="HowToCheckSize"></a> 如何：检查语义索引的大小  
 **语义关键短语索引或语义文档相似性索引的逻辑大小是什么？**  
 查询动态管理视图 [sys.dm_db_fts_index_physical_stats (Transact SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql)。  
  
 以索引页数显示该逻辑大小。  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_db_fts_index_physical_stats WHERE object_id = OBJECT_ID('table_name')  
GO  
```  
  
 **什么是全文目录的全文索引和语义索引的总大小？**  
 查询 [FULLTEXTCATALOGPROPERTY (Transact SQL)](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql) 元数据函数的 **IndexSize** 属性 。  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'IndexSize')  
GO  
```  
  
 **多少项编入全文目录的全文索引和语义索引？**  
 查询 [FULLTEXTCATALOGPROPERTY (Transact SQL)](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql) 元数据函数的 **ItemCount** 属性 。  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'ItemCount')  
GO  
```  
  
##  <a name="HowToForcePopulation"></a> 如何：强制填充语义索引  
 可以使用 START/STOP/PAUSE 或 RESUME POPULATION 子句以及针对全文索引而描述的相同语法和行为，强制填充全文索引和语义索引。 更多详细信息，请参阅 [ALTER FULLTEXT INDEX (Transact-SQL )](/sql/t-sql/statements/alter-fulltext-index-transact-sql) 和[填充全文索引](../indexes/indexes.md)。  
  
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
  
##  <a name="HowToDisableIndexing"></a> 如何：禁用或重新启用语义索引编制  
 可以使用 ENABLE/DISABLE 子句以及针对全文索引而描述的相同语法和行为，启用或禁用全文索引编制或语义索引编制。 有关详细信息，请参阅 [ALTER FULLTEXT INDEX (Transact-SQL )](/sql/t-sql/statements/alter-fulltext-index-transact-sql)。  
  
 禁用和挂起语义索引编制时，可以继续成功进行针对语义数据的查询并返回以前的索引数据。 此行为与全文搜索的行为不一致。  
  
```sql  
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
  
##  <a name="SemanticIndexing"></a> 语义索引编制的阶段  
 语义搜索对于启用它的每个列将两种类型的数据编入索引：  
  
1.  **关键短语**  
  
2.  **文档相似性**  
  
 语义索引编制在两个阶段中发生，与全文索引编制一起进行：  
  
1.  **阶段 1**。 同时并行填充全文关键字索引和语义关键短语索引。 还在此时提取编制文档相似性索引所需的数据。  
  
2.  **阶段 2**： 然后填充语义文档相似性索引。 此索引依赖于在前一阶段填充的两个索引。  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="ProblemNotPopulated"></a> 问题：未填充语义索引  
 **关联的全文索引填充？**  
 由于语义索引编制依赖于全文索引编制，因此仅在填充关联的全文索引后填充语义索引。  
  
 **全文搜索和语义搜索正确安装和配置？**  
 有关详细信息，请参阅 [安装和配置语义搜索](install-and-configure-semantic-search.md)。  
  
 **将 FDHOST 服务不可用，或是否有另一个条件会导致全文索引编制失败？**  
 有关详细信息，请参阅 [全文索引疑难解答](troubleshoot-full-text-indexing.md)。  
  
  
