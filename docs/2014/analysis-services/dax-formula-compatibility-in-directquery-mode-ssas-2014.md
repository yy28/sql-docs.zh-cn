---
title: 在 DirectQuery 模式下 (SSAS 2014) 的 DAX 公式兼容性 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2014
ms.assetid: de83cfa9-9ffe-4e24-9c74-96a3876cb4bd
caps.latest.revision: 3
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 700fed6039c53bd7e3c485d06fe5df4eae32e7f8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024246"
---
# <a name="dax-formula-compatibility-in-directquery-mode-ssas-2014"></a>在 DirectQuery 模式下 (SSAS 2014) 的 DAX 公式兼容性
数据分析表达式语言 (DAX) 可以用于在 Analysis Services 表格模型中，创建度量值和使用其他自定义公式[!INCLUDE[ssGemini](../includes/ssgemini-md.md)]Excel 工作簿中的数据模型和 Power BI Desktop 数据模型。 在大多数方面，在这些环境中创建的模型是相同的并且你可以使用相同的度量值、 关系和 Kpi，等等。但是，如果你创作的 Analysis Services 表格模型，并将其部署在 DirectQuery 模式下，有一些限制你可以使用的公式。 本主题概述了这些差异，列出在兼容级别 1100年或 1103年的 SQL Server 2014 Analysis Services tabulars 模型和 DirectQuery 模式下，不支持的函数，并且列出了支持的函数但可能返回不同的结果。  
  
在本主题中，我们使用术语*内存中模型*若要引用的表格模型，这是完全托管在表格模式下运行的 Analysis Services 服务器上的内存中缓存的数据。 我们使用*DirectQuery 模型*来指代已编写和/或具有在 DirectQuery 模式下部署的表格模型。 有关 DirectQuery 模式的信息，请参阅[DirectQuery 模式 （SSAS 表格）](http://msdn.microsoft.com/en-us/45ad2965-05ec-4fb1-a164-d8060b562ea5)。  
  
  
## <a name="bkmk_SemanticDifferences"></a>内存中与 DirectQuery 模式之间的差异  
与内存中模式下部署的模型相比，DirectQuery 模式下部署的相同模型在查询时可能返回不同的结果。 这是因为使用 DirectQuery 时，直接从关系数据存储查询数据和使用相关的关系引擎，而不是存储使用 xVelocity 内存中分析引擎 (VertiPaq) 执行所需的公式的聚合和计算。  
  
例如，某些关系数据存储区在处理数值、日期、Null 等的方式上就存在差异。  
  
相比之下，DAX 语言旨在尽可能接近地模拟 Microsoft Excel 中函数的行为。 例如，在处理 Null、空字符串和零值时，Excel 尝试提供最佳响应，而不考虑精确的数据类型，因此 xVelocity 引擎执行同样的处理。 然而，当表格模型在 DirectQuery 模式下部署并将公式传递到关系数据源进行计算时，必须根据关系数据源的语义处理数据，这通常要求以截然不同的方式处理空字符串与 null。 因此，当针对缓存的数据和针对只从关系存储中返回的数据进行计算时，同一个公式可能返回不同的结果。  
  
此外，某些函数不能在所有在 DirectQuery 模式下因为计算将需要在当前上下文中的数据发送到关系数据源作为参数。 例如，测量中[!INCLUDE[ssGemini](../includes/ssgemini-md.md)]工作簿通常使用引用可用的工作簿中的日期范围的时间智能函数。 在 DirectQuery 模式下，一般不能使用此类公式。  
  
## <a name="semantic-differences"></a>语义差异  
本节列出您可以预期的语义差异类型，并介绍可能适用于函数使用或查询结果的任何限制。  
  
### <a name="bkmk_Comparisons"></a>比较  
内存中模型中的 DAX 支持对两个解析为不同数据类型的标量值的表达式进行比较。 但是，在 DirectQuery 模式下部署的模型使用关系引擎的数据类型和比较运算符，因此可能返回不同的结果。  
  
当在针对 DirectQuery 数据源的计算中使用以下比较时，将始终返回错误：  
  
-   数值数据类型与任何字符串数据类型相比较  
  
-   数值数据类型与布尔值相比较  
  
-   任何字符串数据类型与布尔值相比较  
  
通常，DAX 在内存中模型内更能容忍数据类型不匹配，并最多尝试两次对值进行隐式转换，如本节中所述。 但是，将根据关系引擎的规则，对在 DirectQuery 模式下发送到关系数据存储区的公式进行计算，且这些公式失败的可能性更高。  
  
**字符串和数字的比较**  
示例： `“2” < 3`  
  
此公式比较文本字符串与数字。 对于 DirectQuery 模式和内存中模型，此表达式均为 **true** 。  
  
在内存中模型中，结果为 **true** ，因为作为字符串的数字将隐式转换为数值数据类型，以便与其他数字进行比较。 SQL 还隐式将作为比较所用数字的文本数字转换为数值数据类型。  
  
请注意，这表示在行为方面与 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]的第一个版本发生了变化，此时将返回 **false**，因为文本“2”始终被视为大于任何数字。  
  
