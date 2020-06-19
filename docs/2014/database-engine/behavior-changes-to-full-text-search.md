---
title: 对全文搜索的行为更改 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- behavior changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: 573444e8-51bc-4f3d-9813-0037d2e13b8f
author: rothja
ms.author: jroth
ms.openlocfilehash: cbe807237651bd8bb81fa1c9f028847654b97889
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936169"
---
# <a name="behavior-changes-to-full-text-search"></a>全文搜索的行为更改
  本主题介绍全文搜索中的行为更改。 与早期版本的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 相比， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的功能的工作或交互方式会受到行为更改的影响。  
  
## <a name="behavior-changes-in-full-text-search-in-sssql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中全文搜索的行为更改  
 将很快提供相关信息。  
  
## <a name="behavior-changes-in-full-text-search-in-sssql11"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中全文搜索的行为更改  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 为美国英语 (LCID 1033) 和英国英语 (LCID 2057) 安装了新版本的断字符和词干分析器。 但是，如果您想要保留这些组件的以前行为，您可以切换到其早期版本。 有关详细信息，请参阅 [更改用于美国英语和英国英语的断字符](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)。  
  
### <a name="new-word-breakers-and-stemmers-installed"></a>安装了新的断字符和词干分析器  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 更新全文搜索和语义搜索所使用的所有断字符和词干分析器。 为了保持索引内容和查询结果之间的一致性，建议您重新填充现有全文索引。  
  
1.  英语已有了新的断字符。 如果您必须保留先前行为，请参阅 [Change the Word Breaker Used for US English and UK English](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)。  
  
2.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的先前版本附带的丹麦语、波兰语和土耳其语的第三方断字符已替换为 [!INCLUDE[msCoName](../includes/msconame-md.md)] 组件。 默认情况下启用这些新组件。  
  
3.  捷克语和希腊语已有了新的断字符。 先前版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 全文搜索不包括对这两种语言的支持。  
  
### <a name="behavior-changes-of-new-word-breakers-and-stemmers"></a>新断字符和词干分析器的行为更改  
 在填充和查询全文索引时，新组件可能返回不同于旧组件的结果。 下表说明在英语结果中一些可以预计的差异。  
  
 如果您必须保持断字符和词干分析器的以前的行为，请参阅以下主题：  
  
-   [更改用于美国英语和英国英语的断字符](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
-   [将搜索功能所使用的断字符还原到以前的版本](../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
 在某些情况下，新组件返回 *更多* 结果：  
  
|**术语**|**先前断字符和词干分析器的结果**|**新断字符和词干分析器的结果**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|cat-dog|cat<br /><br /> dog|cat<br /><br /> cat-dog<br /><br /> dog|  
|cat@dog.com|cat<br /><br /> com<br /><br /> dog|cat<br /><br /> cat@dog.com<br /><br /> com<br /><br /> dog|  
|12/11/2011<br /><br /> *（其中此字词表示日期）*|12/11/2011<br /><br /> dd20111211|11<br /><br /> 12<br /><br /> 12/11/2011<br /><br /> 2011<br /><br /> dd20111211|  
  
 在某些情况下，新组件返回 *类似* 结果：  
  
|**术语**|**先前断字符和词干分析器的结果**|**新断字符和词干分析器的结果**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|100$|100$<br /><br /> nn100$|100$<br /><br /> nn100usd|  
|022|022<br /><br /> nn022|022<br /><br /> nn22|  
|10:49AM<br /><br /> *（其中此字词表示时间）*|10:49AM<br /><br /> tt1049|10:49AM<br /><br /> tt24104900|  
  
 在某些情况下，新组件返回 *较少* 结果或返回应用程序可能无法预期的结果：  
  
|**术语**|**先前断字符和词干分析器的结果**|**新断字符和词干分析器的结果**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|jě﨩ˊÿqCžl<br /><br /> *（其中字词为无效英文字符）*|' jě﨩ˊÿqCžl '|je yq zl|  
|table's|table's<br /><br /> 表|table's|  
|cat-|cat<br /><br /> cat-|cat|  
|v z *（其中，v 和 z 为干扰词）*|*（无结果）*|v z|  
|$100 000 USD|$100<br /><br /> 000<br /><br /> nn000<br /><br /> nn100$<br /><br /> USD|$100 000 USD<br /><br /> nn100000usd|  
|beautiful U.S land|beautiful<br /><br /> land<br /><br /> u.s<br /><br /> us|beautiful<br /><br /> land|  
|Mt. Kent and Mt Challenger|challenger<br /><br /> kent<br /><br /> mt<br /><br /> Mt.|mt<br /><br /> kent<br /><br /> challenger|  
  
## <a name="behavior-changes-in-full-text-search-in-sql-server-2008"></a>SQL Server 2008 中全文搜索的行为更改  
 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 和更高版本中，全文引擎作为数据库服务集成到关系数据库中，作为服务器查询和存储引擎基础结构的一部分。 新的全文搜索体系结构可实现以下目的：  
  
-   集成的存储和管理-全文搜索现在直接与的固有存储和管理功能集成 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，并且 MSFTESQL 服务已不再存在。  
  
    -   全文索引存储在数据库文件组内部，而不是在文件系统中。 对数据库执行管理操作（如创建备份）会自动影响其全文索引。  
  
    -   现在，全文目录是虚拟对象，并不属于任何文件组；它是表示一组全文索引的逻辑概念。 因此，许多目录管理功能已不推荐使用，继而也就引发了某些功能的重大更改。 有关详细信息，请参阅[SQL Server 2014 中不推荐使用的数据库引擎功能](deprecated-database-engine-features-in-sql-server-2016.md)和[对全文搜索的重大更改](breaking-changes-to-full-text-search.md)。  
  
        > [!NOTE]  
        >  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)][!INCLUDE[tsql](../includes/tsql-md.md)]指定全文目录的 DDL 语句可以正常工作。  
  
