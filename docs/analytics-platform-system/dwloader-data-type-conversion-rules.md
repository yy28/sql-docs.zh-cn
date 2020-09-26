---
title: Dwloader 数据类型转换规则
description: 本主题介绍 dwloader 命令行加载程序在将数据加载到并行数据仓库 (PDW) 时支持的输入数据格式和隐式数据类型转换。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c1ce48c3352ffbd0a1c112f7fd60db2f0d85c6e6
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379556"
---
# <a name="data-type-conversion-rules-for-dwloader---parallel-data-warehouse"></a>Dwloader 数据仓库的数据类型转换规则
本主题介绍 [Dwloader 命令行加载程序](dwloader.md) 在 PDW 中加载数据时支持的输入数据格式和隐式数据类型转换。 当输入数据与 SQL Server PDW 目标表中的数据类型不匹配时，将发生隐式数据转换。 在设计加载过程时使用此信息，以确保将数据成功加载到 SQL Server PDW 中。  
   
  
## <a name="inserting-literals-into-binary-types"></a><a name="InsertBinaryTypes"></a>将文本插入二进制类型  
下表定义了接受的文本类型、格式和转换规则，用于将文本值加载到类型为 **binary** (*n*) 或 **varbinary** (*n*) 的 SQL Server PDW 列。  
  
|输入数据类型|输入数据示例|转换为 binary 或 varbinary 数据类型|  
|-------------------|-----------------------|-----------------------------------------------|  
|二进制文本|0x*hexidecimal_string*<br /><br />示例：12Ef 或0x12Ef|0x 前缀是可选的。<br /><br />数据源长度不能超过为数据类型指定的字节数。<br /><br />如果数据源长度小于 **binary** 数据类型的大小，则会将数据填充到右侧，使其达到数据类型大小。|  
  
## <a name="inserting-literals-into-date-and-time-types"></a><a name="InsertDateTimeTypes"></a>将文本插入日期和时间类型  
日期和时间文本是使用特定格式的字符串文本表示的，并用单引号括起来。 下表定义允许的文本类型、格式和转换规则，以便将日期或时间文本加载到类型为 **datetime**、 **smalldatetime**、 **date**、 **time**、 **datetimeoffset**或 **datetime2**的列中。 表定义给定数据类型的默认格式。 可以指定的其他格式在 " [日期时间格式](#DateFormats)" 部分中定义。 日期和时间文字不能包含前导空格或尾随空格。 无法在固定宽度模式下加载**date**、 **smalldatetime**和 null 值。  
  
### <a name="datetime-data-type"></a>datetime 数据类型  
下表定义了用于将文本值加载到类型为 **datetime**的列的默认格式和规则。 空字符串 ( "" ) 转换为默认值 "1900-01-01 12：00： 00.000"。 只包含空格 ( "" ) 生成错误的字符串。  
  
|输入数据类型|输入数据示例|转换为 datetime 数据类型|  
|-------------------|-----------------------|------------------------------------|  
|**Datetime**格式的字符串文本|' yyyy-mm-dd hh： MM： ss [. fff] '<br /><br />示例： "2007-05-08 12：35： 29.123"|在插入值时，缺少小数位设置为0。 例如，文本 "2007-05-08 12:35" 插入为 "2007-05-08 12：35： 00.000"。|  
|**Smalldatetime**格式的字符串文字|' yyyy-mm-dd hh： MM '<br /><br />示例： "2007-05-08 12:35"|在插入值时，秒数和剩余小数位数设置为0。|  
|**日期**格式的字符串文字|"yyyy-mm-dd"<br /><br />示例： "2007-05-08"|在插入值时，时间值 (小时、分钟、秒和小数) 设置为12：00：00.000。|  
|**Datetime2**格式的字符串文本|' yyyy-mm-dd hh： MM： ss. fffffff '<br /><br />示例： "2007-05-08 12：35： 29.1234567"|源数据不能超过三个小数位。 例如，将插入文本 "2007-05-08 12：35： 29.123"，但值 "2007-05-8 12：35： 29.1234567" 生成错误。|  
  
### <a name="smalldatetime-data-type"></a>smalldatetime 数据类型  
下表定义了将文本值加载到类型 **smalldatetime**的列的默认格式和规则。 空字符串 ( "" ) 转换为默认值 "1900-01-01 12:00"。 只包含空格 ( "" ) 生成错误的字符串。  
  
