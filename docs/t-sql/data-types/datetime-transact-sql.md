---
title: "datetime (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- datetime_TSQL
- datetime
dev_langs: TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetime
- dates [SQL Server], data types
- datetime data type [SQL Server]
- data types [SQL Server], date and time
ms.assetid: 9bd1cc5b-227b-4032-95d6-7581ddcc9924
caps.latest.revision: "64"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4493e165efbc0410d444f34fc41e30cc08e90307
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="datetime-transact-sql"></a>datetime (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

用于定义一个与采用 24 小时制并带有秒小数部分的一日内时间相组合的日期。
  
> [!NOTE]  
>  使用**时间**，**日期**， **datetime2**和**datetimeoffset**对于新的工作的数据类型。 这些类型符合 SQL 标准。 它们更易于移植。 **时间**， **datetime2**和**datetimeoffset**提供更大秒精度。 **datetimeoffset**为全局已部署的应用程序提供的时区支持。  
  
## <a name="datetime-description"></a>datetime 说明  
  
|属性|值|  
|---|---|
|语法|**datetime**|  
|用法|声明@MyDatetime **datetime**<br /><br /> 创建表 Table1 (Column1 **datetime** )|  
|默认的字符串文字格式<br /><br /> （用于下级客户端）|不适用|  
|日期范围|1753 年 1 月 1 日到 9999 年 12 月 31 日|  
|时间范围|00:00:00 至 23:59:59.997|  
|时区偏移量范围|无|  
|各元素的范围|YYYY 是表示年份的四位数字，范围为 1753 到 9999。<br /><br /> MM 是表示指定年份中的月份的两位数字，范围为 01 到 12。<br /><br /> DD 是表示指定月份中的某一天的两位数字，范围为 01 到 31（最高值取决于相应月份）。<br /><br /> hh 是表示小时的两位数字，范围为 00 到 23。<br /><br /> mm 是表示分钟的两位数字，范围为 00 到 59。<br /><br /> ss 是表示秒钟的两位数字，范围为 00 到 59。<br /><br /> n* 为一个 0 到 3 位的数字，范围为 0 到 999，表示秒的小数部分。|  
|字符长度|最低 19 位到最高 23 位|  
|存储大小|8 字节|  
|精确度|舍入到 .000、.003 或 .007 秒三个增量。|  
|默认值|1900-01-01 00:00:00|  
|日历|公历（不包括完整的年份范围。）|  
|用户定义的秒的小数部分精度|是|  
|时区偏移量感知和保留|是|  
|夏时制感知|是|  
  
## <a name="supported-string-literal-formats-for-datetime"></a>datetime 支持的字符串文字格式  
下表列出的受支持的字符串文本格式**datetime**。 ODBC，除外**datetime**字符串文本是用单引号 （'），例如，字符串文字。 如果环境未**us_english**，字符串文本应采用格式 N 字符串文字。
  
|数字|Description|  
|---|---|
|日期格式：<br /><br /> [0]4/15/[19]96 -- (mdy)<br /><br /> [0]4-15-[19]96 -- (mdy)<br /><br /> [0]4.15.[19]96 -- (mdy)<br /><br /> [0]4/[19]96/15 -- (myd)<br /><br /> 15/[0]4/[19]96 -- (dmy)<br /><br /> 15/[19]96/[0]4 -- (dym)<br /><br /> [19]96/15/[0]4 -- (ydm)<br /><br /> [19]96/[0]4/15 -- (ymd)<br /><br /> 时间格式：<br /><br /> 14:30<br /><br /> 14:30[:20:999]<br /><br /> 14:30[:20.9]<br /><br /> 4am<br /><br /> 4 PM|您可以指定日期数据，其中月份也通过数值指定。 例如 5/20/97 表示 1997 年 5 月 20 日。 当使用数值日期格式时，请在使用正斜杠符号 (/)、连字符 (-) 或句点 (.) 作为分隔符的字符串中指定年、月、日。 此字符串必须采用以下格式：<br /><br /> *数字分隔符数字分隔符数字 [时间] [时间]*<br /><br /> <br /><br /> 当语言设置为**us_english**，日期的默认顺序是 mdy。 你可以使用更改的日期顺序[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)语句。<br /><br /> SET DATEFORMAT 的设置决定了如何解释日期值。 如果顺序和设置不匹配，这些值将由于超出范围而不会被解释成日期，或者被错误地解释。 例如，12/10/08 可以解释成六个不同的日期，具体解释为哪一日期取决于 DATEFORMAT 的设置。 四位数字的年份被解释为年。|  
  
|字母|Description|  
|---|---|
|Apr[il] [15][,] 1996<br /><br /> Apr[il] 15[,] [19]96<br /><br /> Apr[il] 1996 [15]<br /><br /> [15] Apr[il][,] 1996<br /><br /> 15 Apr[il][,][19]96<br /><br /> 15 [19]96 apr[il]<br /><br /> [15] 1996 apr[il]<br /><br /> 1996 APR[IL] [15]<br /><br /> 1996 [15] APR[IL]|您可以指定一个日期数据，其中使用完整的月份名称来指定月份。 例如，月份用英语 April 或使用其缩写 Apr 指定；逗号是可选的，且忽略大小写。<br /><br /> 下面是使用字母日期格式的一些准则：<br /><br /> 1） 将括在单引号 （'） 的日期和时间数据。 对于英语以外的其他语言，使用 N'。<br /><br /> 2） 字符括在括号是可选的。<br /><br /> 3） 如果你指定仅年份的最后两位数，值小于的值的最后两位数[配置两位数年份截止服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)配置选项处于同一世纪的截止年份. 大于或等于该选项值的值处于截止年份的上一个世纪。 例如，如果**两位数年份截止**是 2050 （默认值）、 25 被解释为 2025年且 50 解释为 1950 年。 为避免不确定性，请使用四位数年份。<br /><br /> 4） 如果缺少一天，则将提供该月的第一天。<br /><br /> <br /><br /> 当按字母形式指定月份时，SET DATEFORMAT 会话设置不起作用。|  
  
|ISO 8601|Description|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.mmm]<br /><br /> YYYYMMDD[ hh:mm:ss[.mmm]]|示例：<br /><br /> 1) 2004年-05-23T14:25:10<br /><br /> 2) 2004年-05-23T14:25:10.487<br /><br /> <br /><br /> 若要使用 ISO 8601 格式，必须按此格式指定每一个元素。 这还包括**T**，冒号 （:） 和句点 （.） 格式中所示。<br /><br /> 方括号表示秒小数部分是可选的。 时间部分按 24 小时制指定。<br /><br /> T 指示的时间部分的开头**datetime**值。<br /><br /> 使用 ISO 8601 格式的优点是它是一种国际标准，不会产生模糊的指定。 此外，此格式不受 SET DATEFORMAT 或[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)设置。|  
  
