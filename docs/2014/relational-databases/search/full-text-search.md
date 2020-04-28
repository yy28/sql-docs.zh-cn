---
title: 全文搜索 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server]
ms.assetid: a0ce315d-f96d-4e5d-b4eb-ff76811cab75
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 61faaa7854aa362e7d269cf3f00911470126f42c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176837"
---
# <a name="full-text-search"></a>全文搜索
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中的全文搜索为用户和应用程序提供了对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中基于字符的数据运行全文查询的功能。 在可以对某一表运行全文查询之前，数据库管理员必须对该表创建全文索引。 全文索引包括表中一个或多个基于字符的列。 这些列可以具有下列任何一种数据类型：`char`、`varchar`、`nchar`、`nvarchar`、`text`、`ntext`、`image`、`xml` 或 `varbinary(max)` 和 FILESTREAM。 每个全文索引都对表中的一个或多个列创建索引，并且每个列都可以使用特定语言。

 全文查询根据特定语言（例如，英语或日语）的规则对词和短语进行操作，从而对全文索引中的文本数据执行语言搜索。 全文查询可以包括简单的词和短语，或者词或短语的多种形式。 全文查询返回包含至少一个匹配项（也称为“命中”**）的所有文档。 当目标文档包含在全文查询中指定的所有字词，并符合任何其他搜索条件（如匹配的字词之间的距离）时，即发生匹配。

> [!NOTE]
>  全文搜索是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎的一个可选组件。 有关详细信息，请参阅[Install SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)。

