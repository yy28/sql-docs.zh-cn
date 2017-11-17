---
title: "CAST 和 CONVERT (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CAST_TSQL
- CONVERT_TSQL
- CAST
- CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- automatic data type conversion
- varbinary data type
- CONVERT function
- data types [SQL Server], converting
- large value data types
- implicit data type conversions
- image data type, converting
- explicit data type conversions [SQL Server]
- binary [SQL Server], converting
- text data type, converting
- date and time [SQL Server], cast and convert
- truncating conversions
- converting data types [SQL Server], conversion functions
- time zones [SQL Server]
- roundtrip conversions
ms.assetid: a87d0850-c670-4720-9ad5-6f5a22343ea8
caps.latest.revision: 136
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: b7f2f78bbda485de979c76076404f35122b61277
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="cast-and-convert-transact-sql"></a>CAST 和 CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

将一种数据类型的表达式转换为另一种数据类型的表达式。  
例如，下面的示例将输入数据类型，更改为两个其他数据类型，具有不同级别的精度。
```sql  
SELECT 9.5 AS Original, CAST(9.5 AS int) AS int, 
    CAST(9.5 AS decimal(6,4)) AS decimal;
SELECT 9.5 AS Original, CONVERT(int, 9.5) AS int, 
    CONVERT(decimal(6,4), 9.5) AS decimal;
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
|源语言   |int    |decimal |  
|----|----|----|  
|9.5 |9 |9.5000 |  

> [!TIP]
> 许多[示例](#BKMK_examples)位于本主题底部。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for CAST:  
CAST ( expression AS data_type [ ( length ) ] )  
  
-- Syntax for CONVERT:  
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )  
```  
  
## <a name="arguments"></a>参数  
*expression*  
是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。
  
*data_type*  
目标数据类型。 这包括**xml**， **bigint**，和**sql_variant**。 不能使用别名数据类型。
  
*length*  
指定目标数据类型长度的可选整数。 默认值为 30。
  
*样式*  
是一个整数表达式指定如何将转换 CONVERT 函数*表达式*。 如果 style为 NULL，则返回 NULL。 范围由*data_type*。 
  
## <a name="return-types"></a>返回类型
返回*表达式*转换为*data_type*。