|未分隔的|Description|  
|---|---|
|YYYYMMDD hh:mm:ss[.mmm]||  
  
|ODBC|Description|  
|---|---|
|{ ts '1998-05-02 01:23:56.123' }<br /><br /> { d '1990-10-02' }<br /><br /> { t '13:33:41' }|ODBC API 用于定义转义序列以表示日期和时间值，ODBC 称之为时间戳数据。 此 ODBC 时间戳格式也受支持的 OLE DB 语言定义 (DBGUID SQL) [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB 访问接口[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 使用 ADO、OLE DB 和基于 ODBC 的 API 的应用程序可以使用这种 ODBC 时间戳格式来表示日期和时间。<br /><br /> ODBC 时间戳转义序列的格式是: { *literal_type* *constant_value*}:<br /><br /> <br /><br /> - *literal_type*指定转义序列的类型。 时间戳具有三个*literal_type*说明符：<br />1) d = 仅限日期<br />2) t = 仅时间<br />3) ts = 时间戳 （时间 + 日期）<br /><br /> <br /><br /> -*constant_value*是转义序列的值。 *constant_value*必须遵循这些格式为每个*literal_type*。<br />d: yyyy-月-日<br />t: hh: mm: [.fff]<br />ts: yyyy mm dd hh: mm: [.fff]|  
  
## <a name="rounding-of-datetime-fractional-second-precision"></a>datetime 秒的小数部分精度的舍入  
**datetime**值舍入为增量的.000、.003，或.007 秒下, 表中所示。
  
