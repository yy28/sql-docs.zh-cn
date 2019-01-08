---
title: Dwloader 的数据类型转换规则-并行数据仓库 |Microsoft Docs
description: 本主题介绍的输入的数据格式和隐式数据类型转换时将数据加载到并行数据仓库 (PDW) 命令行加载程序支持该 dwloader。"
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 46d092ee5d3b981c60d7bd5bde49f9994dab4b08
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52519577"
---
# <a name="data-type-conversion-rules-for-dwloader---parallel-data-warehouse"></a>数据类型转换规则适用于 dwloader 的并行数据仓库
本主题介绍的输入的数据格式和隐式数据类型转换的[dwloader 命令行加载程序](dwloader.md)时它将数据加载到 PDW 支持。 输入的数据与 SQL Server PDW 目标表中的数据类型不匹配时，会发生隐式数据转换。 当设计加载过程以确保你的数据将载入 SQL Server PDW 成功时，请使用此信息。  
   
  
## <a name="InsertBinaryTypes"></a>将文本插入到二进制类型  
下表定义可接受文本的类型、 格式和加载到 SQL Server PDW 类型的列的文本值的转换规则**二进制**(*n*) 或**varbinary**(*n*)。  
  
|输入的数据类型|输入的数据示例|转换为 binary 或 varbinary 数据类型|  
|-------------------|-----------------------|-----------------------------------------------|  
|二进制文字|[0x]*hexidecimal_string*<br /><br />例如：12Ef 或 0x12Ef|0x 前缀是可选的。<br /><br />数据源长度不能超过指定的数据类型的字节数。<br /><br />如果数据源长度的大小小于**二进制**数据类型，数据被填充为零的权限访问的数据类型大小。|  
  