## <a name="date-and-time-styles"></a>Date 和 Time 样式  
当*表达式*是日期或时间数据类型，*样式*可以是下表中显示的值之一。 其他值作为 0 进行处理。 开头[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 当从转换时，支持的唯一样式日期和时间类型**datetimeoffset**是 0 或 1。 所有其他转换样式均返回错误 9809。
  
>  [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用科威特算法来支持阿拉伯样式的日期格式。
  
|不带世纪 (yy) (<sup>1</sup>)|带世纪数位 (yyyy)|Standard|输入/输出 (<sup>3</sup>)|  
|---|---|--|---|
|-|**0**或**100** (<sup>1，</sup><sup>2</sup>)|datetime 和 smalldatetime 的默认值|mon dd yyyy hh:miAM（或 PM）|  
|**1**|**101**|美国|1 = mm/dd/yy<br /> 101 = mm/dd/yyyy|  
|**2**|**102**|ANSI|2 = yy.mm.dd<br /> 102 = yyyy.mm.dd|  
|**3**|**103**|英国/法国|3 = dd/mm/yy<br /> 103 = dd/mm/yyyy|  
|**4**|**104**|德语|4 = dd.mm.yy<br /> 104 = dd.mm.yyyy|  
|**5**|**105**|意大利语|5 = dd-mm-yy<br /> 105 = dd-mm-yyyy|  
|**6**|**106** <sup>(1)</sup>|-|6 = dd mon yy<br /> 106 = dd mon yyyy|  
|**7**|**107** <sup>(1)</sup>|-|7 = Mon dd, yy<br /> 107 = Mon dd, yyyy|  
|**8**|**108**|-|hh:mi:ss|  
|-|**9**或**109** (<sup>1，</sup><sup>2</sup>)|默认格式 + 毫秒|mon dd yyyy hh:mi:ss:mmmAM（或 PM）|  
|**10**|**110**|USA|10 = mm-dd-yy<br /> 110 = mm-dd-yyyy|  
|**11**|**111**|日本|11 = yy/mm/dd<br /> 111 = yyyy/mm/dd|  
|**12**|**112**|ISO|12 = yymmdd<br /> 112 = yyyymmdd|  
|-|**13**或**113** (<sup>1，</sup><sup>2</sup>)|欧洲默认格式 + 毫秒|dd mon yyyy hh:mi:ss:mmm(24h)|  
|**14**|**114**|-|hh:mi:ss:mmm(24h)|  
|-|**20**或**120** (<sup>2</sup>)|ODBC 规范|yyyy-mm-dd hh:mi:ss(24h)|  
|-|**21**或**121** (<sup>2</sup>)|time、date、datetime2 和 datetimeoffset 的 ODBC 规范（带毫秒）默认值|yyyy-mm-dd hh:mi:ss.mmm(24h)|  
|-|**126** (<sup>4</sup>)|ISO8601|yyyy-mm-ddThh:mi:ss.mmm（无空格）<br /> 注意： 时毫秒的值 (mmm) 为 0，则不显示毫秒值。 例如，值“2012-11-07T18:26:20.000”显示为“2012-11-07T18:26:20”。|  
|-|**127**(<sup>6, 7</sup>)|带时区 Z 的 ISO8601。|yyyy-mm-ddThh:mi:ss.mmmZ（无空格）<br /> 注意： 时毫秒的值 (mmm) 为 0，则不显示毫秒值。 例如，值“2012-11-07T18:26:20.000”显示为“2012-11-07T18:26:20”。|  
|-|**130** (<sup>1,</sup><sup>2</sup>)|回历 (<sup>5</sup>)|dd mon yyyy hh:mi:ss:mmmAM<br /> 在此样式中，mon 表示完整月份名称的多标记回历 unicode 表示形式。 此值不未正确呈现在默认的 SSMS 美国安装。|  
|-|**131** (<sup>2</sup>)|回历 (<sup>5</sup>)|dd/mm/yyyy hh:mi:ss:mmmAM|  
  
<sup>1</sup>这些样式的值将返回具有不确定性的结果。 包括所有 (yy)（不带世纪数位）样式和一部分 (yyyy)（带世纪数位）样式。
  
<sup>2</sup>的默认值 (*样式** *0** 或**100**， **9**或**109**， **13**或**113**， **20**或**120**，和**21**或**121**)始终返回世纪 (yyyy /)。
  
<sup>3</sup>输入转换为**datetime**; 输出转换为字符数据时。
  
<sup>4</sup>专用于 XML。 有关从转换**datetime**或**smalldatetime**为字符数据时，输出格式是上表中所述。
  
<sup>5</sup>回历是具有几种变体的日历系统。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用科威特算法。
  
> [!IMPORTANT]  
>  默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基于截止年份 2049 年来解释两位数的年份。 换言之，就是将两位数的年份 49 解释为 2049，将两位数的年份 50 解释为 1950。 许多客户端应用程序（如基于自动化对象的应用程序）都使用截止年份 2030 年。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供更改使用的截止年份两位数年份截止配置选项[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并允许的日期的一致处理。 建议您指定四位数年份。  
  
<sup>6</sup>到字符数据从强制转换时，才支持**datetime**或**smalldatetime**。 仅表示的字符数据的日期或仅时间组件时被强制转换为**datetime**或**smalldatetime**数据类型未指定的时间组件设置为 00:00:00.000，和未指定日期部分设置为 1900年-01-01。
  
<sup>7</sup>可选时区指示符，Z，用于轻松地映射 XML **datetime**到的时区信息的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**不具有任何时区的值. Z 是时区 UTC-0 的指示符。 其他时区则以 + 或 - 方向的 HH:MM 偏移量来指示。 例如： `2006-12-12T23:45:12-08:00`。
  
当你将转换为字符数据从**smalldatetime**，包括秒或毫秒的样式显示在这些位置的零。 当从转换情况下可以截断不需要的日期部分**datetime**或**smalldatetime**通过使用适当的值**char**或**varchar**数据类型长度。
  
转换为**datetimeoffset**从字符数据，包括时间样式，时区偏移量追加到结果。
  
## <a name="float-and-real-styles"></a>float 和 real 样式
当*表达式*是**float**或**实际**，*样式*可以是下表中显示的值之一。 其他值作为 0 进行处理。
  
|值|“输出”|  
|---|---|
|**0** （默认值）|最多包含 6 位。 根据需要使用科学记数法。|  
|**1**|始终为 8 位值。 始终使用科学记数法。|  
|**2**|始终为 16 位值。 始终使用科学记数法。|  
|**3**|始终为 17 位。 用于无损转换。 使用此样式，每个非重复 float 或真正的价值被保证将转换为不同的字符字符串。<br /> **适用于：** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，启动和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。|  
|**126, 128, 129**|为了保持向后兼容而包括在内，在以后的版本中可能不推荐使用。|  
  
## <a name="money-and-smallmoney-styles"></a>money 和 smallmoney 样式
当*表达式*是**money**或**smallmoney**，*样式*可以是下表中显示的值之一。 其他值作为 0 进行处理。
  
|值|“输出”|  
|---|---|
|**0** （默认值）|小数点左侧每三位数字之间不以逗号分隔，小数点右侧取两位数，例如 4235.98。|  
|**1**|小数点左侧每三位数字之间以逗号分隔，小数点右侧取两位数，例如 3,510.92。|  
|**2**|小数点左侧每三位数字之间不以逗号分隔，小数点右侧取四位数，例如 4235.9819。|  
|**126**|转换为 char(n) 或 varchar(n) 时，等同于样式 2|  
  
## <a name="xml-styles"></a>xml 样式
当*表达式*是**xml***，样式*可以是下表中显示的值之一。 其他值作为 0 进行处理。
  
|值|“输出”|  
|---|---|
|**0** （默认值）|使用默认的分析行为，即放弃无用的空格，且不允许使用内部 DTD 子集。<br /> **注意：**转换为**xml**数据类型，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]无关紧要的空白区域以不同的方式比在中处理 XML 1.0。 有关详细信息，请参阅[创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)。|  
|**1**|保留无用空格。 此样式设置可设置默认值**xml: space**处理相同的行为就像**xml: space ="preserve"**已改为指定。|  
|**2**|启用有限的内部 DTD 子集处理。<br /><br /> 如果启用，则服务器可使用内部 DTD 子集提供的以下信息来执行非验证分析操作。<br /> 的将应用默认值的属性。<br /> -内部实体引用解析并且展开。<br /> 针对语法正确性检查-DTD 内容模型。<br /> 分析器将忽略外部 DTD 子集。 它也不会评估 XML 声明，以查看是否**独立**特性设置**是**或**没有**，但改为分析的 XML 实例，就像它是独立文档。|  
|**3**|保留无用空格，并启用有限的内部 DTD 子集处理。|  
  
## <a name="binary-styles"></a>二进制样式
当*表达式*是**binary(n)**， **varbinary （n)**， **char(n)**，或**varchar(n)**， *样式*可以是下表中显示的值之一。 表中没有列出的样式值将返回错误。
  
|值|“输出”|  
|---|---|
|**0** （默认值）|将 ASCII 字符转换为二进制字节，或者将二进制字节转换为 ASCII 字符。 每个字符或字节按照 1:1 进行转换。<br /> 如果*data_type*是二进制的类型，0x 添加到的结果的左侧的字符。|  
|**1**, **2**|如果*data_type*是二进制的类型，表达式必须为字符表达式。 *表达式*必须是组成偶数个十六进制数字 (0、 1、 2、 3、 4、 5、 6、 7、 8、 9、 A、 B、 C、 D、 E、 F、 a、 b、 c、 d、 e、 f)。 如果*样式*是设置为 1 的字符必须是 0 x 的前两个字符表达式中。 如果表达式中包含的字符数为奇数或者包含任何无效的字符，则会引发错误。<br /> 如果转换后的表达式的长度大于的长度*data_type*结果右截断。<br /> 固定长度*data_types*都大于转换后的结果具有零添加到结果的右侧。<br /> 如果 data_type 为字符类型，则表达式必须为二进制表达式。 每个二进制字符均转换为两个十六进制字符。 如果转换后的表达式的长度大于*data_type*长度，将右截断。<br /> 如果*data_type*是修复大小字符类型和转换后的结果的长度小于其长度*data_type*; 空间添加到转换后的表达式的右侧以维护一个偶数十六进制数字个数。<br /> 0x 将添加到的转换结果的左侧的字符*样式*1。|  
  
## <a name="implicit-conversions"></a>隐式转换
隐式转换指那些没有指定 CAST 或 CONVERT 函数的转换。 显式转换指那些需要指定 CAST 或 CONVERT 函数的转换。 以下图例显示了可对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统提供的数据类型执行的所有显式和隐式数据类型转换。 其中包括**xml**， **bigint**，和**sql_variant**。 在从分配上没有隐式转换**sql_variant**数据类型，但没有隐式转换为**sql_variant**。
  
> [!TIP]  
>  此图表是在一个可下载的 PDF 文件的可用[Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=35834)。  
  
![数据类型转换表](../../t-sql/data-types/media/lrdatahd.png "数据类型转换表")
  
你之间进行转换时**datetimeoffset**和字符类型**char**， **varchar**， **nchar**，和**nvarchar**转换后的时区偏移量的部分应始终为双精度数字 HH 和 MM-例如，08:00。
  
> [!NOTE]  
>  因为 Unicode 数据始终使用偶数个字节时, 要格外小心转换**二进制**或**varbinary**和 Unicode 支持的数据类型。 例如，以下转换不返回 41; 的十六进制值它将返回 4100: `SELECT CAST(CAST(0x41 AS nvarchar) AS varbinary)`。  
  
## <a name="large-value-data-types"></a>大型值数据类型
大型值数据类型显示为其较小的对应项，相同的隐式和显式转换行为专门**varchar**， **nvarchar**和**varbinary**数据类型。 但是，应该考虑以下原则：
-   从转换**映像**到**varbinary （max)**和相反的操作是隐式转换，因此是之间的转换**文本**和**varchar （max)**，和**ntext**和**nvarchar (max)**。  
-   允许从大值数据类型，如**varchar （max)**到较小的对应数据类型，如**varchar**，是隐式转换，但如果的较大值太大了，则会发生截断指定较小的数据类型的长度。  
-   从转换**varchar**， **nvarchar**，或**varbinary**类型隐式执行其相应的大型值数据。  
-   从转换**sql_variant**到大型值数据类型的数据类型为显式转换。  
-   大型值数据类型无法转换为**sql_variant**数据类型。  
  
