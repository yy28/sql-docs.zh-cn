---
title: 语义搜索 DDL、函数、存储过程和视图 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], database objects
ms.assetid: 182f395f-3168-48a4-b723-ef4403544f9f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ee5cf7136739b012615121e00d8b8d3ed7c7c6ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011037"
---
# <a name="semantic-search-ddl-functions-stored-procedures-and-views"></a>语义搜索 DDL、函数、存储过程和视图
  列出用于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中支持统计语义搜索的 Transact-SQL 语句和数据库对象。  
  
 有关支持全文搜索的语句和数据库对象的列表，请参阅 [全文搜索 DDL、函数、存储过程和视图](../views/views.md)。  
  
##  <a name="transact-sql-data-definition-language-ddl-statements"></a><a name="ddl"></a>Transact-sql 数据定义语言（DDL）语句  
  
|Object|更多信息|  
|------------|----------------------|  
|[ALTER FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/alter-fulltext-index-transact-sql)|[对表和列启用语义搜索](enable-semantic-search-on-tables-and-columns.md)|  
|[CREATE FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/create-fulltext-index-transact-sql)|[对表和列启用语义搜索](enable-semantic-search-on-tables-and-columns.md)|  
  
##  <a name="system-functions"></a><a name="func"></a> 系统函数  
  
|Object|更多信息|  
|------------|----------------------|  
|[semantickeyphrasetable (Transact-SQL)](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql)|[使用语义搜索查找文档中的关键短语](find-key-phrases-in-documents-with-semantic-search.md)|  
|[semanticsimilaritydetailstable (Transact-SQL)](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql)|[使用语义搜索来查找相似和相关文档](find-similar-and-related-documents-with-semantic-search.md)|  
|[semanticsimilaritytable (Transact-SQL)](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql)|[使用语义搜索来查找相似和相关文档](find-similar-and-related-documents-with-semantic-search.md)|  
  
##  <a name="system-metadata-functions"></a><a name="meta"></a> 系统元数据函数  
  
|Object|更多信息|  
|------------|----------------------|  
|[COLUMNPROPERTY (Transact-SQL)](/sql/t-sql/functions/columnproperty-transact-sql)|[对表和列启用语义搜索](enable-semantic-search-on-tables-and-columns.md)|  
|[DATABASEPROPERTYEX (Transact-SQL)](/sql/t-sql/functions/databasepropertyex-transact-sql)|[对表和列启用语义搜索](enable-semantic-search-on-tables-and-columns.md)|  
|[FULLTEXTCATALOGPROPERTY (Transact-SQL)](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)|[管理和监视语义搜索](manage-and-monitor-semantic-search.md)|  
|[INDEXPROPERTY (Transact-SQL)](/sql/t-sql/functions/indexproperty-transact-sql)|[管理和监视语义搜索](manage-and-monitor-semantic-search.md)|  
|[OBJECTPROPERTYEX (Transact-SQL)](/sql/t-sql/functions/objectproperty-transact-sql)|[对表和列启用语义搜索](enable-semantic-search-on-tables-and-columns.md)|  
|[SERVERPROPERTY (Transact-SQL)](/sql/t-sql/functions/serverproperty-transact-sql)|[安装和配置语义搜索](install-and-configure-semantic-search.md)|  
  
##  <a name="system-stored-procedures"></a><a name="sproc"></a> 系统存储过程  
  
|Object|更多信息|  
|------------|----------------------|  
|[sp_fulltext_semantic_register_language_statistics_db (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql)|[安装和配置语义搜索](install-and-configure-semantic-search.md)|  
|[sp_fulltext_semantic_unregister_language_statistics_db (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql)|[安装和配置语义搜索](install-and-configure-semantic-search.md)|  
  
##  <a name="system-views---catalog-views"></a><a name="cv"></a> 系统视图 - 目录视图  
  
|Object|更多信息|  
|------------|----------------------|  
|[sys.fulltext_index_columns (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|[管理和监视语义搜索](manage-and-monitor-semantic-search.md)|  
|[sys.fulltext_semantic_language_statistics_database (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql)|[安装和配置语义搜索](install-and-configure-semantic-search.md)|  
|[sys.fulltext_semantic_languages (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql)|[安装和配置语义搜索](install-and-configure-semantic-search.md)|  
  
##  <a name="system-views---dynamic-management-views"></a><a name="dmv"></a> 系统视图 - 动态管理视图  
  
|Object|更多信息|  
|------------|----------------------|  
|[sys.dm_db_fts_index_physical_stats (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql)|[管理和监视语义搜索](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_index_population (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|[管理和监视语义搜索](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_semantic_similarity_population (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql)|[管理和监视语义搜索](manage-and-monitor-semantic-search.md)|  
  
## <a name="see-also"></a>另请参阅  
 [管理和监视语义搜索](manage-and-monitor-semantic-search.md)  
  
  