## <a name="InsertDateTimeTypes"></a>将文本插入到日期和时间类型  
通过使用字符串文本括在单引号内的特定格式表示日期和时间文本。 下表定义了允许的文本类型、 格式和转换规则加载到类型的列的日期或时间文字**datetime**， **smalldatetime**，**日期**，**时间**， **datetimeoffset**，或**datetime2**。 表定义的默认格式为给定的数据类型。 可以指定其他格式节中定义[日期时间格式](#DateFormats)。 日期和时间文本不能包含前导或尾部空格。 **日期**， **smalldatetime**，并且不能在固定的宽度模式下加载 null 值。  
  
### <a name="datetime-data-type"></a>datetime 数据类型  
下表定义了默认的格式，用于将加载到类型的列的文本值的规则**datetime**。 空字符串 （"） 转换的默认值为 1900年-01-01 12:00:00.000。 包含仅空格的字符串 () 生成错误。  
  
|输入的数据类型|输入的数据示例|转换为 datetime 数据类型|  
|-------------------|-----------------------|------------------------------------|  
|字符串文本用**datetime**格式|年-月-日 hh: mm: [.fff]'<br /><br />例如：2007年-05-08 12:35:29.123|插入值时，缺少的小数位数将设置为 0。 例如，文本 2007年-05-08 12:35 作为插入 2007年-05-08 12:35:00.000。|  
|字符串文本用**smalldatetime**格式|年-月-日 hh: mm<br /><br />例如：2007年-05-08 12:35|秒数和剩余的小数位数设置为 0 时插入的值。|  
|字符串文本用**日期**格式|年-月-日<br /><br />例如：2007年-05-08'|时间 （小时、 分钟、 秒和小数部分） 的值设置为 12:00:00.000 时插入的值。|  
|字符串文本用**datetime2**格式|年-月-日： ss.fffffff<br /><br />例如：2007年-05-08 12:35:29.1234567|源数据不能超过三个小数位数。 例如，文本 2007年-05-08 12:35:29.123 将插入，但值 2007年-05-8 12:35:29.1234567 将生成错误。|  
  
### <a name="smalldatetime-data-type"></a>smalldatetime 数据类型  
下表定义了默认的格式，用于将加载到类型的列的文本值的规则**smalldatetime**。 空字符串 （"） 转换的默认值为 1900年-01-01 12:00。 包含仅空格的字符串 () 生成错误。  
  
|输入的数据类型|输入的数据示例|转换为 smalldatetime 数据类型|  
|-------------------|-----------------------|-----------------------------------------|  
|字符串文本用**smalldatetime**格式|年-月-日 hh: mm 或者年-月-日 hh: mm:<br /><br />例如：2007年-05-08 12:00 或 2007年-05-08 12:00:15|源数据必须具有对年、 月、 日期、 小时和分钟值。 秒是可选的并且如果存在，必须设置为 00 的值。 任何其他值将生成错误。<br /><br />秒是可选的。 当加载到 smalldatetime 列，dwloader 将向上秒和秒的小数部分舍入。 例如，1999年-01-05 20:10:35.123 将加载为 01 05 20:11。|  
|字符串文本用**日期**格式|年-月-日<br /><br />例如：2007年-05-08'|时间 （小时、 分钟、 秒和小数部分） 的值设置为 0 时插入的值。|  
  
### <a name="date-data-type"></a>date 数据类型  
下表定义了默认的格式，用于将加载到类型的列的文本值的规则**日期**。 空字符串 （"） 转换的默认值为 1900年-01-01。 包含仅空格的字符串 () 生成错误。  
  
|输入的数据类型|输入的数据示例|转换为日期数据类型|  
|-------------------|-----------------------|--------------------------------|  
|字符串文本用**日期**格式|年-月-日<br /><br />例如：2007年-05-08'||  
  
### <a name="time-data-type"></a>时间数据类型  
下表定义了默认的格式，用于将加载到类型的列的文本值的规则**时间**。 空字符串 （"） 转换为默认值"00:00:00.0000"。 包含仅空格的字符串 () 生成错误。  
  
|输入的数据类型|输入的数据示例|转换为时间数据类型|  
|-------------------|-----------------------|--------------------------------|  
|字符串文本用**时间**格式|'hh:mm:ss.fffffff'<br /><br />例如："12:35:29.1234567"|如果数据源有小于或等于精度 （数字的小数位数） 的精度大于**时间**数据类型，数据填充到右侧的零。 例如，作为"12:35:29.1230000"插入文本值"12:35:29.123"。|  
  
### <a name="datetimeoffset-data-type"></a>datetimeoffset 数据类型  
下表定义了默认的格式，用于将加载到类型的列的文本值的规则**datetimeoffset** (*n*)。 默认格式是年-月-日： ss.fffffff {+ |-} hh: mm。 空字符串 （"） 转换的默认值为 1900年-01-01 12:00:00.0000000 + 00:00。 包含仅空格的字符串 () 生成错误。 小数位数取决于列定义。 例如，定义为的列**datetimeoffset** (2) 将具有两个小数位。  
  
|输入的数据类型|输入的数据示例|转换为 datetimeoffset 数据类型|  
|-------------------|-----------------------|------------------------------------------|  
|字符串文本用**datetime**格式|年-月-日 hh: mm: [.fff]'<br /><br />例如：2007年-05-08 12:35:29.123|缺少的小数位数和偏移量的值设置为 0 时插入的值。 例如，文本 2007年-05-08 12:35:29.123 作为插入 2007年-05-08 12:35:29.1230000 + 00:00。|  
|字符串文本用**smalldatetime**格式|年-月-日 hh: mm<br /><br />例如：2007年-05-08 12:35|插入值时，秒、 剩余的小数位数和偏移量的值都设置为 0。|  
|字符串文本用**日期**格式|年-月-日<br /><br />例如：2007年-05-08'|时间 （小时、 分钟、 秒和小数部分） 的值设置为 0 时插入的值。 例如，文字"2007年-05-08 作为插入 2007年-05-08 00:00:00.0000000 + 00:00。|  
|字符串文本用**datetime2**格式|年-月-日： ss.fffffff<br /><br />例如：2007年-05-08 12:35:29.1234567|源数据不能超过指定的 datetimeoffset 列中的小数秒数。 如果数据源具有小于或等于数秒的小数部分，右侧用零填充数据。 例如，如果数据类型为 datetimeoffset (5)，文本值 2007年-05-08 12:35:29.123 + 12:15 作为插入 12:35:29.12300 + 12:15。|  
|字符串文本用**datetimeoffset**格式|年-月-日： ss.fffffff {+&#124;-} hh: mm<br /><br />例如：2007年-05-08 12:35:29.1234567 + 12:15|源数据不能超过指定的 datetimeoffset 列中的小数秒数。 如果数据源具有小于或等于数秒的小数部分，右侧用零填充数据。 例如，如果数据类型为 datetimeoffset (5)，文本值 2007年-05-08 12:35:29.123 + 12:15 作为插入 12:35:29.12300 + 12:15。|  
  
### <a name="datetime2-data-type"></a>datetime2 数据类型  
下表定义了默认的格式，用于将加载到类型的列的文本值的规则**datetime2** (*n*)。 默认格式为年-月-日： ss.fffffff。 空字符串 （"） 转换的默认值为 1900年-01-01 12:00:00。 包含仅空格的字符串 () 生成错误。 小数位数取决于列定义。 例如，定义为的列**datetime2** (2) 将具有两个小数位。  
  
|输入的数据类型|输入的数据示例|转换为 datetime2 数据类型|  
|-------------------|-----------------------|-------------------------------------|  
|字符串文本用**datetime**格式|年-月-日 hh: mm: [.fff]'<br /><br />例如：2007年-05-08 12:35:29.123|秒的小数部分是可选的当插入的值设置为 0。|  
|字符串文本用**smalldatetime**格式|年-月-日 hh: mm<br /><br />例如：2007年-05-08 12|可选秒数和剩余的小数位数设置为 0 时插入的值。|  
|字符串文本用**日期**格式|年-月-日<br /><br />例如：2007年-05-08'|时间 （小时、 分钟、 秒和小数部分） 的值设置为 0 时插入的值。 例如，文字"2007年-05-08 作为插入 2007年-05-08 12:00:00.0000000。|  
|字符串文本用**datetime2**格式|年-月-日 hh:mm:ss:fffffff<br /><br />例如：2007年-05-08 12:35:29.1234567|如果数据源包含数据和时间是小于或等于中指定的值的组件**datetime2**(*n*)，则数据将插入; 否则将生成错误。|  
  
### <a name="DateFormats"></a>日期时间格式  
Dwloader 加载到 SQL Server PDW 的输入数据支持下列数据格式。 表后列出了更多详细信息。  
  
|DATETIME|smalldatetime|日期|datetime2|datetimeoffset|  
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
  
-   若要分隔月、 日和年值，可以使用 '-'，'/' 或 '。 '. 为简单起见，该表仅使用“-”分隔符。  
  
-   若要指定以文本形式的月份，请使用三个或多个字符。 几个月使用 1 或 2 个字符将解释为数字。  
  
-   若要分隔时间值，请使用: 符号。  
  
-   括在方括号中的字母是可选的。  
  
-   字母“tt”指定 [AM|PM|am|pm]。 AM 是默认值。 当指定“tt”时，小时值 (hh) 必须在 0 到 12 范围内。  
  
-   字母“zzz”以格式 {+|-}HH:ss] 为系统的当前时区指定时区偏移。  
  
## <a name="InsertNumerictypes"></a>将文本插入到数值类型  
下表定义加载到使用数值类型的 SQL Server PDW 列的文本值的默认格式和转换规则。  
  
### <a name="bit-data-type"></a>bit 数据类型  
下表定义了默认的格式，用于将加载到类型的列的文本值的规则**位**。 空字符串 （"） 或一个字符串，包含仅空格 () 转换为 0。  
  
|输入的数据类型|输入的数据示例|转换为 bit 数据类型|  
|-------------------|-----------------------|-------------------------------|  
|字符串文本用**整数**格式|ffffffffff<br /><br />例如："1"或者"321"|一个整数值格式化为字符串文字不能包含负值。 例如，"-123"的值将生成错误。<br /><br />大于 1 的值转换为 1。 例如，"123"的值转换为 1。|  
|字符串文本|'TRUE' 或者 'FALSE'<br /><br />示例: ' true'|值 'TRUE' 转换为 1;值 'FALSE' 转换为 0。|  
|整数文本|fffffffn<br /><br />例如：1 或 321|大于 1 或小于 0 的值转换为 1。 例如，值 123 和-123 都转换为 1。|  
|十进制文本|fffnn.fffn<br /><br />例如：1234.5678|大于 1 或小于 0 的值转换为 1。 例如，将 123.45 和-123.45 的值转换为 1。|  
  
### <a name="decimal-data-type"></a>Decimal 数据类型  
下表定义的文本值加载到类型的列的规则**十进制**(*p，s*)。 数据转换规则都与 SQL Server 相同。 有关详细信息，请参阅[数据类型转换 （数据库引擎）](https://go.microsoft.com/fwlink/?LinkId=202128) MSDN 上。  
  
|输入的数据类型|输入的数据示例|  
|-------------------|-----------------------|  
|整数文本|321312313123|  
|十进制文本|123344.34455|  
  
### <a name="float-and-real-data-types"></a>float 和 real 数据类型  
下表定义的文本值加载到类型的列的规则**float**或**实际**。 数据转换规则都与 SQL Server 相同。 有关详细信息，请参阅[数据类型转换 （数据库引擎）](../t-sql/data-types/data-type-conversion-database-engine.md) MSDN 上。  
  
|输入的数据类型|输入的数据示例|  
|-------------------|-----------------------|  
|整数文本|321312313123|  
|十进制文本|123344.34455|  
|浮点型|3.12323E+14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int、 bigint、 tinyint、 smallint 数据类型  
下表定义的文本值加载到类型的列的规则**int**， **bigint**， **tinyint**，或者**smallint**。 数据源不能超过给定的数据类型允许的范围。 例如，对于范围**tinyint**是 0 到 255 和范围**int**为-2,147,483,648 到 2,147,483,647。  
  
|输入的数据类型|输入的数据示例|到整数数据类型转换|  
|-------------------|-----------------------|------------------------------------|  
|整数文本|321312313123||  
|十进制文本|123344.34455|小数点右侧的值将被截断。|  
  
### <a name="money-and-smallmoney-data-types"></a>money 和 smallmoney 数据类型  
可选的小数点和可选的货币符号作为前缀的数字字符串形式表示 money 文字值。 数据源不能超过给定的数据类型允许的范围。 例如，对于范围**smallmoney**是-214，748.3648 214，748.3647 和范围**资金**是-922,337,203,685,477.5808 到 922,337,203,685,477.5807。 下表定义的文本值加载到类型的列的规则**资金**或**smallmoney**。  
  
|输入的数据类型|输入的数据示例|转换为 money 或 smallmoney 数据类型|  
|-------------------|-----------------------|-----------------------------------------------|  
|整数文本|321312|缺少数字后的小数位数将设置为 0 时插入的值。 例如，作为 12345.0000 插入文字 12345|  
|十进制文本|123344.34455|如果小数点后的位数超过 4，值舍入为最接近的值。 例如，作为 123344.3446 插入值 123344.34455。|  
|Money 文字|$123456.7890|货币符号不插入的值。<br /><br />如果小数点后的位数超过 4，值舍入为最接近的值。|  
  
## <a name="InsertStringTypes"></a>将文本插入到字符串类型  
下表定义加载到使用字符串类型的 SQL Server PDW 列的文本值的默认格式和转换规则。  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>char、 varchar、 nchar 和 nvarchar 数据类型  
下表定义了默认的格式，用于将加载到类型的列的文本值的规则**char**， **varchar**， **nchar**和**nvarchar**. 数据源长度不能超过指定的数据类型的大小。 如果数据源长度的大小小于**char**或**nchar**数据类型，数据填充到右侧的空白区域以达到数据类型大小。  
  
|输入的数据类型|输入的数据示例|转换为字符数据类型|  
|---------------|-------------------|----------------------------------|  
|字符串文本|格式: 字符串<br /><br />示例: ' abc'| 不适用 |  
|Unicode 字符串文本|格式：N'character 字符串<br /><br />例如：N'abc'| 不适用 |  
|整数文本|格式： ffffffffffn<br /><br />例如：321312313123| 不适用 |  
|十进制文本|格式： ffffff.fffffff<br /><br />例如：12344.34455| 不适用 |  
|Money 文字|格式： $ffffff.fffnn<br /><br />示例: $ 123456.99|可选的货币符号不插入的值。 若要插入的货币符号，请为字符串文字插入的值。 这将与加载程序，将每个文本视为文字字符串的格式匹配。<br /><br />不允许使用逗号。<br /><br />如果小数点后的位数超过 2，值舍入为最接近的值。 例如，作为 123.95 插入值 123.946789。<br /><br />使用 CONVERT 函数将 money 的文本，则允许仅默认样式 0 （不以逗号分隔，小数点后的 2 位数）。|  
  
### <a name="general-remarks"></a>一般备注  
**dwloader**执行 SMP SQL Server 执行，但不支持隐式转换的所有 SMP SQL Server 支持的相同的隐式转换。  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  