有关如何将从转换的详细信息**xml**数据类型，请参阅[创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)。
  
## <a name="xml-data-type"></a>xml 数据类型
当你显式或隐式强制转换**xml**数据类型设置为一个字符串或二进制数据类型、 内容**xml**数据类型进行序列化基于一组规则。 有关这些规则的信息，请参阅[定义的 XML 序列化数据](../../relational-databases/xml/define-the-serialization-of-xml-data.md)。 有关如何将从其他数据类型间转换信息**xml**数据类型，请参阅[创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)。
  
## <a name="text-and-image-data-types"></a>文本和图像数据类型
不支持自动的数据类型转换**文本**和**映像**数据类型。 另外，你可以显式转换**文本**为字符数据的数据和**映像**数据到**二进制**或**varbinary**，但最大长度为 8000字节数。 如果你尝试如尝试转换包括到字母的字符表达式不正确转换**int**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回一条错误消息。
  
## <a name="output-collation"></a>输出排序规则  
如果 CAST 或 CONVERT 的输出是字符串，并且输入也是字符串，则输出将与输入具有相同的排序规则和排序规则标签。 如果输入不是字符串，则输出采用数据库的默认排序规则以及强制默认的排序规则标签。 有关详细信息，请参阅[排序规则优先顺序 &#40;Transact SQL &#41;](../../t-sql/statements/collation-precedence-transact-sql.md).
  
若要为输出分配不同的排序规则，请将 COLLATE 子句应用于 CAST 或 CONVERT 函数的结果表达式。 例如：
  
`SELECT CAST('abc' AS varchar(5)) COLLATE French_CS_AS`
  
## <a name="truncating-and-rounding-results"></a>截断和舍入结果
转换字符或二进制表达式时 (**char**， **nchar**， **nvarchar**， **varchar**，**二进制**，或**varbinary**) 到不同的数据类型的表达式，数据可以被截断，只显示部分，或由于结果为太短，无法显示，则返回一个错误。 转换到**char**， **varchar**， **nchar**， **nvarchar**，**二进制**，和**varbinary**会被截断下, 表中所示的转换除外。
  
|被转换的数据类型|转换为的数据类型|结果|  
|---|---|---|
|**int**， **smallint**，或**tinyint**|**char**|*|  
||**varchar**|*|  
||**nchar**|E|  
||**nvarchar**|E|  
|**money**， **smallmoney**，**数值**，**十进制**， **float**，或**实际**|**char**|E|  
||**varchar**|E|  
||**nchar**|E|  
||**nvarchar**|E|  
  
\*= 结果长度太短，无法显示。 E = 因为结果长度太短无法显示而返回错误。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]保证只能往返转换，转换的数据类型转换从原始数据类型并重新生成相同的值版本之间的差异。 以下示例显示的即是这样的往返转换：
  