-   集成查询处理-新的全文搜索查询处理器是数据库引擎的一部分，并与 SQL Server 查询处理器完全集成。 这表示查询优化器将识别全文查询谓词，并尽可能高效地自动执行它们。  
  
-   增强的管理和故障排除-集成的全文搜索提供的工具可帮助您分析搜索结构，例如全文索引、给定断字符的输出、非索引字配置等。  
  
-   非索引字和非索引字表已替代干扰词和干扰词文件。 非索引字表是一种数据库对象，有助于简化非索引字的可管理性任务，并提高不同服务器实例和环境之间的完整性的一个数据库对象。 有关详细信息，请参阅 [为全文搜索配置和管理非索引字和非索引字表](../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
-   [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 和更高版本包括 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 中存在的许多语言的新断字符。 只有英语、朝鲜语、泰语和中文（所有形式）的断字符保持不变。 对于其他语言，如果全文目录是在 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 数据库升级到 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 或更高版本时导入的，则全文目录中全文索引使用的一种或多种语言现在可能与新断字符关联，这些断字符的行为可能与导入的断字符的行为略有不同。 有关如何确保查询和全文索引内容之间的一致性的详细信息，请参阅[升级全文搜索](../relational-databases/search/upgrade-full-text-search.md)。  
  
-   已添加一个新的 FDHOST 启动器 (MSSQLFDLauncher) 服务。 有关详细信息，请参阅[全文搜索入门](../relational-databases/search/get-started-with-full-text-search.md)。  
  
-   全文索引处理[FILESTREAM](../relational-databases/blob/filestream-sql-server.md)列的方式与处理列的方式相同 `varbinary(max)` 。 FILESTREAM 表必须有一列包含每个 FILESTREAM BLOB 的文件扩展名。 有关详细信息，请参阅[利用全文搜索进行查询](../relational-databases/search/query-with-full-text-search.md)、[配置和管理搜索筛选器](../relational-databases/search/configure-and-manage-filters-for-search.md)和[sys. fulltext_document_types &#40;transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql)。  
  
     全文引擎会对 FILESTREAM BLOB 的内容进行索引。 对诸如图像之类的文件进行索引可能没有用。 更新 FILESTREAM BLOB 时，会重新对其进行索引。  
  
## <a name="see-also"></a>另请参阅  
 [全文搜索](../relational-databases/search/full-text-search.md)   
 [全文搜索向后兼容性](../../2014/database-engine/full-text-search-backward-compatibility.md)   
 [升级全文搜索](../relational-databases/search/upgrade-full-text-search.md)   
 [全文搜索入门](../relational-databases/search/get-started-with-full-text-search.md)  
  
  
