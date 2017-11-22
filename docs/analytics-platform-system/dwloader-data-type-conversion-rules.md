---
title: "数据类型 dwloader 的转换的规则"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "本主题介绍该 dwloader 命令行加载程序时将数据加载到 PDW 支持的输入的数据格式和隐式数据类型转换。"
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 79c48520-b08b-4b15-a943-a551cc90a2c4
caps.latest.revision: "30"
ms.openlocfilehash: 2ac1325b3765bafbe34dc61f65f7641431afdfa0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="data-type-conversion-rules-for-dwloader"></a>数据类型 dwloader 的转换的规则
本主题介绍的输入的数据格式和隐式数据类型转换， [dwloader 命令行加载程序](dwloader.md)时它将数据加载到 PDW 支持。 隐式数据转换发生时输入的数据与 SQL Server PDW 目标表中的数据类型不匹配。 在设计你的加载过程以确保你的数据将载入 SQL Server PDW 成功时，请使用此信息。  
   
  
## <a name="InsertBinaryTypes"></a>将文本插入到二进制类型  
下表定义接受文本的类型、 格式和用于加载到类型的 SQL Server PDW 列的文本值的转换规则**二进制**(*n*) 或**varbinary**(*n*)。  
  
|输入的数据类型|输入的数据示例|转换为 binary 或 varbinary 数据类型|  
|-------------------|-----------------------|-----------------------------------------------|  
|二进制文本|[0 x]*hexidecimal_string*<br /><br />示例： 12Ef 或 0x12Ef|0x 前缀是可选的。<br /><br />数据源长度不能超过为数据类型指定的字节数。<br /><br />如果数据源长度小于大小**二进制**数据类型，数据填充到用零权访问的数据类型大小。|  
  