```sql
DECLARE @myval decimal (5, 2);  
SET @myval = 193.57;  
SELECT CAST(CAST(@myval AS varbinary(20)) AS decimal(10,5));  
-- Or, using CONVERT  
SELECT CONVERT(decimal(10,5), CONVERT(varbinary(20), @myval));  
```  
  
> [!NOTE]  
>  不要尝试构造**二进制**值，然后将它们转换为数值数据类型类别的数据类型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不能保证的结果**十进制**或**数值**数据类型转换为**二进制**都是相同的版本之间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
以下示例显示了由于太小而无法显示的结果表达式。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, SUBSTRING(p.Title, 1, 25) AS Title,
    CAST(e.SickLeaveHours AS char(1)) AS [Sick Leave]  
FROM HumanResources.Employee e JOIN Person.Person p 
    ON e.BusinessEntityID = p.BusinessEntityID  
WHERE NOT e.BusinessEntityID >5;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```   
FirstName   LastName      Title   Sick Leave
---------   ------------- ------- --------`
Ken         Sanchez       NULL   *
Terri       Duffy         NULL   *
Roberto     Tamburello    NULL   *
Rob         Walters       NULL   *
Gail        Erickson      Ms.    *
(5 row(s) affected)  
```
  
转换小数位数不同的数据类型时，结果值有时被截断，有时被舍入。 下表显示了此行为。
  
|From|若要|行为|  
|---|---|---|
|**numeric**|**numeric**|舍入|  
|**numeric**|**int**|截断|  
|**numeric**|**money**|舍入|  
|**money**|**int**|舍入|  
|**money**|**numeric**|舍入|  
|**float**|**int**|截断|  
|**float**|**numeric**|舍入<br /><br /> 转换**float**使用科学记数法到的值**十进制**或**数值**被限制为 17 位精度的值。 精度高于 17 的任何值都将舍入为零。|  
|**float**|**datetime**|舍入|  
|**datetime**|**int**|舍入|  
  
例如，可能截断或舍入到的转换的过程值 10.6496 和-10.6496 **int**或**数值**类型：
  
```sql
SELECT  CAST(10.6496 AS int) as trunc1,
         CAST(-10.6496 AS int) as trunc2,
         CAST(10.6496 AS numeric) as round1,
         CAST(-10.6496 AS numeric) as round2;
 ```
查询结果的以下表所示：
 
|trunc1|trunc2|round1|round2|
|---|---|---|---|
|10|-10|11|-11|
 
在进行数据类型转换时，若目标数据类型的小数位数小于源数据类型的小数位数，则该值将被截断。 例如，以下转换的结果为 `$10.3497`：
  
`SELECT CAST(10.3496847 AS money);`
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回一条错误消息时非数字**char**， **nchar**， **varchar**，或**nvarchar**数据转换为**int**， **float**，**数值**，或**十进制**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]也会返回错误时空字符串 ("") 转换为**数值**或**十进制**。
  
## <a name="certain-datetime-conversions-are-nondeterministic"></a>某些 datetime 转换都是非确定性函数
下表列出了从 string 到 datetime 的转换为不确定性转换的样式。
  
|||  
|-|-|  
|低于 100 的所有样式<sup>1</sup>|106|  
|107|109|  
|113|130|  
  
<sup>1</sup>除了样式 20 和 21
  
## <a name="supplementary-characters-surrogate-pairs"></a>增补字符 （代理项对）
从[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，如果你使用增补字符 (SC) 排序规则，为转换运算从**nchar**或**nvarchar**到**nchar**或**nvarchar**内代理项对的较小的长度的类型将不会截断; 它截断增补字符前面。 例如，以下代码段导致 `@x` 仅保留 `'ab'`。 没有足够的空间来保留增补字符。
  
```sql
DECLARE @x NVARCHAR(10) = 'ab' + NCHAR(0x10000);  
SELECT CAST (@x AS NVARCHAR(3));  
```  
  
在使用 SC 排序规则时，`CONVERT` 行为类似于 `CAST`。
  
## <a name="compatibility-support"></a>兼容性支持
在早期版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，CAST 和 CONVERT 上的操作的默认样式**时间**和**datetime2**数据类型是 121 当在计算的列表达式中使用任一类型除外。 对于计算列，默认样式为 0。 当创建用于涉及自动参数化的查询中或约束定义中的计算列时，此行为会影响计算列。
  
下兼容性级别 110 和更高版本，默认值样式强制转换和转换操作上**时间**和**datetime2**数据类型始终是 121。 如果您的查询依赖旧行为，请使用低于 110 的兼容性级别或在受影响的查询中显式指定 0 样式。
  
将数据库升级到兼容级别 110 或更高将不更改已存储到磁盘的用户数据。 您必须相应手动更正此数据。 例如，如果您使用了 SELECT INTO 来从包含上述计算列表达式的源创建表，将存储数据（使用样式 0）而非存储计算列定义本身。 您需要手动更新此数据，以匹配样式 121。
  
## <a name="BKMK_examples"></a> 示例  
  
### <a name="a-using-both-cast-and-convert"></a>A. 同时使用 CAST 和 CONVERT  
每个示例检索标价的第一位是 `3` 的产品的名称，并将其 `ListPrice` 转换为 `int`。
  
```sql
-- Use CAST  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CAST(ListPrice AS int) LIKE '3%';  
GO  
  
