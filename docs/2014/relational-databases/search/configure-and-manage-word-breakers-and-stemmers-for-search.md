---
title: 配置和管理断字符和词干分析器以便搜索 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- full-text search [SQL Server], stemmers
- linguistic analysis [full-text search]
- full-text indexes [SQL Server], linguistic analysis
- full-text search [SQL Server], word breakers
- default full-text language option
- stemmers [full-text search]
- conjugating verbs [full-text search]
- word breakers [full-text search]
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 22cb7371a0215989d2759ddfb2c84f51ba5c3c31
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "84997582"
---
# <a name="configure-and-manage-word-breakers-and-stemmers-for-search"></a>配置和管理断字符和词干分析器以便搜索
  断字符和词干分析器用于对所有全文索引数据执行语言分析。 语言分析将涉及到查找词边界（断字）和组合动词（词干分析）。 断字符和词干分析器是特定于语言的，并且各语言的语言分析规则也各不相同。 对于给定语言，“断字符” ** 通过根据语言的词法规则确定词的边界位置来标识各个词。 每个词（也称为标记  ）使用压缩表示形式插入全文索引以减少其大小。 词干分析器** 根据该语言的规则生成特定词的变形形式（例如，“running”、“ran”和“runner”是单词“run”的不同形式）。  
  
 使用特定于语言的断字符，能够使得为该语言生成的词更加准确。 如果断字符用于整个语系而不是特定的子语言，将使用该语系中的主要语言。 例如，使用法语断字符来处理加拿大法语文本。 如果某一特定语言没有可用的断字符，将使用非特定语言断字符。 使用非特定语言断字符时，词将在非特定语言字符（如空格和标点符号）处断开。  
  
##  <a name="registering-word-breakers"></a><a name="register"></a>注册断字符  
 要想使用某种语言的断字符，就必须为其进行注册。 对于已注册的断字符，关联的语言资源（词干分析器、干扰词（非索引字）和同义词库文件）也将可用于全文索引和查询操作。 若要查看当前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中注册了断字符的语言列表，请使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
 SELECT * FROM sys.fulltext_languages  
  
 如果您添加、删除或更改了断字符，则需要刷新为全文索引和查询而支持的 Microsoft Windows 区域设置标识符 (LCID) 列表。 有关详细信息，请参阅 [查看或更改注册的筛选器和断字符](view-or-change-registered-filters-and-word-breakers.md)。  
  
##  <a name="setting-the-default-full-text-language-option"></a><a name="default"></a>设置默认全文语言选项  
 对于的本地化版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序会将 `default full-text language` 选项设置为服务器的语言（如果存在合适的匹配项）。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的非本地化版本，`default full-text language` 选项为“英语”。  
  
 创建或修改全文索引时，可以为每个全文索引列指定不同的语言。 如果未指定列的语言，默认值是配置选项 `default full-text language` 的值。  
  
> [!NOTE]  
>  在单个全文查询函数子句中列出的所有列必须使用同一语言，除非在查询中指定了 LANGUAGE 选项。 所查询的用于全文索引列的语言确定了对全文查询谓词（[CONTAINS](/sql/t-sql/queries/contains-transact-sql) 和 [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)）以及函数（[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 和 [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql)）的参数执行的语言分析。  
  
##  <a name="choosing-the-language-for-an-indexed-column"></a><a name="lang"></a>为索引列选择语言  
 创建全文索引时，建议为每个索引列都指定一种语言。 如果未为列指定语言，则将使用系统默认语言。 某列的语言确定使用什么断字符和词干分析器对该列创建索引。 另外，该语言的同义词库文件将由针对相应列的全文查询使用。  
  
 如果要选择用于创建全文索引的列语言，有几个事项需要注意。 这些注意事项均与全文引擎如何对文本进行词汇切分再编制其索引有关。 有关详细信息，请参阅 [创建全文索引时选择语言](choose-a-language-when-creating-a-full-text-index.md)。  
  
 **查看列的断字符语言**  
  
-   [管理全文索引](../indexes/indexes.md)  
  
-   [sys.fulltext_index_columns (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
    ```  
    SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;  
    ```  
  
##  <a name="obtaining-information-about-word-breakers"></a><a name="info"></a>获取有关断字符的信息  
 **查看断字符、同义词库和非索引字表组合的词汇切分结果**  
  
-   [sys.dm_fts_parser (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)。  
  
 **返回有关已注册断字符的信息**  
  
-   [sp_help_fulltext_system_components (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql)  
  
##  <a name="troubleshooting-word-breaking-time-out-errors"></a><a name="tshoot"></a>排除断字超时错误  
 在许多情况下可能会出现断字超时错误。 有关这些情况及如何针对每种情况做出反应的信息，请参阅 [MSSQLSERVER_30053](../errors-events/mssqlserver-30053-database-engine-error.md)。  
  
##  <a name="understanding-the-impact-of-new-word-breakers"></a><a name="impact"></a>了解新断字符的影响  
 每个版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通常都包括新的断字符，这些断字符与早期断字符相比具有更好的语言规则并且更加准确。 新断字符的行为可能与从以前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入的全文索引中的断字符行为稍有不同。 如果全文目录是在数据库升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的当前版本时导入的，这一点将非常重要。 该全文目录中全文索引使用的一种或多种语言现在可能与新断字符关联。 有关详细信息，请参阅 [全文搜索升级](upgrade-full-text-search.md)。  
  
 有关所有断字符的完整列表，请参阅[transact-sql&#41;&#40;fulltext_languages ](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;更改全文索引](/sql/t-sql/statements/alter-fulltext-index-transact-sql)   
 [CREATE FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [sp_fulltext_service &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)   
 [sys. fulltext_languages &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [为全文搜索配置和管理非索引字和非索引字](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [升级全文搜索](upgrade-full-text-search.md)  
  
  