##  <a name="what-can-i-do-with-full-text-search"></a><a name="benefits"></a>对于全文搜索，我该怎么办？
 全文搜索适用于各种业务方案，如电子商务-在网站上搜索项目;法律公司-在法律数据存储库中搜索案例历史记录;或人力资源部门-将作业说明与存储的简历匹配。 不管是什么样的商业应用场景，全文搜索的基本管理任务和开发任务是相同的。 然而，在给定的商业应用场景中，可以对全文索引和查询进行优化以使其满足业务目标。 例如，对于电子商务来说，最大限度地提高性能可能比对结果进行排序、检索的准确性（实际上有多少个现有匹配项是由全文查询返回的）或支持多种语言更重要。 对于律师事务所来说，首先需要考虑的可能是返回所有可能存在的匹配项（“返回全部”** 信息）。

 [本主题内容](#top)

###  <a name="full-text-search-queries"></a><a name="queries"></a>全文搜索查询
 在将列添加到全文索引之后，用户和应用程序即可对列中的文本运行全文查询。 这些查询可以搜索以下项中的任一项：

-   一个或多个特定的词或短语（“简单词”**）

-   以指定文本开头的词或短语（“前缀词”**）

-   特定词的变形（“派生词”**）

-   与另一个词或短语邻近的词或短语（“邻近词”**）

-   特定词的同义词形式（“同义词库”**）

-   使用加权值的词或短语（“加权词”**）

 全文查询不区分大小写。 例如对于 "Aluminum" 或 "aluminum"，搜索将返回相同的结果。

 全文查询使用一小组 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 谓词（CONTAINS 和 FREETEXT）和函数（CONTAINSTABLE 和 FREETEXTTABLE）。 然而，给定商业应用场景的搜索目标会对全文查询的结构产生影响。 例如：

-   电子商务（在网站上搜索产品）：

    ```
    SELECT product_id 
    FROM products 
    WHERE CONTAINS(product_description, "Snap Happy 100EZ"
        OR FORMSOF(THESAURUS,'Snap Happy')
        OR '100EZ') 
    AND product_cost < 200 ;
    ```

-   招聘员工（搜索具有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用经验的职位候选人）：

    ```
    SELECT candidate_name,SSN 
    FROM candidates 
    WHERE CONTAINS(candidate_resume,"SQL Server") AND candidate_division = 'DBA';
    ```

 有关详细信息，请参阅 [使用全文搜索查询](query-with-full-text-search.md)。

 [本主题内容](#top)

###  <a name="comparing-like-to-full-text-search"></a><a name="like"></a>与全文搜索的比较
 与全文搜索不同， [LIKE](/sql/t-sql/language-elements/like-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 谓词仅对字符模式有效。 另外，不能使用 LIKE 谓词来查询格式化的二进制数据。 此外，对大量非结构化的文本数据执行 LIKE 查询要比对相同数据执行同样的全文查询慢得多。 对数百万行文本数据进行的 LIKE 查询可能需要几分钟的时间才能返回结果；而对于同样的数据，全文查询只需要几秒甚至更少的时间，具体取决于返回的行数。

 [本主题内容](#top)

##  <a name="components-and-architecture-of-full-text-search"></a><a name="architecture"></a>全文搜索的组件和体系结构
 全文搜索体系结构包括以下进程：

-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 进程 (sqlservr.exe)。

-   筛选器后台程序宿主进程 (fdhost.exe)。

     为了安全起见，筛选器由称为筛选器后台程序宿主的单独进程加载。 fdhost.exe 进程是由 FDHOST 启动器服务 (MSSQLFDLauncher) 创建的，这些进程使用 FDHOST 启动器服务帐户的安全凭据运行。 因此，必须运行 FDHOST 启动器服务才能正常进行全文索引和全文查询。 有关设置此服务的服务帐户的信息，请参阅 [设置用于全文筛选器后台程序启动器的服务帐户](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)。

 这两个进程包含全文搜索体系结构的各组件。 下图概括了这些组件及其关系。 该图后面的内容介绍了这些组件。

 ![全文搜索体系结构](../../database-engine/media/ifts-arch.gif "全文搜索体系结构")

 [本主题内容](#top)

###  <a name="sql-server-process"></a><a name="sqlprocess"></a>SQL Server 进程
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 进程使用全文搜索的以下组件：

-   **用户表。** 这些表包含要进行全文索引的数据。

-   **全文收集器。** 全文收集器使用全文爬网线程。 它负责计划和驱动对全文索引的填充，并负责监视全文目录。

-   **同义词库文件。** 这些文件包含搜索项的同义词。 有关详细信息，请参阅 [为全文搜索配置和管理同义词库文件](configure-and-manage-thesaurus-files-for-full-text-search.md)。

-   **非索引字表对象。** 非索引字表对象包含对搜索无用的常见词列表。 有关详细信息，请参阅 [为全文搜索配置和管理非索引字和非索引字表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。

-   **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]查询处理器。** 查询处理器编译并执行 SQL 查询。 如果 SQL 查询包含全文搜索查询，则在编译和执行期间该查询都会发送到全文引擎。 查询结果将与全文索引相匹配。

-   **全文引擎。** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的全文引擎现已与查询处理器完全集成。 全文引擎编译和执行全文查询。 作为查询执行的一部分，全文引擎可能会接收来自同义词库和非索引字表的输入。

-   **索引编写器（索引器）。** 索引编写器生成用于存储索引标记的结构。

-   **筛选器后台程序管理器。** 筛选器后台程序管理器负责监视全文引擎筛选器后台程序宿主的状态。

 [本主题内容](#top)

###  <a name="filter-daemon-host-process"></a><a name="fdhostprocess"></a>筛选器后台程序宿主进程
 筛选器后台程序宿主是一个由全文引擎启动的进程。 它运行下列全文搜索组件，这些组件负责对表中的数据进行访问、筛选和断字，同时还负责对查询输入进行断字和提取词干。

 筛选器后台程序宿主的组件如下：

-   **协议处理程序。** 此组件从内存中取出数据，以进行进一步的处理，并访问指定数据库的用户表中的数据。 其职责之一是从全文索引列中收集数据，并将所收集的数据传递给筛选器后台程序宿主，从而由该宿主根据需要应用筛选和断字符。

-   **筛选.** 某些数据类型需要筛选，然后才能为文档中的数据（包括 、、 或  列中的数据）创建全文索引。 给定文档采用何种筛选器取决于文档类型。 例如，Microsoft Word (.doc) 文档、Microsoft Excel (.xls) 文档和 XML (.xml) 文档分别使用不同的筛选器。 然后，筛选器从文档中提取文本块区，删除嵌入的格式并保留文本，如有可能的话也会保留有关文本位置的信息。 结果将以文本化信息流的形式出现。 有关详细信息，请参阅 [配置和管理搜索筛选器](configure-and-manage-filters-for-search.md)。

-   **断字符和词干分析器。** 断字符是特定于语言的组件，它根据给定语言的词汇规则查找词边界（“断字”**）。 每个断字符都与用于组合动词及执行变形扩展的特定于语言的词干分析器组件相关联。 在创建索引时，筛选器后台程序宿主使用断字符和词干分析器来对给定表列中的文本数据执行语言分析。 与全文索引中的表列相关的语言将决定为列创建索引时要使用的断字符和词干分析器。 有关详细信息，请参阅 [配置和管理断字符和词干分析器以便搜索](configure-and-manage-word-breakers-and-stemmers-for-search.md)。

 [本主题内容](#top)

##  <a name="full-text-search-processing"></a><a name="processing"></a>全文搜索处理
 全文搜索由全文引擎提供支持。 全文引擎有两个角色：索引支持和查询支持。

###  <a name="full-text-indexing-process"></a><a name="indexing"></a>全文索引过程
 全文填充（也称为爬网）开始后，全文引擎会将大批数据存入内存并通知筛选器后台程序宿主。 宿主对数据进行筛选和断字，并将转换的数据转换为倒排词列表。 然后，全文搜索从词列表中提取转换的数据，对其进行处理以删除非索引字，然后将某一批次的词列表永久保存到一个或多个倒排索引中。

 对`varbinary(max)`存储在`image`或列中的数据编制索引时，筛选器（实现**IFilter**接口）根据指定的文件格式（例如， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word）来提取文本。 在某些情况下，筛选器组件要求`varbinary(max)`将或`image`数据写出到 filterdata 文件夹，而不是推送到内存。

 在处理过程中，通过断字符将收集到的文本数据分隔成各个单独的标记或关键字。 用于词汇切分的语言将在列级指定，或者也可以通过筛选器组件在 `varbinary(max)`、`image` 或 `xml` 数据内标识。

 还可能会进行其他处理以删除非索引字，并在将标记存储到全文索引或索引片断之前对其进行规范化。

 填充完成后，将触发最终的合并过程，以便将索引碎片合并为一个主全文索引。 由于只需要查询主索引而不需要查询大量索引碎片，因此这将提高查询性能，并且可以使用更好的计分统计信息来得出相关性排名。

 [本主题内容](#top)

###  <a name="full-text-querying-process"></a><a name="querying"></a>全文查询过程
 查询处理器将查询的全文部分传递到全文引擎以进行处理。 全文引擎执行断字，此外，它还可以执行同义词库扩展、词干分析以及非索引字（干扰词）处理。 然后，查询的全文部分以 SQL 运算符的形式表示，主要作为流式表值函数 (STVF)。 在查询执行过程中，这些 STVF 访问倒排索引以检索正确结果。 此时会将结果返回给客户端，或者先将它们进一步处理，再将它们返回给客户端。

 [本主题内容](#top)

##  <a name="linguistic-components-and-language-support-in-full-text-search"></a><a name="components"></a>全文搜索中的语言组件和语言支持
 全文搜索支持大约 50 种不同语言，例如英语、西班牙语、中文、日语、阿拉伯语、孟加拉语和印地语。 有关支持的全文语言的完整列表，请参阅 [sys.fulltext_languages (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)。 全文索引中包含的每一列与一个 Microsoft Windows 区域设置标识符 (LCID) 相关联，每个区域设置标识符等同于全文搜索支持的一种语言。 例如，LCID 1033 等于美国英语，LCID 2057 等于英国英语。 对于每种支持的全文语言， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供语言组件以支持对以该语言存储的全文数据进行索引和查询。

 语言特有组件包括：

-   **断字符和词干分析器。** 断字符根据给定语言的词汇规则查找词边界（“断字”**）。 每个断字符与一个词干分析器相关联，该词干分析器组合了同一种语言的动词。 有关详细信息，请参阅 [配置和管理断字符和词干分析器以便搜索](configure-and-manage-word-breakers-and-stemmers-for-search.md)。

-   **非索引字表。** 提供系统非索引字表，其中包含一组基本非索引字（也称为干扰词）。 “非索引字”** 是对搜索没有任何帮助并且被全文查询忽略的词。 例如，在英语区域设置中，诸如“a”、“and”、“is”和“the”之类的词都被视为非索引字。 通常情况下，需要配置一个或多个同义词库文件和非索引字表。 有关详细信息，请参阅 [为全文搜索配置和管理非索引字和非索引字表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。

-   **同义词库文件。** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 还会安装一个全局同义词库文件，并且还为每种全文语言安装一个同义词库文件。 安装的同义词库文件实际上是空的，不过可以编辑它们以便为特定语言或商业应用场景定义同义词。 通过开发针对全文数据定制的同义词库，您可以有效地扩大对这些数据的全文查询的范围。 有关详细信息，请参阅 [为全文搜索配置和管理同义词库文件](configure-and-manage-thesaurus-files-for-full-text-search.md)。

-   **筛选器 (iFilter)。**  对 `varbinary(max)`、`image` 或 `xml` 数据类型列中的文档进行索引时，需要使用筛选器来执行额外的处理工作。 此筛选器必须特定于文档类型（.doc、.pdf、.xls、.xml 等）。 有关详细信息，请参阅 [配置和管理搜索筛选器](configure-and-manage-filters-for-search.md)。

 断字符（和词干分析器）以及筛选器在筛选器后台程序宿主进程 (fdhost.exe) 中运行。

 [本主题内容](#top)

##  <a name="related-tasks"></a><a name="reltasks"></a> 相关任务

-   [全文搜索入门](get-started-with-full-text-search.md)

-   撰写全文查询

    -   [使用全文搜索查询](query-with-full-text-search.md)

    -   [使用 NEAR 搜索与另一个词邻近的词](search-for-words-close-to-another-word-with-near.md)

    -   [使用 RANK 限制搜索结果](limit-search-results-with-rank.md)

    -   [改进全文查询的性能](improve-the-performance-of-full-text-queries.md)

    -   [使用搜索属性列表搜索文档属性](search-document-properties-with-search-property-lists.md)

    -   [查找搜索属性的属性集 GUID 和属性整数 ID](find-property-set-guids-and-property-integer-ids-for-search-properties.md)

-   管理目录和索引

    -   [创建和管理全文目录](create-and-manage-full-text-catalogs.md)

    -   [创建和管理全文索引](create-and-manage-full-text-indexes.md)

    -   [创建全文索引时选择语言](choose-a-language-when-creating-a-full-text-index.md)

    -   [填充全文索引](populate-full-text-indexes.md)

    -   [管理全文索引](../../database-engine/manage-full-text-indexes.md)

    -   [改进全文索引的性能](improve-the-performance-of-full-text-indexes.md)

    -   [排除全文索引故障](troubleshoot-full-text-indexing.md)

    -   [备份和还原全文目录和索引](back-up-and-restore-full-text-catalogs-and-indexes.md)

-   管理语言组件

    -   [配置和管理搜索筛选器](configure-and-manage-filters-for-search.md)

    -   [配置和管理断字符和词干分析器以便搜索](configure-and-manage-word-breakers-and-stemmers-for-search.md)

    -   [查看或更改注册的筛选器和断字符](view-or-change-registered-filters-and-word-breakers.md)

    -   [将搜索功能所使用的断字符还原到以前的版本](revert-the-word-breakers-used-by-search-to-the-previous-version.md)

    -   [更改用于美国英语和英国英语的断字符](change-the-word-breaker-used-for-us-english-and-uk-english.md)

    -   [使用自定义词典自定义断字符的行为](customize-the-behavior-of-word-breakers-with-a-custom-dictionary.md)

    -   [为全文搜索配置和管理非索引字和非索引字表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)

    -   [为全文搜索配置和管理同义词库文件](configure-and-manage-thesaurus-files-for-full-text-search.md)

-   管理全文搜索

    -   [管理和监视服务器实例的全文搜索](manage-and-monitor-full-text-search-for-a-server-instance.md)

    -   [设置用于全文筛选器后台程序启动器的服务帐户](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)

-   [升级全文搜索](upgrade-full-text-search.md)

 [本主题内容](#top)

##  <a name="related-content"></a><a name="relcontent"></a> 相关内容

-   [全文搜索 DDL、函数、存储过程和视图](../views/views.md)

 [本主题内容](#top)