-- Use CONVERT.  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
GO  
```  
  
### <a name="b-using-cast-with-arithmetic-operators"></a>B. 将 CAST 与算术运算符结合使用  
以下示例将本年度截止到现在的全部销售额 (`Computed`) 除以佣金百分比 (`SalesYTD`)，从而得出单列计算结果 (`CommissionPCT`)。 在舍入到最接近的整数后，此结果将转换为 `int` 数据类型。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT CAST(ROUND(SalesYTD/CommissionPCT, 0) AS int) AS Computed  
FROM Sales.SalesPerson   
WHERE CommissionPCT != 0;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```  
Computed
------
379753754
346698349
257144242
176493899
281101272
0  
301872549
212623750
298948202
250784119
239246890
101664220
124511336
97688107
(14 row(s) affected)  
```  
  
### <a name="c-using-cast-to-concatenate"></a>C. 使用 CAST 进行连接  
下面的示例连接通过使用强制转换的非字符表达式。 使用 AdventureWorksDW。
  
```sql
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice  
FROM dbo.DimProduct  
WHERE ListPrice BETWEEN 350.00 AND 400.00;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ListPrice
------------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09  
```  
  
### <a name="d-using-cast-to-produce-more-readable-text"></a>D. 使用 CAST 生成可读性更高的文本  
下面的示例使用强制转换选择列表中要转换`Name`列**char （10)**列。 使用 AdventureWorksDW。
  
```sql
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Name        UnitPrice
----------  ---------
Long-Sleev  31.2437
Long-Sleev  32.4935
Long-Sleev  49.99  
```  
  
### <a name="e-using-cast-with-the-like-clause"></a>E. 将 CAST 与 LIKE 子句一起作用  
以下示例将 `money` 列 `SalesYTD` 转换为 `int` 列，然后再转换为 `char(20)` 列，以便在 `LIKE` 子句中使用该列。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, s.SalesYTD, s.BusinessEntityID  
FROM Person.Person AS p   
JOIN Sales.SalesPerson AS s   
    ON p.BusinessEntityID = s.BusinessEntityID  
WHERE CAST(CAST(s.SalesYTD AS int) AS char(20)) LIKE '2%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
FirstName        LastName            SalesYTD         SalesPersonID
---------------- ------------------- ---------------- -------------
Tsvi             Reiter              2811012.7151      279
Syed             Abbas               219088.8836       288
Rachel           Valdez              2241204.0424      289
(3 row(s) affected)  
```
  