|输入数据类型|输入数据示例|转换为 smalldatetime 数据类型|  
|-------------------|-----------------------|-----------------------------------------|  
|**Smalldatetime**格式的字符串文字|' yyyy-mm-dd hh： mm ' 或 ' yyyy-mm-dd hh： mm： ss '<br /><br />示例： "2007-05-08 12:00" 或 "2007-05-08 12:00:15"|源数据必须具有年、月、日、小时和分钟的值。 秒是可选的，如果存在，则必须设置为值00。 任何其他值将生成错误。<br /><br />秒是可选的。 加载到 smalldatetime 列时，dwloader 将舍入秒和秒的小数部分。 例如，1999-01-05 20：10：35.123 将加载为 01-05 20:11。|  
|**日期**格式的字符串文字|"yyyy-mm-dd"<br /><br />示例： "2007-05-08"|在插入值时，时间值 (小时、分钟、秒和小数) 设置为0。|  
  
### <a name="date-data-type"></a>date 数据类型  
下表定义了用于将文字值加载到 **date**类型的列的默认格式和规则。 空字符串 ( "" ) 转换为默认值 "1900-01-01"。 只包含空格 ( "" ) 生成错误的字符串。  
  
|输入数据类型|输入数据示例|转换为 date 数据类型|  
|-------------------|-----------------------|--------------------------------|  
|**日期**格式的字符串文字|"yyyy-mm-dd"<br /><br />示例： "2007-05-08"||  
  
### <a name="time-data-type"></a>时间数据类型  
下表定义了用于将文本值加载到类型为 **time**的列的默认格式和规则。 空字符串 ( "" ) 转换为默认值 "00：00： 00.0000"。 只包含空格 ( "" ) 生成错误的字符串。  
  
|输入数据类型|输入数据示例|转换为 time 数据类型|  
|-------------------|-----------------------|--------------------------------|  
|**时间**格式的字符串文字|"hh： mm： ss. fffffff"<br /><br />示例： "12：35： 29.1234567"|如果数据源的精度较小或相等 (小数位数) 与 **time** 数据类型的精度相同，则将用零填充数据。 例如，文本值 "12：35： 29.123" 插入为 "12：35： 29.1230000"。|  
  
### <a name="datetimeoffset-data-type"></a>datetimeoffset 数据类型  
下表定义了用于将文本值加载到类型为 **datetimeoffset** (*n*) 的列中的默认格式和规则。 默认格式为 "yyyy-mm-dd hh： MM： ss. fffffff {+ |-} hh： MM"。 空字符串 ( "" ) 转换为默认值 "1900-01-01 12：00： 00.0000000 + 00:00"。 只包含空格 ( "" ) 生成错误的字符串。 小数位数值取决于列定义。 例如，定义为 **datetimeoffset** (2) 的列将具有两个小数位。  
  
|输入数据类型|输入数据示例|转换为 datetimeoffset 数据类型|  
|-------------------|-----------------------|------------------------------------------|  
|**Datetime**格式的字符串文本|' yyyy-mm-dd hh： MM： ss [. fff] '<br /><br />示例： "2007-05-08 12：35： 29.123"|在插入值时，缺少小数位和偏移值设置为0。 例如，文字 "2007-05-08 12：35： 29.123" 被插入为 "2007-05-08 12：35： 29.1230000 + 00:00"。|  
|**Smalldatetime**格式的字符串文字|' yyyy-mm-dd hh： MM '<br /><br />示例： "2007-05-08 12:35"|秒，在插入值时，剩余的小数位数和偏移量值将设置为0。|  
|**日期**格式的字符串文字|"yyyy-mm-dd"<br /><br />示例： "2007-05-08"|在插入值时，时间值 (小时、分钟、秒和小数) 设置为0。 例如，文本 "2007-05-08" 插入为 "2007-05-08 00：00： 00.0000000 + 00:00"。|  
|**Datetime2**格式的字符串文本|' yyyy-mm-dd hh： MM： ss. fffffff '<br /><br />示例： "2007-05-08 12：35： 29.1234567"|源数据不能超过 datetimeoffset 列中指定的秒小数部分。 如果数据源的小数部分的小数位数较小或相等，则使用零将数据填充到右侧。 例如，如果数据类型为 datetimeoffset (5) ，则文本值 "2007-05-08 12：35： 29.123 + 12:15" 将插入为 "12：35： 29.12300 + 12:15"。|  
|**Datetimeoffset**格式的字符串文字|' yyyy-mm-dd hh： MM： ss. fffffff {+&#124;-} hh： MM '<br /><br />示例： "2007-05-08 12：35： 29.1234567 + 12:15"|源数据不能超过 datetimeoffset 列中指定的秒小数部分。 如果数据源的小数部分的小数位数较小或相等，则使用零将数据填充到右侧。 例如，如果数据类型为 datetimeoffset (5) ，则文本值 "2007-05-08 12：35： 29.123 + 12:15" 将插入为 "12：35： 29.12300 + 12:15"。|  
  
