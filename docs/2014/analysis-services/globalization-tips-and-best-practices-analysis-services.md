---
title: 全球化提示和最佳做法 (Analysis Services) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- translations [Analysis Services], client applications
- date comparisons
- day-of-week comparisons [Analysis Services]
- time [Analysis Services]
- month comparisons [Analysis Services]
ms.assetid: 71a8c438-1370-4c69-961e-d067ee4e47c2
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 684da8d68061248556d99dcc06c8c8e9207e65d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127431"
---
# <a name="globalization-tips-and-best-practices-analysis-services"></a>全球化提示和最佳实践 (Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]**  多维  
  
 这些提示和准则有助于提高你的商业智能解决方案的可移植性，并避免直接与语言和排序规则设置相关的错误。  
  
-   [在整个堆栈中使用相似排序规则](#bkmk_sameColl)  
  
-   [通用排序规则建议](#bkmk_recos)  
  
-   [对象标识符区分大小写](#bkmk_objid)  
  
-   [使用 Excel 和 SQL Server Profiler 进行区域设置测试](#bkmk_test)  
  
-   [在包含翻译的解决方案中撰写 MDX 查询](#bkmk_mdx)  
  
-   [撰写包含日期和时间值的 MDX 查询](#bkmk_datetime)  
  
##  <a name="bkmk_sameColl"></a> 在整个堆栈中使用相似排序规则  
 如果可能，请在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中使用与用于数据库引擎的排序规则设置相同的排序规则设置，尽量采用一致的全半角区分、大小写区分以及重音区分。  
  
 每个服务都有其自己的排序规则设置，数据库引擎默认设置为 SQL_Latin1_General_CP1_CI_AS 且 Analysis Services 设置为 Latin1_General_AS。 在区分大小写、区分全半角和区分重音方面，默认设置是兼容的。 请注意，如果你改变任一排序规则的设置，则在排序规则属性以基本方式分离时会遇到问题。  
  
 即便排序规则设置功能相当，你也会遇到特殊情况，即每个服务对字符串内任意位置的空格做出不同解释。  
  
 空格字符是“特殊情况”，因为它能以 Unicode 格式用单字节字符集 (SBCS) 或双字节字符集 (DBCS) 来表示。 在关系引擎中，两个由空格隔开的复合字符串 - 一个使用 SBCS，另一个使用 DBCS - 被视为相同。 在 Analysis Services 中，处理期间，同样的两个复合字符串不等同，第二个实例将被标记为副本。  
  
 有关详细信息和建议的解决方法，请参见 [根据不同的排序规则，Unicode 字符串中的空白具有不同的处理结果](http://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx)。  
  
##  <a name="bkmk_recos"></a> 通用排序规则建议  
 Analysis Services 始终显示所有可用语言和排序规则的完整列表；它不基于你所选的语言来筛选排序规则。 请务必选择可操作的组合。  
  
 一些更常使用的排序规则包括以下列表中的排序规则。  
  
 你应该考虑将此列表作为进一步调查的起点，而非排除其他选项的最终建议。 你可能会发现未专门建议使用的排序规则最适用于你的数据。 彻底的测试是验证是否正确排序或比较数据值的唯一方法。 与以前一样，测试排序规则时，务必运行处理和查询工作负荷。  
  
-   Latin1_General_100_AS 通常用于使用 [ISO 基本拉丁字母表](http://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet)26 个字符的应用程序。  
  
-   包含斯堪的纳维亚字母（如 ø）的北欧语言可使用 Finnish_Swedish_100。  
  
-   东欧语言（例如俄语）通常使用 Cyrillic_General_100。  
  
-   中文语言和排序规则因地区而异，但通常不是简体中文就是繁体中文。  
  
     在中国和新加坡，Microsoft 技术支持部门通常见到的是简体中文，简体中文以拼音作为首选的排序方式。 建议使用的排序规则是 Chinese_PRC（用于 SQL Server 2000）、Chinese_PRC_90（用于 SQL Server 2005）或 Chinese_Simplified_Pinyin_100（用于 SQL Server 2008 和更高版本）。  
  
     在中国台湾地区，更常见的是繁体中文，建议使用的是基于笔画数的排序方式：Chinese_Taiwan_Stroke（用于 SQL Server 2000）、Chinese_Taiwan_Stroke_90（用于 SQL Server 2005）或 Chinese_Traditional_Stroke_Count_100（用于 SQL Server 2008 和更高版本）。  
  
     其他区域（如中国香港和中国澳门）也使用繁体中文。 在中国香港，就排序规则而言，Chinese_Hong_Kong_Stroke_90（在 SQL Server 2005 上）的使用较为常见。 在中国澳门，较常使用的是 Chinese_Traditional_Stroke_Count_100（在 SQL Server 2008 和更高版本上）。  
  
-   对于日语，最常使用的排序规则是 Japanese_CI_AS。 Japanese_XJIS_100 用于支持 [JIS2004](http://en.wikipedia.org/wiki/JIS_X_0213)的安装。 Japanese_BIN2 的使用通常见于数据迁移项目，用于由非 Windows 平台或数据源而非 SQL Server 关系数据引擎发出的数据。  
  
     Japanese_Bushu_Kakusu_100 很少见于运行 Analysis Services 工作负荷的服务器。  
  
-   建议针对朝鲜语使用 Korean_100。 虽然在列表中 Korean_Wansung_Unicode 仍可用，但不推荐使用。  
  
##  <a name="bkmk_objid"></a> 对象标识符区分大小写  
 在 SQL Server 2012 SP2 中启动，对象 ID 区分大小写独立于排序规则而强制执行，但是行为随着语言变化：  
  
|语言脚本|区分大小写|  
|---------------------|----------------------|  
|**基本拉丁字母表**|以拉丁语脚本表示的对象标识符（任意 26 个英语大写或小写字母）将视为区分大小写，无论排序规则如何。 例如，以下对象 ID 被认为是相同的：54321**abcdef**、54321**ABCDEF**、54321**AbCdEf**。 在内部，Analysis Services 将字符串中的字符都视作是大写，然后执行与语言无关的简单字节比较。<br /><br /> 请注意，只有这 26 个字符会受到影响。 如果语言是西欧语言，但使用斯堪的纳维亚语言字符，则其他字符将不为大写。|  
|**西里尔语，希腊语，科普特语，亚美尼亚语**|非拉丁语双脚本中的对象标识符（如西里尔语）总是区分大小写。 例如，Измерение 和 измерение 被视为两个不同值，尽管唯一的区别是首字母的大小写。|  
  
 **对象标识符区分大小写的意义**  
  
 仅对象标识符（而非对象名）受限于表中描述的大小写行为。 如果你看到解决方案工作方式有所变化（之前和之后的比较 - 安装 SQL Server 2012 SP2 或更高版本之后），它将最可能是一个处理问题。 查询不受对象标识符影响。 对于两种查询语言（DAX 和 MDX），公式引擎会使用对象名（而非标识符）。  
  
> [!NOTE]  
>  与区分大小写相关的代码更改对某些应用程序来说是重大更改。 请参阅[Analysis Services Features in SQL Server 2014 的重大更改](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)有关详细信息。  
  
##  <a name="bkmk_test"></a> 使用 Excel、SQL Server Profiler 和 SQL Server Management Studio 进行区域设置测试  
 测试翻译时，连接必须指定翻译的 LCID。 如 [从 SSAS 获取不同语言到 Excel](http://extremeexperts.com/sql/Tips/ExcelDiffLocale.aspx)中所述，你可以使用 Excel 测试你的翻译。  
  
 你可以通过手动编辑 .odc 文件以包括区域设置标识符连接字符串属性来实现此操作。 使用 Adventure Works 示例多维数据库尝试此操作。  
  
-   搜索现有的 .odc 文件。 当你找到一个 Adventure Works 多维数据库时，右键单击该文件在记事本中将其打开。  
  
-   将 `Locale Identifier=1036` 添加到连接字符串。 保存并关闭该文件。  
  
-   打开 Excel |“数据” | “现有连接”。 在列表中筛选此计算机上的连接文件。 查找 Adventure Works 的连接（仔细查看名称；你可能发现不止一个）。 打开该连接。  
  
     你会看到 Adventure Works 示例数据库的法语翻译。  
  
     ![Excel 数据透视表及法语翻译](media/ssas-localetest-excel.png "包含法语翻译的 Excel 数据透视表")  
  
 作为后续步骤，可以使用 Server Profiler 来确认区域设置。 单击一个 `Session Initialize` 事件，然后查看下方文本区域中的属性列表以找到 `<localeidentifier>1036</localeidentifier>`。  
  
 在 Management Studio 中，你可以指定服务器连接上的区域设置标识符。  
  
-   在对象资源管理器|“连接”  |  | 中，单击“其他连接参数” **Additional ion Parameters** 选项卡。  
  
-   输入 `Local Identifier=1036` ，然后单击 “连接”。  
  
-   对 Adventure Works 数据库执行 MDX 查询。 查询结果应为法语翻译。  
  
     ![使用 SSMS 中的法语翻译的 MDX 查询](media/ssas-localetest-ssms.png "与在 SSMS 中的法语翻译的 MDX 查询")  
  
##  <a name="bkmk_mdx"></a> 在包含翻译的解决方案中撰写 MDX 查询  
 翻译提供 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象名称的显示信息，但是不翻译相同对象的标识符。 尽可能使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象的标识符和键，而不使用翻译后的标题和名称。 例如，使用多维表达式 (MDX) 语句和脚本的成员键而不是成员名称以确保多种语言之间的可移植性。  
  
> [!NOTE]  
>  回想一下，表格对象名总是区分大小写，无论排序规则如何。 另一方面，多维对象名区分排序规则的大小写。 由于仅多维对象名区分大小写，请确保所有引用多维对象的 MDX 查询的大小写正确。  
  
##  <a name="bkmk_datetime"></a> 撰写包含日期和时间值的 MDX 查询  
 以下建议能使你的基于日期和时间的 MDX 查询在不同语言之间更易于移植：  
  
1.  **使用数值部分进行比较与操作**  
  
     执行月份和星期的比较和操作时，请使用数值日期和时间部分，不要使用等效的字符串（例如，使用 MonthNumberofYear 而不是 MonthName）。 数值受语言翻译的差异的影响最小。  
  
2.  **在结果集中使用等效的字符串**  
  
     生成面向最终用户的结果集时，考虑使用此字符串（如 MonthName），那么你的多语言受众就能从你提供的翻译中获益。  
  
3.  **使用 ISO 日期格式表示通用日期和时间信息**  
  
     一个 [Analysis Services 专家](http://geekswithblogs.net/darrengosbell/Default.aspx) 提出了这一建议：“我一直对传递到 SQL 或 MDX 中的查询的任何日期字符串使用 ISO 日期格式 yyyy-mm-dd，因为它很明确而且无论客户端或服务器的区域设置如何都将正常工作。 我同意在分析不明确的日期格式时服务器应遵从其区域设置，但是我也认为如果你已有不对解释开放的选项，总之最好选择那个选项。”  
  
4.  `Use the Format function to enforce a specific format, regardless of regional language settings`  
  
     以下 MDX 查询（借用自一个论坛帖子）演示了如何使用 Format 以指定格式返回日期，不管基础区域设置如何。  
  
     请参阅 [SSAS 2012 generates invalid dates](http://www.networksteve.com/forum/topic.php/SSAS_2012_generates_invalid_dates/?TopicId=40504&Posts=2) （SSAS 2012 生成无效日期）（Network Steve 上的论坛帖子）查看原始帖子内容。  
  
    ```  
    WITH MEMBER [LinkTimeAdd11Date_Manual] as Format(dateadd("d",15,"2014-12-11"), "mm/dd/yyyy")  
    member [LinkTimeAdd15Date_Manual] as Format(dateadd("d",11,"2014-12-13"), "mm/dd/yyyy")  
    SELECT  
    { [LinkTimeAdd11Date_Manual]  
    ,[LinkTimeAdd15Date_Manual]  
    }  
    ON COLUMNS   
    FROM [Adventure Works]  
  
    ```  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services Multiidimensional 的全球化方案](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [编写国际化 Transact-SQL 语句](../relational-databases/collations/write-international-transact-sql-statements.md)  
  
  