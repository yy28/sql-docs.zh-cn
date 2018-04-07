---
title: 使用插入加载数据
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Tsql INSERT 语句可用于将数据加载到 SQL Server 并行数据仓库 (PDW) 分布式或复制表的。
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 6e951b0e-e95b-4fd1-b5f3-c65607aee0d8
caps.latest.revision: 21
ms.openlocfilehash: d11799aabdf3f0695a1a8e33add730886a4bcbbe
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="load-data-with-insert"></a>使用插入加载数据

Tsql INSERT 语句可用于将数据加载到 SQL Server 并行数据仓库 (PDW) 分布式或复制表的。 有关插入的详细信息，请参阅[插入](../t-sql/statements/insert-transact-sql.md)。 对于复制的表和分布式表中的所有非分布列，PDW 使用 SQL Server 隐式转换为目标列的数据类型的语句中指定的数据值。 有关 SQL Server 数据转换规则的详细信息，请参阅[数据类型转换为 SQL](http://msdn.microsoft.com/library/ms191530&#40;v=sql11&#40;.aspx)。 但是，对于分发列，PDW 支持 SQL Server 支持的隐式转换的一个子集。 因此，当使用 INSERT 语句将数据加载到分布列时，必须在下表中定义的格式之一指定源数据。  
  
  
## <a name="InsertingLiteralsBinary"></a>将文本插入到二进制类型  
下表定义接受文本的类型、 格式和的文本值插入分布列的类型的转换规则**二进制**(*n*) 或**varbinary**(*n*)。  
  
|文本类型|格式|转换规则|  
|----------------|----------|--------------------|  
|二进制文本|0x*hexidecimal_string*<br /><br />示例： 0x12Ef|必须以 0x 前缀二进制文本。<br /><br />数据源长度不能超过为数据类型指定的字节数。<br /><br />如果数据源长度小于大小**二进制**数据类型，数据填充到用零权访问的数据类型大小。|  
  
## <a name="InsertingLiteralsDateTime"></a>将文本插入日期和时间类型  
由在特定的格式，括在单引号中使用字符值表示日期和时间的文本。 下表定义了允许的文本类型、 格式和类型的 SQL Server PDW 分发列中插入日期或时间文字的转换规则**datetime**， **smalldatetime**，**日期**，**时间**， **datetimeoffset**，或**datetime2**。  
  
### <a name="datetime-data-type"></a>datetime 数据类型  
下表定义的接受的格式和文本值插入分布列的类型的规则**datetime**。 任何空字符串 （"） 转换为默认值 1900年-01-01 12:00:00.000。 包含仅空格的字符串 () 生成错误。  
  
|文本类型|格式|转换规则|  
|----------------|----------|--------------------|  
|字符串括起来**datetime**格式|'YYYY-MM-DD hh:mm:ss[.nnn]'<br /><br />示例: 2007年-05-08 12:35:29.123|插入值时，缺少小数位数均设置为 0。 例如，文本 2007年-05-08 12:35 作为插入 2007年-05-08 12:35:00.000。|  
|字符串括起来**smalldatetime**格式|YYYY MM DD hh: mm<br /><br />示例: 2007年-05-08 12:35|秒数和剩余的小数位数设置为 0 时插入的值。|  
|字符串括起来**日期**格式|'YYYY-MM-DD'<br /><br />示例: 2007年-05-08|时间值 （小时、 分钟、 秒和秒的小数部分） 设置为 12:00:00.000 时插入的值。|  
|字符串括起来**datetime2**格式|'YYYY-MM-DD hh:mm:ss.nnnnnnn'<br /><br />示例: 2007年-05-08 12:35:29.1234567|源数据不能超过三个小数位。 例如，文本 2007年-05-08 12:35:29.123 将插入，但该值 ' 2007年-05-08 12:35:29.1234567 会生成错误。|  
  
### <a name="smalldatetime-data-type"></a>smalldatetime 数据类型  
下表定义的接受的格式和文本值插入分布列的类型的规则**smalldatetime**。 任何空字符串 （"） 转换为默认值 1900年-01-01 12:00。 包含仅空格的字符串 () 生成错误。  
  
|文本类型|格式|转换规则|  
|----------------|----------|--------------------|  
|字符串括起来**smalldatetime**格式|YYYY MM DD hh: mm 或者 YYYY-月-日 hh:mm:00<br /><br />示例: 2007年-05-08 12:00 或 2007年-05-08 12:00:00|源数据必须为年、 月、 日期、 小时和分钟的值。 秒是可选的并且如果存在，必须设置为 00 的值。 任何其他值将生成错误。|  
|字符串括起来**日期**格式|'YYYY-MM-DD'<br /><br />示例: 2007年-05-08|插入值时，时间值 （小时、 分钟、 秒和秒的小数部分） 将设置为 0。|  
  
### <a name="date-data-type"></a>日期数据类型  
下表定义的接受的格式和文本值插入分布列的类型的规则**日期**。 任何空字符串 （"） 转换为默认值 1900年-01-01。 包含仅空格的字符串 () 生成错误。  
  
|文本类型|格式|转换规则|  
|----------------|----------|--------------------|  
|字符串括起来**日期**格式|'YYYY-MM-DD'<br /><br />示例: 2007年-05-08|这是唯一接受的格式。|  
  
### <a name="time-data-type"></a>时间数据类型  
下表定义的接受的格式和文本值插入分布列的类型的规则**时间**。 任何空字符串 （"） 转换为默认值"00:00:00.0000"。 包含仅空格的字符串 () 生成错误。  
  
|文本类型|格式|转换规则|  
|----------------|----------|--------------------|  
|字符串括起来**时间**格式|'hh:mm:ss.nnnnnnn'<br /><br />示例:"12:35:29.1234567"|如果数据源都具有一个小于或等于精度 （数字的小数位数） 比的精度**时间**数据类型，数据填充到零右侧。 例如，文本值"12:35:29.123"可作为"12:35:29.1230000"插入。<br /><br />具有更大的精度，比目标数据类型的值将被拒绝。|  
  
### <a name="datetimeoffset-data-type"></a>datetimeoffset 数据类型  
下表定义的接受的格式和文本值插入分布列的类型的规则**datetimeoffset** (*n*)。 默认格式是 ' YYYY-月-日 hh:mm:ss.nnnnnnn {+ |-} hh: mm。 空字符串 （"） 转换为默认值 1900年-01-01 12:00:00.0000000 + 00:00。 包含仅空格的字符串 () 生成错误。 小数位数取决于列定义。 例如，定义为一列**datetimeoffset** (2) 将具有两个小数位。  
  
|文本类型|格式|转换规则|  
|----------------|----------|--------------------|  
|字符串括起来**datetime**格式|'YYYY-MM-DD hh:mm:ss[.nnn]'<br /><br />示例: 2007年-05-08 12:35:29.123|插入值时，缺少小数位数和偏移量的值将设置为 0。 例如，文本 2007年-05-08 12:35:29.123 作为插入 2007年-05-08 12:35:29.1230000 + 00:00。|  
|字符串括起来**smalldatetime**格式|YYYY MM DD hh: mm<br /><br />示例: 2007年-05-08 12:35|插入值时，秒、 剩余的小数位数和偏移量的值将设置为 0。|  
|字符串括起来**日期**格式|'YYYY-MM-DD'<br /><br />示例: 2007年-05-08|插入值时，时间值 （小时、 分钟、 秒和秒的小数部分） 将设置为 0。 例如，文本"2007年-05-08 作为插入 2007年-05-08 00:00:00.0000000 + 00:00。|  
|字符串括起来**datetime2**格式|'YYYY-MM-DD hh:mm:ss.nnnnnnn'<br /><br />示例: 2007年-05-08 12:35:29.1234567|源数据不能超过指定的 datetimeoffset 列中的小数秒数。 如果数据源具有小于或等于的小数部分组成的秒数，则用零右侧填充数据。 例如，如果数据类型是 datetimeoffset (5) 的文本值 2007年-05-08 12:35:29.123 + 12:15 作为插入 12:35:29.12300 + 12:15。|  
|字符串括起来**datetimeoffset**格式|YYYY-月-日 hh:mm:ss.nnnnnnn {+&#124;-} hh: mm<br /><br />示例: 2007年-05-08 12:35:29.1234567 + 12:15|源数据不能超过指定的 datetimeoffset 列中的小数秒数。 如果数据源具有小于或等于的小数部分组成的秒数，则用零右侧填充数据。 例如，如果数据类型是 datetimeoffset (5) 的文本值 2007年-05-08 12:35:29.123 + 12:15 作为插入 12:35:29.12300 + 12:15。|  
  
### <a name="datetime2-data-type"></a>datetime2 数据类型  
下表定义的接受的格式和文本值插入分布列的类型的规则**datetime2** (*n*)。 默认格式为 YYYY-月-日 hh:mm:ss.nnnnnnn。 空字符串 （"） 转换为默认值 1900年-01-01 12:00:00。 包含仅空格的字符串 () 生成错误。 小数位数取决于列定义。 例如，定义为一列**datetime2** (2) 将具有两个小数位。  
  
|文本类型|格式|转换规则|  
|----------------|----------|--------------------|  
|字符串括起来**datetime**格式|'YYYY-MM-DD hh:mm:ss[.nnn]'<br /><br />示例: 2007年-05-08 12:35:29.123|秒的小数部分是可选的并且插入的值将设置为 0。<br /><br />具有小数部分位数多于目标数据类型的值将被拒绝。|  
|字符串括起来**smalldatetime**格式|YYYY MM DD hh: mm<br /><br />示例: 2007年-05-08 12|插入值时，可选的秒数和剩余的小数位数将设置为 0。|  
|字符串括起来**日期**格式|'YYYY-MM-DD'<br /><br />示例: 2007年-05-08|插入值时，时间值 （小时、 分钟、 秒和秒的小数部分） 将设置为 0。 例如，文本"2007年-05-08 作为插入 2007年-05-08 12:00:00.0000000。|  
|字符串括起来**datetime2**格式|'YYYY-MM-DD hh:mm:ss:nnnnnnn'<br /><br />示例: 2007年-05-08 12:35:29.1234567|如果数据源包含日期和时间是小于或等于中指定的值的组件**datetime2**(*n*)，则数据将插入; 否则将生成错误。|  
  
## <a name="InsertLiteralsNumeric"></a>将文本插入到数值类型  
下表定义的接受的格式和将一个文本值插入到 SQL Server PDW 分布列使用数值类型的转换规则。  
  
### <a name="bit-data-type"></a>bit 数据类型  
下表定义的接受的格式和文本值插入分布列的类型的规则**位**。 一个空字符串 （'） 或包含仅空格的字符串 () 转换为 0。  
  
|文本类型|format|转换规则|  
|----------------|----------|--------------------|  
|字符串括起来**整数**格式|'nnnnnnnnnn'<br /><br />示例: '1' 或者"321"|格式化为字符串文本的整数值不能包含值为负。 例如，值-123 生成错误。<br /><br />大于 1 的值转换为 1。 例如，"123"的值将转换为 1。|  
|字符串文本|'TRUE' 或者 'FALSE'<br /><br />示例: ' true'|值 'TRUE' 转换为 1;FALSE 的值转换为 0。|  
|整数文本|nnnnnnnn<br /><br />示例: 1 或 321|大于 1 或小于 0 的值转换为 1。 例如，值 123 和-将转换为 1。|  
|十进制文本|nnnnn.nnnn<br /><br />示例： 1234.5678|大于 1 或小于 0 的值转换为 1。 例如，123.45 和-123.45 的值将转换为 1。|  
  
### <a name="decimal-data-type"></a>decimal 数据类型  
下表定义的接受的格式和文本值插入分布列的类型的规则**十进制**(*p、 s*)。 数据转换规则都与 SQL Server 的相同。 有关详细信息，请参阅[数据类型转换](http://msdn.microsoft.com/library/ms191530&#40;v=sql11&#40;.aspx)MSDN 上。  
  
|文本类型|格式|  
|----------------|----------|  
|字符串括起来**整数**格式|'nnnnnnnnnnnn'<br /><br />示例:"321312313123"|  
|字符串括起来**十进制**格式|'nnnnnn.nnnnn'<br /><br />示例:"123344.34455"|  
|整数文本|nnnnnnnnnnnn<br /><br />示例： 321312313123|  
|十进制文本|nnnnnn.nnnnn<br /><br />示例:"123344.34455"|  
  
### <a name="float-and-real-data-types"></a>浮点型和实型数据类型  
下表定义的接受的格式和文本值插入分布列的类型的规则**float**或**实际**。 数据转换规则都与 SQL Server 的相同。 有关详细信息，请参阅[数据类型转换](http://msdn.microsoft.com/library/ms191530&#40;v=sql11&#40;.aspx)MSDN 上。  
  
|文本类型|格式|  
|----------------|----------|  
|字符串括起来**整数**格式|'nnnnnnnnnnnn'<br /><br />示例:"321312313123"|  
|字符串括起来**十进制**格式|'nnnnnn.nnnnn'<br /><br />示例:"123344.34455"|  
|字符串括起来**浮点数**格式|'n.nnnnnE+nn'<br /><br />示例: 3.12323E + 14|  
|整数文本|nnnnnnnnnnnn<br /><br />示例： 321312313123|  
|十进制文本|nnnnnn.nnnnn<br /><br />示例： 123344.34455|  
|浮点型|n.nnnnnE+nn<br /><br />示例： 3.12323E + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int、 bigint、 tinyint、 smallint 数据类型  
下表定义的接受的格式和文本值插入分布列的类型的规则**int**， **bigint**， **tinyint**，或**smallint**。 数据源不能超过给定的数据类型所允许的范围。 例如，对于范围**tinyint**并 0 到 255 的范围**int**为-2,147,483,648 到 2,147,483,647。  
  
|文本类型|格式|转换规则|  
|------------|------|----------------|
|字符串括起来**整数**格式|'nnnnnnnnnnnnnn'<br /><br />示例:"321312313123"| InclusionThresholdSetting |  
|整数文本|nnnnnnnnnnnnnn<br /><br />示例： 321312313123| InclusionThresholdSetting|  
|十进制文本|nnnnnn.nnnnn<br /><br />示例： 123344.34455|小数点右侧的值将被截断。|  
  
### <a name="money-and-smallmoney-data-types"></a>money 和 smallmoney 数据类型  
Money 文字值表示为带有可选小数点和作为前缀的货币符号的数字。 数据源不能超过给定的数据类型所允许的范围。 例如，对于范围**smallmoney**是-214，748.3648 214，748.3647 和的范围**money**是到 922337203685，477.5807-922337203685，477.5808。 下表定义的接受的格式和文本值插入分布列的类型的规则**money**或**smallmoney**。  
  
|文本类型|格式|转换规则|  
|----------------|----------|--------------------|  
|字符串括起来**整数**格式|'nnnnnnnn'<br /><br />示例:"123433"|插入值时，即小数点后的缺少数字均设置为 0。 例如，作为 12345.0000 插入文本"12345"。|  
|字符串括起来**十进制**格式|'nnnnnn.nnnnn'<br /><br />示例:"123344.34455"|如果小数点后的数字个数超过 4，值舍入为最接近的值。 例如，"123344.34455"的值可作为 123344.3446 插入。|  
|字符串括起来**money**格式|'$nnnnnn.nnnn'<br /><br />示例:"$ 123456.7890"|可选的货币符号不插入的值。<br /><br />如果小数点后的数字个数超过 4，值舍入为最接近的值。|  
|整数文本|nnnnnnnn<br /><br />示例： 123433|插入值时，即小数点后的缺少数字均设置为 0。 例如，文本 12345 可作为 12345.0000 插入。|  
|十进制文本|nnnnnn.nnnnn<br /><br />示例： 123344.34455|如果小数点后的数字个数超过 4，值舍入为最接近的值。 例如，值 123344.34455 可作为 123344.3446 插入。|  
|Money 文本|$nnnnnn.nnnn<br /><br />示例: $ 123456.7890|可选的货币符号不插入的值。<br /><br />如果小数点后的数字个数超过 4，值舍入为最接近的值。|  
  
## <a name="InsertLiteralsString"></a>将文本插入到字符串类型  
下表定义的接受的格式和将一个文本值插入到某个 SQL Server PDW 列的字符串类型的转换规则。  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>char、 varchar、 nchar 和 nvarchar 数据类型  
下表定义的接受的格式和文本值插入分布列的类型的规则**char**， **varchar**， **nchar**和**nvarchar**。 数据源长度不能超过指定的数据类型的大小。 如果数据源长度小于大小**char**或**nchar**数据类型，数据填充到右侧空格来达到数据类型大小。  
  
|文本类型|格式|转换规则|  
|----------------|----------|--------------------|  
|字符串文本|格式: 字符字符串<br /><br />示例: ' abc'| InclusionThresholdSetting|  
|Unicode 字符串文本|格式： N'character 字符串<br /><br />示例： N'abc'|  InclusionThresholdSetting |  
|整数文本|格式： nnnnnnnnnnn<br /><br />示例： 321312313123| InclusionThresholdSetting |  
|十进制文本|格式： nnnnnn.nnnnnnn<br /><br />示例： 12344.34455| InclusionThresholdSetting |  
|Money 文本|格式： $nnnnnn.nnnnn<br /><br />示例: $ 123456.99|货币符号不插入的值。 若要插入的货币符号，请为字符串文本插入的值。 这与匹配的格式**dwloader**工具，将每个文本视为字符串文字。<br /><br />不允许使用逗号。<br /><br />如果小数点后的数字个数超过 2，值舍入为最接近的值。 例如，值 123.946789 可作为 123.95 插入。<br /><br />使用 CONVERT 函数来插入 money 文本时，允许仅默认样式 0 （不带逗号和即小数点后的 2 位数）。|  

  
## <a name="see-also"></a>另请参阅  
 
[分布式的数据](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-distributed-data/)  
[Insert](../t-sql/statements/insert-transact-sql.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Metadata query examples](metadata-query-examples.md) 
-->