### <a name="datetime2-data-type"></a>datetime2 数据类型  
下表定义了用于将文本值加载到类型为 **datetime2** (*n*) 的列的默认格式和规则。 默认格式为 "yyyy-mm-dd hh： MM： ss. fffffff"。 空字符串 ( "" ) 转换为默认值 "1900-01-01 12:00:00"。 只包含空格 ( "" ) 生成错误的字符串。 小数位数值取决于列定义。 例如，定义为 **datetime2** (2) 的列将具有两个小数位。  
  
|输入数据类型|输入数据示例|转换为 datetime2 数据类型|  
|-------------------|-----------------------|-------------------------------------|  
|**Datetime**格式的字符串文本|' yyyy-mm-dd hh： MM： ss [. fff] '<br /><br />示例： "2007-05-08 12：35： 29.123"|秒的小数部分是可选的，并在插入值时设置为0。|  
|**Smalldatetime**格式的字符串文字|' yyyy-mm-dd hh： MM '<br /><br />示例： "2007-05-08 12"|在插入值时，可选的秒数和剩余小数位数设置为0。|  
|**日期**格式的字符串文字|"yyyy-mm-dd"<br /><br />示例： "2007-05-08"|在插入值时，时间值 (小时、分钟、秒和小数) 设置为0。 例如，文本 "2007-05-08" 插入为 "2007-05-08 12：00： 00.0000000"。|  
|**Datetime2**格式的字符串文本|"yyyy-mm-dd hh： MM： ss： fffffff"<br /><br />示例： "2007-05-08 12：35： 29.1234567"|如果数据源包含的数据和时间组成部分小于或等于 **datetime2** (*n*) 中指定的值，则插入数据;否则，会生成错误。|  
  
### <a name="datetime-formats"></a><a name="DateFormats"></a>Datetime 格式  
对于正在加载到 SQL Server PDW 中的输入数据，Dwloader 支持以下数据格式。 表中列出了更多详细信息。  
  