|用户指定的值|系统存储的值|  
|---|---|
|01/01/98 23:59:59.999|1998-01-02 00:00:00.000|  
|01/01/98 23:59:59.995<br /><br /> 01/01/98 23:59:59.996<br /><br /> 01/01/98 23:59:59.997<br /><br /> 01/01/98 23:59:59.998|1998-01-01 23:59:59.997|  
|01/01/98 23:59:59.992<br /><br /> 01/01/98 23:59:59.993<br /><br /> 01/01/98 23:59:59.994|1998-01-01 23:59:59.993|  
|01/01/98 23:59:59.990<br /><br /> 01/01/98 23:59:59.991|1998-01-01 23:59:59.990|  
  
## <a name="ansi-and-iso-8601-compliance"></a>对 ANSI 和 ISO 8601 的遵从性  
**datetime**不是 ANSI 或 ISO 8601 符合。
  
##  <a name="_datetime"></a>转换的日期和时间数据  
当转换为日期和时间数据类型时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将会拒绝它无法识别为日期或时间的所有值。 CAST 和 CONVERT 函数中使用的日期和时间数据的信息，请参阅[CAST 和 CONVERT &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
### <a name="converting-other-date-and-time-types-to-the-datetime-data-type"></a>将其他日期和时间类型转换为 datetime 数据类型 
本部分介绍其他日期和时间数据类型转换为时会发生什么情况**datetime**数据类型。  
  
当转换是来自**日期**，复制年、 月和日。 时间部分设置为 00:00:00.000。 下面的代码显示将 `date` 值转换为 `datetime` 值的结果。  
  
```sql
DECLARE @date date = '12-21-16';  
DECLARE @datetime datetime = @date;  
  
SELECT @datetime AS '@datetime', @date AS '@date';  
  
--Result  
--@datetime               @date  
------------------------- ----------  
--2016-12-21 00:00:00.000 2016-12-21  
```  
  
当转换是来自**time(n)**，复制时间组件，并且日期部分设置为 1900年-01-01。 时的小数部分精度**time(n)**值是否大于三个数字，则该值将被截断以适合。 下面的示例显示了将 `time(4)` 值转换为 `datetime` 值的结果。  
  
```sql
DECLARE @time time(4) = '12:10:05.1237';  
DECLARE @datetime datetime = @time;  
  
SELECT @datetime AS '@datetime', @time AS '@time';  
  
--Result  
--@datetime               @time  
------------------------- -------------  
--1900-01-01 12:10:05.123 12:10:05.1237  
```  
  
当转换是来自**smalldatetime**，复制的小时和分钟数。 秒和秒的小数部分设置为 0。 下面的代码显示将 `smalldatetime` 值转换为 `datetime` 值的结果。  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';  
DECLARE @datetime datetime = @smalldatetime;  
  
SELECT @datetime AS '@datetime', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetime               @smalldatetime  
------------------------- -----------------------  
--2016-12-01 12:32:00.000 2016-12-01 12:32:00  
```  
  
当转换是来自**datetimeoffset(n)**，复制的日期和时间的组件。 时区被截断。 时的小数部分精度**datetimeoffset(n)**值是否大于三个数字，则该值将被截断。 下面的示例显示了将 `datetimeoffset(4)` 值转换为 `datetime` 值的结果。  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1968-10-23 12:45:37.1234 +10:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetime AS '@datetime', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@datetime               @datetimeoffset  
------------------------- ------------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237 +01:0   
```  
  
当转换是来自**datetime2(n)**，复制的日期和时间。 时的小数部分精度**datetime2(n)**值是否大于三个数字，则该值将被截断。 下面的示例显示了将 `datetime2(4)` 值转换为 `datetime` 值的结果。  
  
```sql
DECLARE @datetime2 datetime2(4) = '1968-10-23 12:45:37.1237';  
DECLARE @datetime datetime = @datetime2;  
  
SELECT @datetime AS '@datetime', @datetime2 AS '@datetime2';  
  
--Result  
--@datetime               @datetime2  
------------------------- ------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237  
```  
  
## <a name="examples"></a>示例  
下面的示例强制转换到每个字符串的结果进行比较**日期**和**时间**数据类型。
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|数据类型|“输出”|  
|---|---|
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