### <a name="f-using-convert-or-cast-with-typed-xml"></a>F. 使用 CONVERT 或 CAST 转换为类型化的 XML  
以下是几个示例显示使用转换来转换为类型化的 XML 使用[XML 数据类型和列 &#40;SQL server&#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md).
  
此示例将包含空格、文本和标记的字符串转换为类型化的 XML，并删除所有无用空格（节点之间的边界空格）:
  
```sql
CONVERT(XML, '<root><child/></root>')  
```  
  
此示例将包含空格、文本和标记的类似字符串转换为类型化的 XML，并保留无用空格（节点之间的边界空格）：
  
```sql
CONVERT(XML, '<root>          <child/>         </root>', 1)  
```  
  
此示例将包含空格、文本和标记的字符串转换为类型化的 XML：
  
```sql
CAST('<Name><FName>Carol</FName><LName>Elliot</LName></Name>'  AS XML)  
```  
  
有关更多示例，请参阅[创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)。
  
### <a name="g-using-cast-and-convert-with-datetime-data"></a>G. 对 datetime 数据使用 CAST 和 CONVERT  
以下示例显示当前日期和时间，使用 `CAST` 将当前日期和时间更改为字符数据类型，然后使用 `CONVERT` 以 `ISO 8901` 格式显示日期和时间。
  
```sql
SELECT   
   GETDATE() AS UnconvertedDateTime,  
   CAST(GETDATE() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), GETDATE(), 126) AS UsingConvertTo_ISO8601  ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast              UsingConvertTo_ISO8601
----------------------- ---------------------- ------------------------------
2006-04-18 09:58:04.570 Apr 18 2006  9:58AM    2006-04-18T09:58:04.570
(1 row(s) affected)  
```
  
以下示例与上述示例几乎完全相反。 该示例将日期和时间显示为字符数据，使用 `CAST` 将字符数据更改为 `datetime` 数据类型，然后使用 `CONVERT` 将字符数据更改为 `datetime` 数据类型。
  
```sql
SELECT   
   '2006-04-25T15:50:59.997' AS UnconvertedText,  
   CAST('2006-04-25T15:50:59.997' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2006-04-25T15:50:59.997', 126) AS UsingConvertFrom_ISO8601 ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2006-04-25T15:50:59.997 2006-04-25 15:50:59.997 2006-04-25 15:50:59.997
(1 row(s) affected)  
```
  
### <a name="h-using-convert-with-binary-and-character-data"></a>H. 使用 CONVERT 处理二进制和字符数据  
以下示例使用不同样式显示转换二进制和字符数据的结果。
  
```sql
--Convert the binary value 0x4E616d65 to a character value.  
SELECT CONVERT(char(8), 0x4E616d65, 0) AS [Style 0, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, binary to character
----------------------------
Name  
(1 row(s) affected)  
```
 
下面的示例演示如何样式 1 可以强制执行结果被截断。 截断被引起包括字符 0x 结果中。  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 1) AS [Style 1, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, binary to character
------------------------------
0x4E616D
(1 row(s) affected)  
```  
 
下面的示例演示样式 2 不因为截断结果 0x 未包含在结果的字符。  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 2) AS [Style 2, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, binary to character
------------------------------
4E616D65
(1 row(s) affected)  
```
  
将 Name 的字符值转换为二进制值。  
```sql
SELECT CONVERT(binary(8), 'Name', 0) AS [Style 0, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, character to binary
----------------------------
0x4E616D6500000000
(1 row(s) affected)  
```
  
```sql
SELECT CONVERT(binary(4), '0x4E616D65', 1) AS [Style 1, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, character to binary
---------------------------- 
0x4E616D65
(1 row(s) affected)  
```  

```sql
SELECT CONVERT(binary(4), '4E616D65', 2) AS [Style 2, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, character to binary  
----------------------------------  
0x4E616D65
(1 row(s) affected)  
```  
  
### <a name="i-converting-date-and-time-data-types"></a>I. 转换日期和时间数据类型  
以下示例演示了日期、时间及 datetime 数据类型的转换。
  
```sql
DECLARE @d1 date, @t1 time, @dt1 datetime;  
SET @d1 = GETDATE();  
SET @t1 = GETDATE();  
SET @dt1 = GETDATE();  
SET @d1 = GETDATE();  
-- When converting date to datetime the minutes portion becomes zero.  
SELECT @d1 AS [date], CAST (@d1 AS datetime) AS [date as datetime];  
-- When converting time to datetime the date portion becomes zero   
-- which converts to January 1, 1900.  
SELECT @t1 AS [time], CAST (@t1 AS datetime) AS [time as datetime];  
-- When converting datetime to date or time non-applicable portion is dropped.  
SELECT @dt1 AS [datetime], CAST (@dt1 AS date) AS [datetime as date], 
   CAST (@dt1 AS time) AS [datetime as time];  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-using-cast-and-convert"></a>J. 使用 CAST 和 CONVERT  
此示例检索的这些产品的产品的名称`3`中其标价并将转换的第一个数字其`ListPrice`到**int**。使用 AdventureWorksDW。
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(ListPrice AS int) LIKE '3%';  
```  
  
此示例演示相同的查询，使用转换而不强制转换。 使用 AdventureWorksDW。
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
```  
  
### <a name="k-using-cast-with-arithmetic-operators"></a>K. 将 CAST 与算术运算符结合使用  
下面的示例计算单个列计算除以产品单位价格 (`UnitPrice`) 按折扣百分比 (`UnitPriceDiscountPct`)。 在舍入到最接近的整数后，此结果将转换为 `int` 数据类型。 使用 AdventureWorksDW。
  
```sql
SELECT ProductKey, UnitPrice,UnitPriceDiscountPct,  
       CAST(ROUND (UnitPrice*UnitPriceDiscountPct,0) AS int) AS DiscountPrice  
FROM dbo.FactResellerSales  
WHERE SalesOrderNumber = 'SO47355'   
      AND UnitPriceDiscountPct > .02;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ProductKey  UnitPrice  UnitPriceDiscountPct  DiscountPrice
----------  ---------  --------------------  -------------
323         430.6445   0.05                  22
213         18.5043    0.05                  1
456         37.4950    0.10                  4
456         37.4950    0.10                  4
216         18.5043    0.05                  1  
```  
  
### <a name="l-using-cast-with-the-like-clause"></a>L. 将 CAST 与 LIKE 子句一起作用  
以下示例将转换**money**列`ListPrice`到**int**类型然后**char(20)**类型，以便它可以用于 LIKE 子句。 使用 AdventureWorksDW。
  
```sql
SELECT EnglishProductName AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(CAST(ListPrice AS int) AS char(20)) LIKE '2%';  
```  
  
### <a name="m-using-cast-and-convert-with-datetime-data"></a>M. 对 datetime 数据使用 CAST 和 CONVERT  
下面的示例显示当前日期和时间，使用强制转换，以将当前日期和时间更改为字符数据类型，并使用转换然后采用 ISO 8601 格式显示了的日期和时间。 使用 AdventureWorksDW。
  
```sql
SELECT TOP(1)  
   SYSDATETIME() AS UnconvertedDateTime,  
   CAST(SYSDATETIME() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), SYSDATETIME(), 126) AS UsingConvertTo_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast                     UsingConvertTo_ISO8601  
---------------------   ---------------------------   ---------------------------  
07/20/2010 1:44:31 PM   2010-07-20 13:44:31.5879025   2010-07-20T13:44:31.5879025  
```  
  
以下示例与上述示例几乎完全相反。 上面的示例显示为字符数据的日期和时间，使用强制转换来更改到的字符数据**datetime**数据类型，然后使用转换，以更改到的字符数据**datetime**数据类型。 使用 AdventureWorksDW。
  
```sql
SELECT TOP(1)   
   '2010-07-25T13:50:38.544' AS UnconvertedText,  
CAST('2010-07-25T13:50:38.544' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2010-07-25T13:50:38.544', 126) AS UsingConvertFrom_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2010-07-25T13:50:38.544 07/25/2010 1:50:38 PM   07/25/2010 1:50:38 PM  
```  
  
## <a name="see-also"></a>另请参阅
[数据类型转换 &#40; 数据库引擎 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)  
[系统函数 &#40;Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[编写国际化 Transact-SQL 语句](../../relational-databases/collations/write-international-transact-sql-statements.md)
  