|datetime|smalldatetime|date|datetime2|datetimeoffset|  
|------------|-----------------|--------|-------------|------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[yy]yy HH:mm[:00]|[M[M]]M-[d]d-[yy]yy|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm[:00][tt]||[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm[:00][tt]||[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm[:00][tt]||[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[yy]yy-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm[:00][tt]||[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fff]|[d]d-[M[M]]M-[yy]yy HH:mm[:00]|[d]d-[M[M]]M-[yy]yy|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm[:00][tt]||[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[yy]yy-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm[:00][tt]||[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
详细信息：  
  
-   若要分隔月、日和年份值，你可以使用 "-"、"/" 或 ""。 '. 为简单起见，该表仅使用“-”分隔符。  
  
-   若要将月份指定为文本，请使用三个或更多字符。 包含1或2个字符的月份将被解释为数字。  
  
-   若要分隔时间值，请使用 '： ' 符号。  
  
-   括在方括号中的字母是可选的。  
  
-   字母“tt”指定 [AM|PM|am|pm]。 AM 是默认值。 当指定“tt”时，小时值 (hh) 必须在 0 到 12 范围内。  
  
-   字母“zzz”以格式 {+|-}HH:ss] 为系统的当前时区指定时区偏移。  
  
## <a name="inserting-literals-into-numeric-types"></a><a name="InsertNumerictypes"></a>将文本插入数值类型  
下表定义了用于将文本值加载到使用数值类型的 SQL Server PDW 列的默认格式和转换规则。  
  
### <a name="bit-data-type"></a>bit 数据类型  
下表定义了用于将文本值加载到类型为 **bit**的列的默认格式和规则。 空字符串 ( "" ) 或只包含空白的字符串 ( "" ) 转换为0。  
  
|输入数据类型|输入数据示例|转换为 bit 数据类型|  
|-------------------|-----------------------|-------------------------------|  
|**整数**格式的字符串文字|'ffffffffff'<br /><br />示例： "1" 或 "321"|格式为字符串文字的整数值不能包含负值。 例如，值 "-123" 生成错误。<br /><br />大于1的值将转换为1。 例如，值 "123" 将转换为1。|  
|字符串文本|"TRUE" 或 "FALSE"<br /><br />示例： "true"|值 "TRUE" 转换为 1;值 "FALSE" 转换为0。|  
|整数文本|fffffffn<br /><br />示例：1或321|大于1或小于0的值将转换为1。 例如，将值123和-123 转换为1。|  
|Decimal 文本|fffnn.fffn<br /><br />示例：1234.5678|大于1或小于0的值将转换为1。 例如，将值123.45 和-123.45 转换为1。|  
  
### <a name="decimal-data-type"></a>decimal 数据类型  
下表定义了将文本值加载到类型为 **decimal** (*p，s*) 的列的规则。 数据转换规则与 SQL Server 相同。 有关详细信息，请参阅 MSDN 上的 [数据类型转换 (数据库引擎) ](/previous-versions/sql/sql-server-2008-r2/ms191530(v=sql.105)) 。  
  
|输入数据类型|输入数据示例|  
|-------------------|-----------------------|  
|整数文本|321312313123|  
|Decimal 文本|123344.34455|  
  
### <a name="float-and-real-data-types"></a>float 和 real 数据类型  
下表定义了将文本值加载到 **float** 或 **real**类型的列的规则。 数据转换规则与 SQL Server 相同。 有关详细信息，请参阅 MSDN 上的 [数据类型转换 (数据库引擎) ](../t-sql/data-types/data-type-conversion-database-engine.md) 。  
  
|输入数据类型|输入数据示例|  
|-------------------|-----------------------|  
|整数文本|321312313123|  
|Decimal 文本|123344.34455|  
|浮点型文本|3.12323 e + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int、bigint、tinyint、smallint 数据类型  
下表定义了用于将文本值加载到类型为 **int**、 **bigint**、 **tinyint**或 **smallint**的列的规则。 数据源不能超出给定数据类型允许的范围。 例如， **tinyint** 的范围为0到255， **int** 的范围为-2147483648 到2147483647。  
  
|输入数据类型|输入数据示例|转换为整数数据类型|  
|-------------------|-----------------------|------------------------------------|  
|整数文本|321312313123||  
|Decimal 文本|123344.34455|小数点右边的值将被截断。|  
  
### <a name="money-and-smallmoney-data-types"></a>money 和 smallmoney 数据类型  
Money 文本值使用可选的小数点和可选的货币符号作为前缀来表示。 数据源不能超出给定数据类型允许的范围。 例如， **smallmoney** 的范围为-214748.3648 到214748.3647，而 **货币** 的范围为-922337203685477.5808 到922337203685477.5807。 下表定义了将文本值加载到 **money** 或 **smallmoney**类型的列的规则。  
  
|输入数据类型|输入数据示例|转换为 money 或 smallmoney 数据类型|  
|-------------------|-----------------------|-----------------------------------------------|  
|整数文本|321312|在插入值时，小数点后缺少的位数设置为0。 例如，文本12345插入为12345.0000|  
|Decimal 文本|123344.34455|如果小数点后的位数超过4，则该值向上舍入到最接近的值。 例如，将值123344.34455 插入为123344.3446。|  
|Money 文本|$123456.7890|货币符号不是以值插入的。<br /><br />如果小数点后的位数超过4，则该值向上舍入到最接近的值。|  
  
## <a name="inserting-literals-into-string-types"></a><a name="InsertStringTypes"></a>将文本插入字符串类型  
下表定义了用于将文本值加载到使用字符串类型 SQL Server PDW 列的默认格式和转换规则。  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>char、varchar、nchar 和 nvarchar 数据类型  
下表定义了用于将文本值加载到类型 **char**、 **varchar**、 **nchar** 和 **nvarchar**的列的默认格式和规则。 数据源长度不能超过为数据类型指定的大小。 如果数据源长度小于 **char** 或 **nchar** 数据类型的大小，则会将数据填充到右侧，并用空格来达到数据类型大小。  
  
|输入数据类型|输入数据示例|转换为字符数据类型|  
|---------------|-------------------|----------------------------------|  
|字符串文本|格式： "string"<br /><br />示例： "abc"| NA |  
|Unicode 字符串文本|格式： N'character string '<br /><br />示例： N'abc '| NA |  
|整数文本|格式： ffffffffffn<br /><br />示例：321312313123| NA |  
|Decimal 文本|格式： ffffff. fffffff<br /><br />示例：12344.34455| NA |  
|Money 文本|格式： $ffffff. fffnn<br /><br />示例： $123456.99|可选的货币符号不会插入值。 若要插入货币符号，请将值作为字符串文本插入。 这将与加载器的格式匹配，后者将每个文本视为字符串文字。<br /><br />不允许使用逗号。<br /><br />如果小数点后的位数超过2，则该值将向上舍入到最接近的值。 例如，将值123.946789 插入为123.95。<br /><br />当使用 CONVERT 函数插入 money 文本时，仅允许默认样式 0 (小数点后两位数) 。|  
  
### <a name="general-remarks"></a>一般备注  
**dwloader** 执行 smp SQL Server 执行的相同隐式转换，但不支持 smp SQL Server 支持的所有隐式转换。  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