## <a name="InsertDateTimeTypes"></a>将文本插入到日期和时间类型  
通过使用特定的格式，用单引号括起来的字符串文本表示日期和时间的文本。 下表定义了允许的文本类型、 格式和的加载日期或时间文字，到类型的列的转换规则**datetime**， **smalldatetime**，**日期**，**时间**， **datetimeoffset**，或**datetime2**。 表定义了给定的数据类型的默认格式。 可以指定其他格式在节定义[日期时间格式](#DateFormats)。 日期和时间的文本不能包含前导空格或尾随空格。 **日期**， **smalldatetime**，和 null 值不能在固定的宽度模式下加载。  
  
### <a name="datetime-data-type"></a>datetime 数据类型  
下表定义的默认格式和将文字值加载到类型的列的规则**datetime**。 空字符串 （"） 转换为默认值 1900年-01-01 12:00:00.000。 包含仅空格的字符串 () 生成错误。  
  
|输入的数据类型|输入的数据示例|转换为 datetime 数据类型|  
|-------------------|-----------------------|------------------------------------|  
|字符串括起来**datetime**格式|yyyy MM dd hh: mm: [.fff]<br /><br />示例: 2007年-05-08 12:35:29.123|插入值时，缺少小数位数均设置为 0。 例如，文本 2007年-05-08 12:35 作为插入 2007年-05-08 12:35:00.000。|  
|字符串括起来**smalldatetime**格式|yyyy MM dd hh: mm<br /><br />示例: 2007年-05-08 12:35|秒数和剩余的小数位数设置为 0 时插入的值。|  
|字符串括起来**日期**格式|yyyy-月-日<br /><br />示例: 2007年-05-08|时间值 （小时、 分钟、 秒和秒的小数部分） 设置为 12:00:00.000 时插入的值。|  
|字符串括起来**datetime2**格式|yyyy-月-日 hh:mm:ss.fffffff<br /><br />示例: 2007年-05-08 12:35:29.1234567|源数据不能超过三个小数位。 例如，文本 2007年-05-08 12:35:29.123 将插入，但该值 ' 2007年-05-8 12:35:29.1234567 会生成错误。|  
  
### <a name="smalldatetime-data-type"></a>smalldatetime 数据类型  
下表定义的默认格式和将文字值加载到类型的列的规则**smalldatetime**。 空字符串 （"） 转换为默认值 1900年-01-01 12:00。 包含仅空格的字符串 () 生成错误。  
  
|输入的数据类型|输入的数据示例|转换为 smalldatetime 数据类型|  
|-------------------|-----------------------|-----------------------------------------|  
|字符串括起来**smalldatetime**格式|yyyy MM dd hh: mm 或者 yyyy MM dd hh: mm:<br /><br />示例: 2007年-05-08 12:00 或 2007年-05-08 12:00:15|源数据必须为年、 月、 日期、 小时和分钟的值。 秒是可选的并且如果存在，必须设置为 00 的值。 任何其他值将生成错误。<br /><br />秒是可选的。 在加载到 smalldatetime 列，dwloader 将轮秒和秒的小数部分。 例如，1999年-01-05 20:10:35.123 将加载为 01-05 20:11。|  
|字符串括起来**日期**格式|yyyy-月-日<br /><br />示例: 2007年-05-08|插入值时，时间值 （小时、 分钟、 秒和秒的小数部分） 将设置为 0。|  
  
### <a name="date-data-type"></a>date 数据类型  
下表定义的默认格式和将文字值加载到类型的列的规则**日期**。 空字符串 （"） 转换为默认值 1900年-01-01。 包含仅空格的字符串 () 生成错误。  
  
|输入的数据类型|输入的数据示例|转换为日期数据类型|  
|-------------------|-----------------------|--------------------------------|  
|字符串括起来**日期**格式|yyyy-月-日<br /><br />示例: 2007年-05-08||  
  
### <a name="time-data-type"></a>时间数据类型  
下表定义的默认格式和将文字值加载到类型的列的规则**时间**。 空字符串 （"） 转换为默认值"00:00:00.0000"。 包含仅空格的字符串 () 生成错误。  
  
|输入的数据类型|输入的数据示例|转换为时间数据类型|  
|-------------------|-----------------------|--------------------------------|  
|字符串括起来**时间**格式|hh:mm:ss.fffffff<br /><br />示例:"12:35:29.1234567"|如果数据源都具有一个小于或等于精度 （数字的小数位数） 比的精度**时间**数据类型，数据填充到零右侧。 例如，文本值"12:35:29.123"可作为"12:35:29.1230000"插入。|  
  
### <a name="datetimeoffset-data-type"></a>datetimeoffset 数据类型  
下表定义的默认格式和将文字值加载到类型的列的规则**datetimeoffset** (*n*)。 默认格式是 ' yyyy-月-日 hh:mm:ss.fffffff {+ |-} hh: mm。 空字符串 （"） 转换为默认值 1900年-01-01 12:00:00.0000000 + 00:00。 包含仅空格的字符串 () 生成错误。 小数位数取决于列定义。 例如，定义为一列**datetimeoffset** (2) 将具有两个小数位。  
  
|输入的数据类型|输入的数据示例|转换 datetimeoffset 数据类型|  
|-------------------|-----------------------|------------------------------------------|  
|字符串括起来**datetime**格式|yyyy MM dd hh: mm: [.fff]<br /><br />示例: 2007年-05-08 12:35:29.123|插入值时，缺少小数位数和偏移量的值将设置为 0。 例如，文本 2007年-05-08 12:35:29.123 作为插入 2007年-05-08 12:35:29.1230000 + 00:00。|  
|字符串括起来**smalldatetime**格式|yyyy MM dd hh: mm<br /><br />示例: 2007年-05-08 12:35|插入值时，秒、 剩余的小数位数和偏移量的值将设置为 0。|  
|字符串括起来**日期**格式|yyyy-月-日<br /><br />示例: 2007年-05-08|插入值时，时间值 （小时、 分钟、 秒和秒的小数部分） 将设置为 0。 例如，文本"2007年-05-08 作为插入 2007年-05-08 00:00:00.0000000 + 00:00。|  
|字符串括起来**datetime2**格式|yyyy-月-日 hh:mm:ss.fffffff<br /><br />示例: 2007年-05-08 12:35:29.1234567|源数据不能超过指定的 datetimeoffset 列中的小数秒数。 如果数据源具有小于或等于的小数部分组成的秒数，则用零右侧填充数据。 例如，如果数据类型是 datetimeoffset (5) 的文本值 2007年-05-08 12:35:29.123 + 12:15 作为插入 12:35:29.12300 + 12:15。|  
|字符串括起来**datetimeoffset**格式|yyyy-月-日 hh:mm:ss.fffffff {+ &#124;-} hh: mm<br /><br />示例: 2007年-05-08 12:35:29.1234567 + 12:15|源数据不能超过指定的 datetimeoffset 列中的小数秒数。 如果数据源具有小于或等于的小数部分组成的秒数，则用零右侧填充数据。 例如，如果数据类型是 datetimeoffset (5) 的文本值 2007年-05-08 12:35:29.123 + 12:15 作为插入 12:35:29.12300 + 12:15。|  
  
### <a name="datetime2-data-type"></a>datetime2 数据类型  
下表定义的默认格式和将文字值加载到类型的列的规则**datetime2** (*n*)。 默认格式为 yyyy-月-日 hh:mm:ss.fffffff。 空字符串 （"） 转换为默认值 1900年-01-01 12:00:00。 包含仅空格的字符串 () 生成错误。 小数位数取决于列定义。 例如，定义为一列**datetime2** (2) 将具有两个小数位。  
  
|输入的数据类型|输入的数据示例|转换为 datetime2 数据类型|  
|-------------------|-----------------------|-------------------------------------|  
|字符串括起来**datetime**格式|yyyy MM dd hh: mm: [.fff]<br /><br />示例: 2007年-05-08 12:35:29.123|秒的小数部分是可选的并且插入的值将设置为 0。|  
|字符串括起来**smalldatetime**格式|yyyy MM dd hh: mm<br /><br />示例: 2007年-05-08 12|插入值时，可选的秒数和剩余的小数位数将设置为 0。|  
|字符串括起来**日期**格式|yyyy-月-日<br /><br />示例: 2007年-05-08|插入值时，时间值 （小时、 分钟、 秒和秒的小数部分） 将设置为 0。 例如，文本"2007年-05-08 作为插入 2007年-05-08 12:00:00.0000000。|  
|字符串括起来**datetime2**格式|yyyy-月-日 hh:mm:ss:fffffff<br /><br />示例: 2007年-05-08 12:35:29.1234567|如果数据源包含日期和时间是小于或等于中指定的值的组件**datetime2**(*n*)，则数据将插入; 否则将生成错误。|  
  
### <a name="DateFormats"></a>日期时间格式  
Dwloader 输入数据加载到 SQL Server PDW 支持以下数据格式。 在表后列出了更多详细信息。  
  
|datetime|smalldatetime|date|datetime2|datetimeoffset|  
|------------|-----------------|--------|-------------|------------------|  
|[M [M]]M-[d] d-[yy] yy hh: mm: [.fff]|[M [M]]M-[d] d-[yy] yy hh: mm [: 00]|[M [M]]M-[d] d-[yy] yy|[M [M]]M-[d] d-[yy] yy hh: mm: [.fffffff]|[M [M]]M-[d] d-[yy] yy hh: mm: [.fffffff] zzz|  
|[M [M]]M-[d] d-[yy] yy hh: mm: [.fff] [tt]|[M [M]]M-[d] d-[yy] yy hh: mm [: 00] [tt]||[M [M]]M-[d] d-[yy] yy hh: mm: [.fffffff] [tt]|[M [M]]M-[d] d-[yy] yy hh: mm: [.fffffff] [tt] zzz|  
|[M [M]]M-[yy] yy-[d] d hh: mm: [.fff]|[M [M]]M-[yy] yy-[d] d hh: mm [: 00]|[M [M]]M-[yy] yy-[d] d|[M [M]]M-[yy] yy-[d] d hh: mm: [.fffffff]|[M [M]]M-[yy] yy-[d] d hh: mm: [.fffffff] zzz|  
|[M [M]]M-[yy] yy-[d] d hh: mm: [.fff] [tt]|[M [M]]M-[yy] yy-[d] d hh: mm [: 00] [tt]||[M [M]]M-[yy] yy-[d] d hh: mm: [.fffffff] [tt]|[M [M]]M-[yy] yy-[d] d hh: mm: [.fffffff] [tt] zzz|  
|[yy] yy-[M [M]] M-[d] d hh: mm: [.fff]|[yy] yy-[M [M]] M-[d] d hh: mm [: 00]|[yy] yy-[M [M]] d M-[d]|[yy] yy-[M [M]] M-[d] d hh: mm: [.fffffff]|[yy] yy-[M [M]] M-[d] d hh: mm: [.fffffff] zzz|  
|[yy] yy-[M [M]] M-[d] d hh: mm: [.fff] [tt]|[yy] yy-[M [M]] M-[d] d hh: mm [: 00] [tt]||[yy] yy-[M [M]] M-[d] d hh: mm: [.fffffff] [tt]|[yy] yy-[M [M]] M-[d] d hh: mm: [.fffffff] [tt] zzz|  
|[yy] yy-[d] d-[M [M]] M hh: mm: [.fff]|[yy] yy-[d] d-[M [M]] M hh: mm [: 00]|[yy] yy-d [d]-[M [M]] M|[yy] yy-[d] d-[M [M]] M hh: mm: [.fffffff]|[yy] yy-[d] d-[M [M]] M hh: mm: [.fffffff] zzz|  
|[yy] yy-[d] d-[M [M]] M hh: mm: [.fff] [tt]|[yy] yy-[d] d-[M [M]] M hh: mm [: 00] [tt]||[yy] yy-[d] d-[M [M]] M hh: mm: [.fffffff] [tt]|[yy] yy-[d] d-[M [M]] M hh: mm: [.fffffff] [tt] zzz|  
|[d] d-[M [M]] M-[yy] yy hh: mm: [.fff]|[d] d-[M [M]] M-[yy] yy hh: mm [: 00]|[d] d-[M [M]] M-[yy] yy|[d] d-[M [M]] M-[yy] yy hh: mm: [.fffffff]|[d] d-[M [M]] M-[yy] yy hh: mm: [.fffffff] zzz|  
|[d] d-[M [M]] M-[yy] yy hh: mm: [.fff] [tt]|[d] d-[M [M]] M-[yy] yy hh: mm [: 00] [tt]||[d] d-[M [M]] M-[yy] yy hh: mm: [.fffffff] [tt]|[d] d-[M [M]] M-[yy] yy hh: mm: [.fffffff] [tt] zzz|  
|[d] d-[yy] yy-[M [M]] M hh: mm: [.fff]|[d] d-[yy] yy-[M [M]] M hh: mm [: 00]|[d] d-[yy] yy-[M [M]] M|[d] d-[yy] yy-[M [M]] M hh: mm: [.fffffff]|[d] d-[yy] yy-[M [M]] M hh: mm: [.fffffff] zzz|  
|[d] d-[yy] yy-[M [M]] M hh: mm: [.fff] [tt]|[d] d-[yy] yy-[M [M]] M hh: mm [: 00] [tt]||[d] d-[yy] yy-[M [M]] M hh: mm: [.fffffff] [tt]|[d] d-[yy] yy-[M [M]] M hh: mm: [.fffffff] [tt] zzz|  
  
详细信息：  
  
-   若要分隔月、 日和年的值，可以使用 –'，'/'，或。 '. 为简单起见，表使用仅 – 分隔符。  
  
-   若要指定以文本形式的月份，请使用三个或多个字符。 使用 1 或 2 个字符的月将解释为数字。  
  
-   若要分隔时间值，请使用: 符号。  
  
-   用方括号括起来的字母是可选的。  
  
-   字母 tt 指定 [AM |PM | 是 | pm]。 AM 是默认设置。 当指定 tt 时，(hh) 的小时值必须在 0 到 12 范围内。  
  
-   字母 zzz 指定系统的格式的当前时区的时区偏移量 {+ |-} HH:ss]。  
  
## <a name="InsertNumerictypes"></a>将文本插入到数值类型  
下表定义了用于加载到使用数值类型的 SQL Server PDW 列的文本值的默认格式和转换规则。  
  
### <a name="bit-data-type"></a>bit 数据类型  
下表定义的默认格式和将文字值加载到类型的列的规则**位**。 一个空字符串 （'） 或包含仅空格的字符串 () 转换为 0。  
  
|输入的数据类型|输入的数据示例|转换为 bit 数据类型|  
|-------------------|-----------------------|-------------------------------|  
|字符串括起来**整数**格式|ffffffffff<br /><br />示例: '1' 或者"321"|格式化为字符串文本的整数值不能包含值为负。 例如，值-123 生成错误。<br /><br />大于 1 的值转换为 1。 例如，"123"的值将转换为 1。|  
|字符串文本|'TRUE' 或者 'FALSE'<br /><br />示例: ' true'|值 'TRUE' 转换为 1;FALSE 的值转换为 0。|  
|整数文本|fffffffn<br /><br />示例: 1 或 321|大于 1 或小于 0 的值转换为 1。 例如，值 123 和-将转换为 1。|  
|十进制文本|fffnn.fffn<br /><br />示例： 1234.5678|大于 1 或小于 0 的值转换为 1。 例如，123.45 和-123.45 的值将转换为 1。|  
  
### <a name="decimal-data-type"></a>decimal 数据类型  
下表定义了将文本值加载到类型的列的规则**十进制**(*p、 s*)。 数据转换规则都与 SQL Server 的相同。 有关详细信息，请参阅[数据类型转换 （数据库引擎）](http://go.microsoft.com/fwlink/?LinkId=202128) MSDN 上。  
  
|输入的数据类型|输入的数据示例|  
|-------------------|-----------------------|  
|整数文本|321312313123|  
|十进制文本|123344.34455|  
  
### <a name="float-and-real-data-types"></a>浮点型和实型数据类型  
下表定义了将文本值加载到类型的列的规则**float**或**实际**。 数据转换规则都与 SQL Server 的相同。 有关详细信息，请参阅[数据类型转换 （数据库引擎）](../t-sql/data-types/data-type-conversion-database-engine.md) MSDN 上。  
  
|输入的数据类型|输入的数据示例|  
|-------------------|-----------------------|  
|整数文本|321312313123|  
|十进制文本|123344.34455|  
|浮点型|3.12323E + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int、 bigint、 tinyint、 smallint 数据类型  
下表定义了将文本值加载到类型的列的规则**int**， **bigint**， **tinyint**，或**smallint**。 数据源不能超过给定的数据类型所允许的范围。 例如，对于范围**tinyint**并 0 到 255 的范围**int**为-2,147,483,648 到 2,147,483,647。  
  
|输入的数据类型|输入的数据示例|转换为整数数据类型|  
|-------------------|-----------------------|------------------------------------|  
|整数文本|321312313123||  
|十进制文本|123344.34455|小数点右侧的值将被截断。|  
  
### <a name="money-and-smallmoney-data-types"></a>money 和 smallmoney 数据类型  
Money 文字值表示为带有可选小数点和可选的货币符号作为前缀的数字的字符串。 数据源不能超过给定的数据类型所允许的范围。 例如，对于范围**smallmoney**是-214，748.3648 214，748.3647 和的范围**money**是到 922337203685，477.5807-922337203685，477.5808。 下表定义了将文本值加载到类型的列的规则**money**或**smallmoney**。  
  
|输入的数据类型|输入的数据示例|转换到现金或 smallmoney 数据类型|  
|-------------------|-----------------------|-----------------------------------------------|  
|整数文本|321312|插入值时，即小数点后的缺少数字均设置为 0。 例如，作为 12345.0000 插入文本 12345|  
|十进制文本|123344.34455|如果小数点后的数字个数超过 4，值舍入为最接近的值。 例如，值 123344.34455 可作为 123344.3446 插入。|  
|Money 文本|$123456.7890|货币符号不插入的值。<br /><br />如果小数点后的数字个数超过 4，值舍入为最接近的值。|  
  
## <a name="InsertStringTypes"></a>将文本插入到字符串类型  
下表定义了用于加载到使用字符串类型的 SQL Server PDW 列的文本值的默认格式和转换规则。  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>char、 varchar、 nchar 和 nvarchar 数据类型  
下表定义的默认格式和将文字值加载到类型的列的规则**char**， **varchar**， **nchar**和**nvarchar**. 数据源长度不能超过指定的数据类型的大小。 如果数据源长度小于大小**char**或**nchar**数据类型，数据填充到右侧空格来达到数据类型大小。  
  
|输入的数据类型|输入的数据示例|转换为字符数据类型|  
|---------------|-------------------|----------------------------------|  
|字符串文本|格式: 字符字符串<br /><br />示例: ' abc'| 不适用 |  
|Unicode 字符串文本|格式： N'character 字符串<br /><br />示例： N'abc'| 不适用 |  
|整数文本|格式： ffffffffffn<br /><br />示例： 321312313123| 不适用 |  
|十进制文本|格式： ffffff.fffffff<br /><br />示例： 12344.34455| 不适用 |  
|Money 文本|格式： $ffffff.fffnn<br /><br />示例: $ 123456.99|可选的货币符号不插入的值。 若要插入的货币符号，请为字符串文本插入的值。 这与匹配的加载程序将视为字符串文本的每个文本的格式。<br /><br />不允许使用逗号。<br /><br />如果小数点后的数字个数超过 2，值舍入为最接近的值。 例如，值 123.946789 可作为 123.95 插入。<br /><br />使用 CONVERT 函数来插入 money 文本时，允许仅默认样式 0 （不带逗号和即小数点后的 2 位数）。|  
  
### <a name="general-remarks"></a>一般备注  
**dwloader**执行 SMP SQL Server 执行，但不支持所有隐式转换 SMP SQL Server 支持的相同的隐式转换。  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  