**文本与布尔值的比较**  
示例： `“VERDADERO” = TRUE`  
  
此表达式比较文本字符串与布尔值。 通常，对于 DirectQuery 或内存中模型，将字符串值与布尔值进行比较将导致错误。 此规则的唯一例外是当字符串包含字词 **true** 或 **false**时；如果字符串包含 true 或 false 值之一，则将执行到布尔值的转换，此时将发生比较，并给出逻辑结果。  
  
**Null 值的比较**  
示例： `EVALUATE ROW("X", BLANK() = BLANK())`  
  
此公式比较 null 的 SQL 等效值与 null。 它在内存中模型和 DirectQuery 模型中返回 **true** ；在 DirectQuery 模型中进行了预配，以保证与内存中模型相似的行为。  
  
请注意，在 Transact-SQL 中，null 值始终不等于 null。 但在 DAX 中，空白等于另一个空白。 这种行为对于所有内存中模型都是相同的。 务必注意，DirectQuery 模式使用大多数的 SQL Server 语义；但在此情况下，它对于 NULL 比较给出不同的新行为。  
  
### <a name="bkmk_Casts"></a>强制转换  
  
在 DAX 中没有此类转换函数，但在许多比较和算术运算中会执行隐式转换。 它是确定结果的数据类型的比较或算术运算。 例如，  
  
-   布尔值在算术运算中被当作数值（如 TRUE + 1 或应用于布尔值列的函数 MIN）。 NOT 运算也返回一个数值。  
  
-   在比较中以及在与 EXACT、AND、OR、 &amp;&amp;或 || 结合使用时，布尔值始终被当作逻辑值。  
  
**从字符串转换为布尔值**  
在内存中模型和 DirectQuery 模型中，只允许从以下这些字符串转换为布尔值： **“”** （空字符串）、 **“true”**、 **“false”**；其中，空字符串转换为 false 值。  
  
将任何其他字符串转换为布尔数据类型会导致错误。  
  
**从字符串转换为日期/时间**  
在 DirectQuery 模式中，从日期和时间的字符串表示形式转换为实际的 **datetime** 值的行为与在 SQL Server 中相同。  
  
