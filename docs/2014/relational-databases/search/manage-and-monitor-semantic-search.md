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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 94f8edc0fe8b2505adc36705200e299f36b2dbf9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011133"
---
# <a name="manage-and-monitor-semantic-search"></a>管理和监视语义搜索
  说明语义索引编制过程以及与管理和监视索引相关的任务。  
  
##  <a name="HowToMonitorStatus"></a>如何：检查语义索引编制的状态  
 **语义索引编制的第一阶段是否已完成？**  
 查询动态管理视图 [sys.dm_fts_index_population (Transact SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)，并检查 **status** 和 **status_description** 列。  
  
 索引编制的第一阶段包括填充全文关键字索引和语义关键短语索引，以及提取文档相似性数据。  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_index_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
 **语义索引编制的第二阶段是否已完成？**  
 查询动态管理视图 [sys.dm_fts_semantic_similarity_population (Transact SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql)，并检查 **status** 和 **status_description** 列。  
  
 索引编制的第二阶段包括填充语义文档相似性索引。  
  
```wql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_semantic_similarity_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
##  <a name="HowToCheckSize"></a>如何：检查语义索引的大小  
 **语义关键短语索引或语义文档相似性索引的逻辑大小是多少？**  
 查询动态管理视图 [sys.dm_db_fts_index_physical_stats (Transact SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql)。  
  
 以索引页数显示该逻辑大小。  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_db_fts_index_physical_stats WHERE object_id = OBJECT_ID('table_name')  
GO  
```  
  
 **全文目录的全文索引和语义索引的总大小是多少？**  
 查询 **FULLTEXTCATALOGPROPERTY (Transact SQL)** 元数据函数的 [IndexSize](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql) 属性 。  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'IndexSize')  
GO  
```  
  
 **有多少项编入全文目录的全文索引和语义索引？**  
 查询 **FULLTEXTCATALOGPROPERTY (Transact SQL)** 元数据函数的 [ItemCount](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql) 属性 。  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'ItemCount')  
GO  
```  
  
##  <a name="HowToForcePopulation"></a>如何：强制填充语义索引  
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
  
##  <a name="HowToDisableIndexing"></a>如何禁用或重新启用语义索引编制  
 可以使用 ENABLE/DISABLE 子句以及针对全文索引而描述的相同语法和行为，启用或禁用全文索引编制或语义索引编制。 有关详细信息，请参阅 [ALTER FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/alter-fulltext-index-transact-sql)。  
  
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
  
##  <a name="SemanticIndexing"></a>语义索引的阶段  
 语义搜索对于启用它的每个列将两种类型的数据编入索引：  
  
1.  **关键短语**  
  
2.  **文档相似性**  
  
 语义索引编制在两个阶段中发生，与全文索引编制一起进行：  
  
1.  **阶段 1**。 同时并行填充全文关键字索引和语义关键短语索引。 还在此时提取编制文档相似性索引所需的数据。  
  
2.  **阶段 2**： 然后填充语义文档相似性索引。 此索引依赖于在前一阶段填充的两个索引。  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="ProblemNotPopulated"></a>问题：未填充语义索引  
 **是否已填充关联的全文索引？**  
 由于语义索引编制依赖于全文索引编制，因此仅在填充关联的全文索引后填充语义索引。  
  
 **是否正确安装和配置了全文搜索和语义搜索？**  
 有关详细信息，请参阅 [安装和配置语义搜索](install-and-configure-semantic-search.md)。  
  
 **FDHOST 服务是否不可用或存在导致全文索引编制失败的其他情况？**  
 有关详细信息，请参阅 [全文索引疑难解答](troubleshoot-full-text-indexing.md)。  
  
  
