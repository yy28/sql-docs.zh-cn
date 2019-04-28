---
title: 全文搜索的重大更改 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- full-text catalogs [SQL Server], breaking changes
- breaking changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: c55a6748-e5d9-4fdb-9a1f-714475a419c5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 45b13c29af6a9c5e82533a4b66213d1cb1b9dd15
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787755"
---
# <a name="breaking-changes-to-full-text-search"></a>对全文搜索的重大更改
  本主题介绍全文搜索的重大更改。 这些更改可能导致基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的早期版本的应用程序、脚本或功能无法继续使用。 在进行升级时可能会遇到这些问题。 有关详细信息，请参阅 [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)。  
  
## <a name="breaking-changes-in-full-text-search-in-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中全文搜索的重大更改  
 将很快提供相关信息。  
  
## <a name="breaking-changes-in-full-text-search-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中全文搜索的重大更改  
  
### <a name="collation-changed-for-name-column-in-sysfulltextlanguages"></a>sys.fulltext_languages 中名称列的排序规则已更改  
 [sys.fulltext_languages (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql) 目录视图中的语言 **name** 列的排序规则已经从资源数据库的固定排序规则更改为针对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例选择的默认排序规则。 在将 [sys.syslanguages (Transact-SQL)](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql) 视图与 **sys.fulltext_languages (Transact-SQL)** 联接在一起时，这一更改可以比较 **name** 列中的值。 例如，您可以查询默认全文语言不同于默认数据库语言的所有数据库。  
  
## <a name="breaking-changes-in-full-text-search-in-sql-server-2008"></a>SQL Server 2008 中全文搜索的重大更改  
 下面是 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 和 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 及更高版本之间对全文搜索的重大更改。  
  
|功能|应用场景|SQL Server 2005|SQL Server 2008 及更高版本|  
|-------------|--------------|---------------------|----------------------------------------|  
|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)与用户定义类型 (Udt)|全文键为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用户定义类型，例如，`MyType = char(1)`。|返回键的类型是为用户定义类型指定的类型。<br /><br /> 在示例中，这将是**char （1)**。|返回键的类型是用户定义类型。 在示例中，这将是**MyType**。|  
|*top_n_by_rank*参数 (的 CONTAINSTABLE 和[FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) [!INCLUDE[tsql](../includes/tsql-md.md)]语句)|*top_n_by_rank*使用 0 作为参数的查询。|失败并显示一个错误消息，说明您必须使用一个大于零的值。|成功，返回零行。|  
|CONTAINSTABLE 和**ItemCount**|在它将更改推入 MSSearch 之前从基表中删除行。|CONTAINSTABLE 返回虚影记录。 **ItemCount**不会更改。|CONTAINSTABLE 不返回任何虚影记录。|  
|**ItemCount**|表包含 Null 文档或类型列。|除了索引文档，文档为 null 或 null 类型，不会计入**ItemCount**值。|仅索引的文档中计**ItemCount**值。|  
|目录**ItemCount**|扩展名为 NULL 的 Blob 列。|以计数**ItemCount**的目录|它不会计入**ItemCount**的目录。|  
|**UniqueKeyCount**|从目录查询唯一键计数，例如，有两个表（table1 和 table2），每个表都包含三个单词：word1、word2 和 word3。|**UniqueKeyCount** = 9。 下表总结了如何得出此值：<br /><br /> table1 = 3<br /><br /> table1 全文索引的 EOF = 1<br /><br /> table2 = 3<br /><br /> Table2 全文索引的 EOF = 1<br /><br /> 全文目录 = 1|对于每个表中， **UniqueKeyCount**是个数的非重复关键字 + 1 (0xFF)。  不会将在多个文档中出现的同一个单词视为新的唯一键。<br /><br /> 有关目录， **UniqueKeyCount**是总和**UniqueKeyCount**的每个目录下的表。 不同表中的相同单词被视为唯一键。 在这种情况下唯一键计数是 8。|  
|**预计算等级**服务器级选项|FREETEXTTABLE 查询的性能优化。|FREETEXTTABLE 查询选项设置为 1，指定与*top_n_by_rank*使用预计算排名数据存储在全文目录中。|不支持。|  
|[sp_fulltext_pendingchanges](/sql/relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql)更新键列时|对包含两行的表的其中一行更新全文键列，并运行 sp_fulltext_pendingchanges。|两个行均显示。|只显示一行。|  
|内联函数|带全文运算符的内联函数|返回错误消息。|返回相关行。|  
|[sp_fulltext_database](/sql/relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql)|通过使用 sp_fulltext_database 启用或禁用全文搜索。|全文查询不返回任何结果。 如果对数据库禁用全文功能，则将不允许全文操作。|为全文查询返回结果，并且允许全文操作，即使对数据库禁用全文功能也是如此。|  
|特定于区域设置的非索引字|查询特定于 inlocale 的变体的父语言，如比利时法语和加拿大法语。|查询特定于 inlocale 的变体由其父语言的组件 （断字符、 词干分析器和非索引字） 处理。 例如，“法语（法国）”组件用于分析“法语（比利时）”。|必须为每个区域设置标识符 (LCID) 显式添加非索引字。 例如，您需要为比利时、加拿大和法国指定一个 LCID。|  
|同义词库词干分析进程|使用同义词库和变形（词干分析）。|同义词库单词在其扩展之后自动进行词干分析。|如果要得到扩展形式中的词干，则需要显式添加词干。|  
|全文目录路径和文件组|使用全文目录。|每个全文目录都有一个物理路径，并且都属于一个文件组。 系统将其视为数据库文件。|全文目录是虚拟对象，不属于任何文件组。 全文目录是表示一组全文索引的逻辑概念。<br /><br /> 注意：[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)][!INCLUDE[tsql](../includes/tsql-md.md)] 指定全文目录的 DDL 语句正常工作。|  
|[sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql)|使用此目录视图的 path、data_space_id 和 file_id。|这些列都返回一个特定值。|由于全文目录已不再位于文件系统中，因而这些列均返回 NULL。|  
|[sys.sysfulltextcatalogs](/sql/relational-databases/system-compatibility-views/sys-sysfulltextcatalogs-transact-sql)|使用此不推荐使用的系统表的 path 列。|返回全文目录的文件系统路径。|由于全文目录已不再位于文件系统中，因而返回 NULL。|  
|[sp_help_fulltext_catalogs](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql)<br /><br /> [sp_help_fulltext_catalogs_cursor](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql)|使用这些不推荐使用的存储过程的 PATH 列。|返回全文目录的文件系统路径。|由于全文目录已不再位于文件系统中，因而返回 NULL。|  
|[sp_help_fulltext_catalog_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql)|使用此存储过程的 sp_help_fulltext_catalog_components。|返回用于当前数据库中所有全文目录的所有组件（筛选器、断字符和协议处理程序）的列表。|返回空行。|  
|[DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql)|使用**IsFullTextEnabled**属性。|**IsFullTextEnabled**设置指示是否在给定数据库中启用了全文搜索。|此列的值没有任何效果。 用户数据库始终启用全文搜索。|  
  
## <a name="see-also"></a>请参阅  
 [全文搜索的行为更改](../relational-databases/search/full-text-search.md)   
 [全文搜索](../relational-databases/search/full-text-search.md)  
  
  