有关这些规则控制从字符串到的强制转换**datetime**中的数据类型[!INCLUDE[ssGemini](../includes/ssgemini-md.md)]模型，请参阅[DAX 语法参考](https://msdn.microsoft.com/library/ee634217.aspx)。  
  
使用内存中数据存储区的模型所支持的日期文本格式范围比 SQL Server 支持的日期字符串格式的范围更加有限。 然而，DAX 支持自定义日期和时间格式。  
  
**从字符串转换为非布尔值的其他类型**  
当从字符串转换为非布尔值时，DirectQuery 模式的行为与 SQL Server 相同。 有关详细信息，请参阅 [CAST 和 CONVERT (Transact-SQL)](http://msdn.microsoft.com/en-us/a87d0850-c670-4720-9ad5-6f5a22343ea8)。  
  
**不允许从数字转换为字符串**  
示例： `CONCATENATE(102,”,345”)`  
  
在 SQL Server 中，不允许从数字转换为字符串。  
  
此公式在表格模型和 DirectQuery 模式下返回一个错误；然而，此公式在 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]中将生成一个结果。  
  
**在 DirectQuery 中不支持两次尝试转换**  
当第一次转换失败时，内存中模型常常尝试第二次转换。 这在 DirectQuery 模式下绝不会发生。  
  
示例： `TODAY() + “13:14:15”`  
  
在此表达式中，第一个参数具有类型 **datetime** ；第二个参数具有类型 **string**。 但是，将以不同方式处理组合操作数时的转换。 DAX 将执行从 **string** 到 **double**的隐式转换。 在内存中模型内，公式引擎尝试直接转换为 **double**；如果失败，它将尝试将字符串转换为 **datetime**。  
  
在 DirectQuery 模式下，只适用从 **string** 到 **double** 的直接转换。 如果此转换失败，公式将返回错误。  
  
### <a name="bkmk_Math"></a>数学函数和算术运算  
在 DirectQuery 模式下，某些数学函数将返回不同的结果，因为基础数据类型或可应用于运算中的转换存在差异。 此外，上面介绍的有关允许的值范围的限制可能影响算术运算的结果。  
  
**添加顺序**  
当您创建一个添加一系列数字的公式时，内存中模型可能以不同于 DirectQuery 模型的顺序处理这些数字。  因此，当您具有许多非常大的正数和非常大的负数时，您可能在一个运算中获得错误，而导致另一个运算。  
  
**使用 POWER 函数**  
示例： `POWER(-64, 1/3)`  
  
在 DirectQuery 模式下，当求小数指数的值时，POWER 函数无法使用负数作为底数。 这在 SQL Server 中是预期行为。  
  
在内存中模型内，该公式返回 -4。  
  
**数值溢出运算**  
在 Transact-SQL 中，导致数值溢出的运算会返回溢出错误；因此，导致溢出的公式也会在 DirectQuery 模式中引发错误。  
  
但是，同一公式在内存中模型内使用时会返回一个 8 字节整数。 这是因为公式引擎不检查是否出现了数值溢出。  
  
**具有空白的 LOG 函数返回不同的结果**  
SQL Server 处理 Null 值和空白的方式与 xVelocity 引擎不同。 因此，以下公式在 DirectQuery 模式下返回错误，但在内存中模式下返回无穷大 (–inf)。  
  
`EXAMPLE: LOG(blank())`  
  
同样的限制应用于其他对数函数：LOG10 和 LN。  
  
有关 DAX 中的 **blank** 数据类型的详细信息，请参阅 [DAX 语法参考](https://msdn.microsoft.com/library/ee634217.aspx)。  
  
**被零除和除以空白**  
在 DirectQuery 模式下，被零 (0) 除和除以空白将始终导致错误。 SQL Server 不支持无穷大的概念，并且因为任何被零除的自然结果都是无穷大，所以，结果是一个错误。 但是，SQL Server 支持除以 Null 值，其结果必须始终为 Null。  
  
在 DirectQuery 模式下将不会针对这些运算返回不同结果，但这两种运算类型（被零除和被 Null 除）将返回错误。  
  
请注意，在 Excel 和 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 模型中，被零除也返回错误。 除以空白将返回空白。  
  
下面的表达式在内存中模型中都是有效的，但在 DirectQuery 模式下将失败：  
  
`1/BLANK`  
  
`1/0`  
  
`0.0/BLANK`  
  
`0/0`  
  
表达式 `BLANK/BLANK` 是一种特殊情况，它在内存中模型和 DirectQuery 模式下同时返回 `BLANK` 。  
  
### <a name="bkmk_Ranges"></a>支持的数字和日期-时间范围  
中的公式[!INCLUDE[ssGemini](../includes/ssgemini-md.md)]和表格模型中的内存受最多方面与 Excel 相同的限制允许的实际数字和日期值。 但是，当从计算或查询中返回最大值时，或者当转换、强制转换、舍入或截断值时，将出现差异。  
  
-   如果在 DirectQuery 模式下，类型 **Currency** 和 **Real** 的值相乘，并且结果大于可能的最大值，则不会引发错误，而返回 Null。  
  
-   在内存中模型中，不会引发错误，但返回最大值。  
  
通常，因为接受的日期范围对于 Excel 和 SQL Server 是不同的，所以，仅当日期在共同的日期范围内（包括以下日期）时，才能保证结果匹配。  
  
-   最早日期：1990 年 3 月 1 日  
  
-   最晚日期：9999 年 12 月 31 日  
  
如果公式中使用的任何日期超出此范围，则公式将导致错误，或结果不匹配。  
  
**CEILING 支持的浮点值**  
示例： `EVALUATE ROW("x", CEILING(-4.398488E+30, 1))`  
  
DAX CEILING 函数的 Transact-SQL 对等函数只支持数量级为 10^19 或更低的值。 一个常识是浮点值应能够适合 **bigint**。  
  
**所含日期超出范围的 Datepart 函数**  
仅当用作参数的日期在有效的日期范围内时，DirectQuery 模式下的结果才与内存中模型中的结果匹配。 如果未满足这些条件，则要么引发错误，要么公式在 DirectQuery 模式下将返回与在内存中模式下不同的结果。  
  
示例： `MONTH(0)` 或 `YEAR(0)`  
  
在 DirectQuery 模式下，此表达式分别返回 12 和 1899。  
  
在内存中模型内，此表达式分别返回 1 和 1900。  
  
示例：  `EOMONTH(0.0001, 1)`  
  
仅当作为参数提供的数据在有效的日期范围内时，此表达式的结果才匹配。  
  
示例： `EOMONTH(blank(), blank())` 或 `EDATE(blank(), blank())`  
  
此表达式的结果在 DirectQuery 模式和内存中模式下应该是相同的。  
  
**截断时间值**  
示例： `SECOND(1231.04097222222)`  
  
在 DirectQuery 模式下，将按照 SQL Server 的规则截断结果，并且表达式的计算结果为 59。  
  
在内存中模型内，每个临时运算的结果将四舍五入；因此，表达式的计算结果为 0。  
  
下面的示例演示如何计算此值：  
  
1.  输入的小数部分 (0.04097222222) 乘以 24。  
  
2.  生成的小时值 (0.98333333328) 乘以 60。  
  
3.  生成的分钟值为 58.9999999968。  
  
4.  分钟值的小数部分 (0.9999999968) 乘以 60。  
  
5.  生成的秒钟值 (59.999999808) 舍入到 60。  
  
6.  60 等效于 0。  
  
**不支持的 SQL 时间数据类型**  
内存中模型不支持使用新的 SQL **Time** 数据类型。 在 DirectQuery 模式下，引用具有此数据类型的列的公式将返回错误。 时间数据列不能导入到内存中模型内。  
  
但是，在[!INCLUDE[ssGemini](../includes/ssgemini-md.md)]和在缓存模型中，有时引擎将强制转换为可接受的数据类型，时间值和公式返回的结果。  
  
这种行为影响将日期列用作参数的所有函数。  
  
### <a name="bkmk_Currency"></a>Currency  
在 DirectQuery 模式下，如果算术运算的结果具有类型 **Currency**，则值必须在以下范围内：  
  
-   最小值：-922337203685477.5808  
  
-   最大值：922337203685477.5807  
  
**结合使用 Currency 和 REAL 数据类型**  
示例： `Currency sample 1`  
  
如果 **Currency** 和 **Real** 类型相乘，并且结果大于 9223372036854774784 (0x7ffffffffffffc00)，则 DirectQuery 模式不会引发错误。  
  
在内存中模型内，如果结果的绝对值大于 922337203685477.4784，则引发错误。  
  
**运算导致值超出范围**  
示例： `Currency sample 2`  
  
如果针对两种货币值的运算导致值超出指定的范围，则在内存中模型内将引发错误，但在 DirectQuery 模型中不引发错误。  
  
**结合使用 Currency 以及其他数据类型**  
将货币值除以其他数值类型的值可能导致不同的结果。  
  
### <a name="bkmk_Aggregations"></a>聚合函数  
对包含一行的表执行统计函数会返回不同的结果。 对空表执行聚合函数的行为对于内存中模型和 DirectQuery 模式也不相同。  
  
**针对具有单行的表执行统计函数**  
如果在 DirectQuery 模式下用作参数的表包含单个行，则统计函数（如 STDEV 和 VAR）将返回 Null。  
  
在内存中模型中，对具有单一行的表使用 STDEV 或 VAR 的公式将返回被零除错误。  
  
### <a name="bkmk_Text"></a>文本函数  
因为关系数据存储区与 Excel 提供的文本数据类型不同，所以，当您搜索字符串或使用子字符串时，可能看到不同的结果。 字符串的长度也可能不同。  
  
通常，使用固定大小列作为参数的任何字符串运算函数都可能具有不同的结果。  
  
此外，在 SQL Server 中，一些文本函数支持 Excel 中未提供的其他参数。 如果公式需要缺少的参数，则在内存中模型内可能获得不同的结果或错误。  
  
**使用 LEFT、RIGHT 等返回字符的运算可能返回正确的字符但大小写不同，或者不返回结果。**  
示例： `LEFT([“text”], 2)`  
  
在 DirectQuery 模式下，所返回的字符的大小写始终与数据库中存储的字母完全相同。 但是，xVelocity 引擎针对值的压缩和编制索引使用不同的算法以提高性能。  
  
默认情况下使用 Latin1_General 排序规则，它不区分大小写，但区分重音。 因此，如果一个文本字符串的多个实例为小写、大写或混合大小写，则所有实例都被视为相同的字符串，索引中只存储字符串的第一个实例。 针对存储的字符串执行的所有文本函数都将检索编入索引的表单的指定部分。 因此，此示例公式将使用第一个实例作为输入，针对整列返回相同的值。  
  
[表格模型中的字符串存储和排序规则](http://msdn.microsoft.com/en-us/8516f0ad-32ee-4688-a304-e705143642ca)  
  
这种行为也适用于其他文本函数，包括 RIGHT、MID 等。  
  
**字符串长度影响结果**  
示例： `SEARCH(“within string”, “sample target  text”, 1, 1)`  
  
如果您使用 SEARCH 函数某个搜索字符串，并且目标字符串大于此内部包含的字符串，DirectQuery 模式将引发错误。  
  
在内存中模型内，将返回所搜索的字符串，但其长度截断为 &lt;内含文本&gt;的长度。  
  
示例： `EVALUATE ROW("X", REPLACE("CA", 3, 2, "California") )`  
  
如果在 DirectQuery 模式下，替换字符串的长度大于原始字符串的长度，则公式将返回 Null。  
  
在内存中模型内，公式遵循 Excel 的行为，它将源字符串和替换字符串串联起来，返回 CACalifornia。  
  
**字符串中间的隐式 TRIM**  
示例： `TRIM(“ A sample sentence with leading white space”)`  
  
DirectQuery 模式将 DAX TRIM 函数转换为 SQL 语句 `LTRIM(RTRIM(<column>))`。 因此，将只删除前导和尾随空格。  
  
相比较而言，内存中模型内的相同公式将遵循 Excel 的行为，删除字符串内的空格。  
  
**隐式 RTRIM 并使用 LEN 函数**  
示例： `LEN(‘string_column’)`  
  
与 SQL Server 类似，DirectQuery 模式自动从字符串列的末尾删除空格；也即，它执行隐式 RTRIM。 因此，如果字符串具有尾随空格，则使用 LEN 函数的公式可能返回不同的值。  
  
**内存中模式支持 SUBSTITUTE 的其他参数**  
示例： `SUBSTITUTE([Title],”Doctor”,”Dr.”)`  
  
示例： `SUBSTITUTE([Title],”Doctor”,”Dr.”, 2)`  
  
在 DirectQuery 模式下，只能使用此函数具有三 (3) 个参数的版本：对列的引用、旧文本和新文本。 如果您使用第二个公式，将引发错误。  
  
在内存中模型中，您可以使用可选的第四个参数来指定要替换的字符串的实例编号。 例如，您可以只替换第二个实例等。  
  
**REPT 运算的字符串长度限制**  
在内存中模型内，使用 REPT 的运算所生成的字符串的长度应小于 32,767 个字符。  
  
在 DirectQuery 模式下，这种限制不适用。  
  
**子字符串运算根据字符类型返回不同的结果**  
示例： `MID([col], 2, 5)`  
  
如果输入文本为 **varchar** 或 **nvarchar**，则公式的结果始终相同。  
  
但是，如果文本是固定长度的字符且 *&lt;num_chars&gt;* 的值大于目标字符串的长度，则在 DirectQuery 模式下，将在结果字符串的末尾添加一个空格。  
  
在内存中模型内，结果将在字符串的最后一个字符处终止，且没有填充。  
  
## <a name="bkmk_SupportedFunc"></a>在 DirectQuery 模式下支持的函数  
以下 DAX 函数可用于 DirectQuery 模式下，但具有前面章节所介绍的限制条件。  
  
**文本函数**  
  
CONCATENATE  
  
FIND  
  
LEFT  
  
LEN  
  
MID  
  
REPLACE  
  
REPT  
  
RIGHT  
  
SUBSTITUTE  
  
TRIM  
  
**统计函数**  
  
COUNT  
  
STDEV.P  
  
STDEV.S  
  
STDEVX.P  
  
STDEVX.S  
  
VAR.P  
  
VAR.S  
  
VARX.P  
  
VARX.S  
  
**日期/时间函数**  
  
DATE  
  
EDATE  
  
EOMONTH  
  
DATE  
  
TIME  
  
SECOND  
  
**数学和数值函数**  
  
CEILING  
  
LN  
  
LOG  
  
LOG10  
  
POWER  
  
**DAX 表查询**  
  
当您针对 DirectQuery 模型使用 DAX 表查询计算公式时，存在一些限制。 DirectQuery 不支持在 ORDER BY 子句中两次引用同一列。 无法创建等效的 Transact-SQL 语句，并且查询将失败。  
  
在内存中模型中，重复 ORDER by 子句对结果没有影响。  
  
## <a name="bkmk_NotSupportedFunc"></a>在 DirectQuery 模式下不支持函数  
对于在 DirectQuery 模式下部署的模型，不支持某些 DAX 函数。 不支持特定函数的原因可能包括以下任一原因或这些原因的组合：  
  
-   基础关系引擎无法执行与由 xVelocity 引擎执行的等效的计算。   
  
-   公式不能转换为等效的 SQL 表达式。  
  
-   转换后的表达式和生成的计算的性能不可接受。  
  
在 DirectQuery 模型中不能使用以下 DAX 函数。  
  
**路径函数**  
  
PATH  
  
PATHCONTAINS  
  
PATHITEM  
  
PATHITEMREVERSE  
  
PATHLENGTH  
  
**杂项函数**  
  
COUNTBLANK  
  
FIXED  
  
FORMAT  
  
RAND  
  
RANDBETWEEN  
  
**时间智能函数： 开始和结束日期**  
  
DATESQTD  
  
DATESYTD  
  
DATESMTD  
  
DATESQTD  
  
DATESINPERIOD  
  
TOTALMTD  
  
TOTALQTD  
  
TOTALYTD  
  
DATESINPERIOD  
  
SAMEPERIODLASTYEAR  
  
PARALLELPERIOD  
  
**时间智能函数： 余额**  
  
OPENINGBALANCEMONTH  
  
OPENINGBALANCEQUARTER  
  
OPENINGBALANCEYEAR  
  
CLOSINGBALANCEMONTH  
  
CLOSINGBALANCEQUARTER  
  
CLOSINGBALANCEYEAR  
  
**时间智能函数： 上一页和下一页句点**  
  
PREVIOUSDAY  
  
PREVIOUSMONTH  
  
PREVIOUSQUARTER  
  
PREVIOUSYEAR  
  
NEXTDAY  
  
NEXTMONTH  
  
NEXTQUARTER  
  
NEXTYEAR  
  
**时间智能函数： 时间段和在一段内的计算**  
  
STARTOFMONTH  
  
STARTOFQUARTER  
  
STARTOFYEAR  
  
ENDOFMONTH  
  
ENDOFQUARTER  
  
ENDOFYEAR  
  
FIRSTDATE  
  
LASTDATE  
  
DATEADD  
  
## <a name="see-also"></a>另请参阅  
[DirectQuery 模式（SSAS 表格）](http://msdn.microsoft.com/en-us/45ad2965-05ec-4fb1-a164-d8060b562ea5)  
  

