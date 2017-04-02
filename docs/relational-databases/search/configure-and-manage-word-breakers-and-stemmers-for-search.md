---
title: "配置和管理断字符和词干分析器以便搜索 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "语言 [全文搜索]"
  - "全文搜索 [SQL Server], 词干分析器"
  - "语言分析 [全文搜索]"
  - "全文索引 [SQL Server], 语言分析"
  - "全文搜索 [SQL Server], 断字符"
  - "default full-text language 选项"
  - "词干分析器 [全文搜索]"
  - "组合动词 [全文搜索]"
  - "断字符 [全文搜索]"
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
caps.latest.revision: 89
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 88
---
# 配置和管理断字符和词干分析器以便搜索
  断字符和词干分析器用于对所有全文索引数据执行语言分析。 语言分析将涉及到查找词边界（断字）和组合动词（词干分析）。 断字符和词干分析器是特定于语言的，并且各语言的语言分析规则也各不相同。 对于给定语言，“断字符”  通过根据语言的词法规则确定词的边界位置来标识各个词。 每个词（也称为标记）使用压缩表示形式插入全文索引以减少其大小。 词干分析器根据该语言的规则生成特定词的变形形式（例如，“running”、“ran”和“runner”是单词“run”的不同形式）。  
  
 使用特定于语言的断字符，能够使得为该语言生成的词更加准确。 如果断字符用于整个语系而不是特定的子语言，将使用该语系中的主要语言。 例如，使用法语断字符来处理加拿大法语文本。 如果某一特定语言没有可用的断字符，将使用非特定语言断字符。 使用非特定语言断字符时，词将在非特定语言字符（如空格和标点符号）处断开。  
  
##  <a name="register"></a> 注册断字符  
 要想使用某种语言的断字符，就必须为其进行注册。 对于已注册的断字符，关联的语言资源（词干分析器、干扰词（非索引字）和同义词库文件）也将可用于全文索引和查询操作。 若要查看当前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册了断字符的语言列表，请使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
 SELECT * FROM sys.fulltext_languages  
  
 如果您添加、删除或更改了断字符，则需要刷新为全文索引和查询而支持的 Microsoft Windows 区域设置标识符 (LCID) 列表。 有关详细信息，请参阅 [View or Change Registered Filters and Word Breakers](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)。  
  
##  <a name="default"></a> 设置默认全文语言选项  
 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地化版本，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将把“默认全文语言”选项设置为服务器的语言（如果存在合适的匹配项）。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的非本地化版本，“默认全文语言”选项为“英语”。  
  
 创建或修改全文索引时，可以为每个全文索引列指定不同的语言。 如果未指定列的语言，默认值是配置选项“默认全文语言”的值。  
  
> [!NOTE]  
>  在单个全文查询函数子句中列出的所有列必须使用同一语言，除非在查询中指定了 LANGUAGE 选项。 所查询的用于全文索引列的语言确定了对全文查询谓词（[CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)）以及函数（[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)）的参数执行的语言分析。  
  
##  <a name="lang"></a> 为索引列选择语言  
 创建全文索引时，建议为每个索引列都指定一种语言。 如果未为列指定语言，则将使用系统默认语言。 某列的语言确定使用什么断字符和词干分析器对该列创建索引。 另外，该语言的同义词库文件将由针对相应列的全文查询使用。  
  
 如果要选择用于创建全文索引的列语言，有几个事项需要注意。 这些注意事项均与全文引擎如何对文本进行词汇切分再编制其索引有关。 有关详细信息，请参阅[创建全文索引时选择语言](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)。  
  
 **查看列的断字符语言**  
  
-   [管理全文索引](../Topic/Manage%20Full-Text%20Indexes.md)  
  
-   [sys.fulltext_index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
    ```  
    SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;  
    ```  
  
##  <a name="info"></a> 获取有关断字符的信息  
 **查看断字符、同义词库和非索引字表组合的词汇切分结果**  
  
-   [sys.dm_fts_parser (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)。  
  
 **返回有关已注册断字符的信息**  
  
-   [sp_help_fulltext_system_components (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
  
##  <a name="tshoot"></a> 排除断字超时错误  
 在许多情况下可能会出现断字超时错误。 有关这些情况及如何针对每种情况做出反应的信息，请参阅 [MSSQLSERVER_30053](../Topic/MSSQLSERVER_30053.md)。  
  
##  <a name="impact"></a> 理解新断字符的影响  
 每个版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通常都包括新的断字符，这些断字符与早期断字符相比具有更好的语言规则并且更加准确。 新断字符的行为可能与从以前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入的全文索引中的断字符行为稍有不同。 如果全文目录是在数据库升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的当前版本时导入的，这一点将非常重要。 该全文目录中全文索引使用的一种或多种语言现在可能与新断字符关联。 有关详细信息，请参阅[全文搜索升级](../../relational-databases/search/upgrade-full-text-search.md)。  
  
 有关所有断字符的完整列表，请参阅 [sys.fulltext_languages (Transact SQL )](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)。  
  
## 另请参阅  
 [ALTER FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [sp_fulltext_service (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [sys.fulltext_languages (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)   
 [为全文搜索配置和管理非索引字和非索引字表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [升级全文搜索](../../relational-databases/search/upgrade-full-text-search.md)  
  
  