---
title: "日期 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- date_TSQL
- date
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], date
- date and time [SQL Server], date
- dates [SQL Server], data types
- date data type [SQL Server]
- data types [SQL Server], date and time
ms.assetid: c963e8b4-5a85-4bd0-9d48-3f8da8f6516b
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c5d3a52b6163f375850b22e27baf9a858ef8ed8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="date-transact-sql"></a>date (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

定义 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的日期。
  
## <a name="date-description"></a>日期说明
  
|属性|值|  
|--------------|-----------|  
|语法|**date**|  
|用法|声明 @MyDate **日期**<br /><br /> 创建表 Table1 (Column1**日期**)|  
|默认字符串文本格式<br /><br /> （用于下级客户端）|YYYY-MM-DD<br /><br /> 有关详细信息，请参阅"下层客户端向后的兼容性"下一节。|  
|范围|0001-01-01 通过 9999-12-31 (1582年-10-15 通过 9999-12-31 的 Informatica)<br /><br /> 1 年 1 月 1 日到公元年 12 月 31 日到 9999 （1582 年 10 月 15，CE 年 12 月 31，Informatica 的 9999 CE）|  
|各元素的范围|YYYY 是表示年份的四位数字，范围为从 0001 到 9999。 为 Informatica，YYYY 仅限于 1582年到 9999 范围内。<br /><br /> MM 是表示指定年份中的月份的两位数字，范围为从 01 到 12。<br /><br /> DD 是表示指定月份中的某一天的两位数字，范围为从 01 到 31（最高值取决于具体月份）。|  
|字符长度|10 位|  
|精度、小数位数|10, 0|  
|存储大小|固定 3 个字节|  
|存储结构|1、3 字节整数存储日期。|  
|精确度|一天|  
|默认值|1900-01-01<br /><br /> 此值用于从隐式转换的追加的日期部分**时间**到**datetime2**或**datetimeoffset**。|  
|日历|公历|  
|用户定义的秒的小数部分精度|是|  
|时区偏移量感知和保留|是|  
|夏时制感知|是|  
  
## <a name="supported-string-literal-formats-for-date"></a>支持日期的字符串文本格式
下表显示有效的字符串的文本格式**日期**数据类型。
  
|数字|Description|  
|-------------|-----------------|  
|mdy<br /><br /> [m]m/dd/[yy]yy<br /><br /> [m]m-dd-[yy]yy<br /><br /> [m]m.dd.[yy]yy<br /><br /> myd<br /><br /> mm/[yy]yy/dd<br /><br /> mm-[yy]yy/dd<br /><br /> [m]m.[yy]yy.dd<br /><br /> dmy<br /><br /> dd/[m]m/[yy]yy<br /><br /> dd-[m]m-[yy]yy<br /><br /> dd.[m]m.[yy]yy<br /><br /> dym<br /><br /> dd/[yy]yy/[m]m<br /><br /> dd-[yy]yy-[m]m<br /><br /> dd.[yy]yy.[m]m<br /><br /> ymd<br /><br /> [yy]yy/[m]m/dd<br /><br /> [yy]yy-[m]m-dd<br /><br /> [yy]yy-[m]m-dd|[m]m、dd 和 [yy]yy 在字符串中表示月、日和年，使用斜线 (/)、连字符 (-) 或句点 (.) 作为分隔符。<br /><br /> 仅支持四位或两位数字表示的年份。 请尽可能使用以四位数字表示的年份。 若要指定一个从 0001 到 9999 之间的整数，表示两位数年份解释为四位数年份的截止年份，使用[配置两位数年份截止服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。<br /><br /> **注意！** 为 Informatica，YYYY 仅限于 1582年到 9999 范围内。<br /><br /> 一个比截止年份的后两位数字小或者与其相等的两位数年份与该截止年份处于同一个世纪。 而一个比截止年份的后两位数字大的两位数年份所处的世纪为该截止年份所处世纪的上一个世纪。 例如，如果“两位数年份截止”为默认值 2049，则两位数年份 49 被解释为 2049 年，而两位数年份 50 被解释为 1950 年。<br /><br /> 默认日期格式由当前语言设置决定。 你可以通过更改日期格式[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)和[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)语句。<br /><br /> **Ydm**不支持格式**日期**。|  
  
|字母|Description|  
|------------------|-----------------|  
|mon [dd][,] yyyy<br /><br /> mon dd[,] [yy]yy<br /><br /> mon yyyy [dd]<br /><br /> [dd] mon[,] yyyy<br /><br /> dd mon[,][yy]yy<br /><br /> dd [yy]yy mon<br /><br /> [dd] yyyy mon<br /><br /> yyyy mon [dd]<br /><br /> yyyy [dd] mon|**mon**表示完整的月份名称或中的当前语言给定月份缩写。 逗号是可选的，且忽略大小写。<br /><br /> 为避免不确定性，请使用四位数年份。<br /><br /> 如果没有指定日，则默认为当月第一天。|  
  
|ISO 8601|描述|  
|--------------|----------------|  
|YYYY-MM-DD<br /><br /> YYYYMMDD|与 SQL 标准相同。 这是唯一定义为国际标准的格式。|  
  
|未分隔的|Description|  
|-----------------|-----------------|  
|[yy]yymmdd<br /><br /> yyyy[mm][dd]|**日期**数据可以指定具有 4、 6 或 8 个位数。 六个或八位字符串始终解释为**ymd**。 月和日必须始终是两位数字。 四位字符串被解释为年。|  
  
|ODBC|Description|  
|----------|-----------------|  
|{ d 'yyyy-mm-dd' }|特定于 ODBC API。|  
  
|W3C XML 格式|Description|  
|--------------------|-----------------|  
|yyyy-mm-ddTZD|专为用于 XML/SOAP 而支持的格式。<br /><br /> TZD 是时区指示符（Z 或 +hh:mm 或 -hh:mm）：<br /><br /> -hh: mm 表示时区偏移量。 hh 是两位数，范围为 0 到 14，它表示时区偏移量中的小时数。<br />-MM 是范围从 0 到 59，表示时区偏移量的附加分钟数的两个数字。<br />-+ （加） 或 – （减号） 必需的时区偏移量。 这两个符号表示用协调世界时 (UTC) 加上或减去时区偏移量以得出本地时间。 时区偏移量的有效范围为 -14:00 到 +14:00。|  
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 和 ISO 8601 法规遵从性  
**日期**符合 ANSI SQL 标准定义中为公历日历:"请注意 85-在要存储在日期范围 0001-01-01 CE 通过 9999-12-31 的公历格式中，数据类型将允许日期的 Datetime CE。"
  
默认字符串文字格式（用于下级客户端）将遵照 SQL 标准格式（定义为 YYYY-MM-DD）。 该格式与 ISO 8601 对 DATE 的定义相同。
  
> [!NOTE]  
>  为 Informatica，范围仅限于 1582年-10-15 (1582 年 10 月 15，CE) 到 9999-12-31 (12 月 31 日到 9999 CE)。  
  
## <a name="backward-compatibility-for-down-level-clients"></a>向后兼容性下层客户端
不支持某些下层客户端**时间**，**日期**， **datetime2**和**datetimeoffset**数据类型。 下表显示了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上级实例与下级客户端之间的类型映射。
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型|传递给下级客户端的默认字符串文字格式|下级 ODBC|下级 OLEDB|下级 JDBC|下级 SQLCLIENT|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
|**datetimeoffset**|YYYY MM DD hh: mm: [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
  
## <a name="converting-date-and-time-data"></a>将日期和时间数据转换
当转换为日期和时间数据类型时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将会拒绝它无法识别为日期或时间的所有值。 CAST 和 CONVERT 函数中使用的日期和时间数据的信息，请参阅[CAST 和 CONVERT &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
当该转换是**time(n)**，转换失败，并且将会出现错误消息 206:"操作数类型冲突： 日期是与时间不兼容"。
  
如果该转换是**datetime**、 复制日期和时间组成部分设置为 00:00:00.000。 下面的代码显示将 `date` 值转换为 `datetime` 值的结果。  
  
```sql
DECLARE @date date= '12-10-25';  
DECLARE @datetime datetime= @date;  
  
SELECT @date AS '@date', @datetime AS '@datetime';  
  
--Result  
--@date      @datetime  
------------ -----------------------  
--2025-12-10 2025-12-10 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
在转换到的情况下**smalldatetime**，当**日期**值位于范围内[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)、 复制的日期部分和时间组成部分设置为00:00:00。 当**日期**值的范围超出了**smalldatetime**引发值，错误消息 242:"的转换**日期**数据类型设置为**smalldatetime**超出范围的值; 产生数据类型和**smalldatetime**值设置为 NULL。 下面的代码显示将 `date` 值转换为 `smalldatetime` 值的结果。
  
```sql
DECLARE @date date= '1912-10-25';  
DECLARE @smalldatetime smalldatetime = @date;  
  
SELECT @date AS '@date', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@date      @smalldatetime  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00  
--  
--(1 row(s) affected)  
```  
  
当该转换是**datetimeoffset(n)**、 的日期进行复制，和时间设置为 00:00.0000000 + 00:00。 下面的代码显示将 `date` 值转换为 `datetimeoffset(3)` 值的结果。
  
```sql
DECLARE @date date = '1912-10-25';  
DECLARE @datetimeoffset datetimeoffset(3) = @date;  
  
SELECT @date AS '@date', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@date      @datetimeoffset  
------------ ------------------------------  
--1912-10-25 1912-10-25 00:00:00.000 +00:00  
--  
--(1 row(s) affected)  
```  
  
如果该转换是**datetime2(n)**，复制的日期部分，并且时间组成部分设置为 00:00:00.00 无论 (n) 的值。 下面的代码显示将 `date` 值转换为 `datetime2(3)` 值的结果。
  
```sql
DECLARE @date date = '1912-10-25';  
DECLARE @datetime2 datetime2(3) = @date;  
  
SELECT @date AS '@date', @datetime2 AS '@datetime2(3)';  
  
--Result  
--@date      @datetime2(3)  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00.00  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-date-to-other-date-and-time-types"></a>将日期转换为其他日期和时间类型
本部分介绍所发生的情况时**日期**数据类型转换为其他日期和时间数据类型。
  
当该转换是**time(n)**，转换失败，并且将会出现错误消息 206:"操作数类型冲突： 日期是与时间不兼容"。
  
如果该转换是**datetime**，复制日期。 下面的代码显示将 `date` 值转换为 `datetime` 值的结果。
  
```sql
DECLARE @date date= '12-10-25';  
DECLARE @datetime datetime= @date;  
  
SELECT @date AS '@date', @datetime AS '@datetime';  
  
--Result  
--@date      @datetime  
------------ -----------------------  
--2025-12-10 2025-12-10 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
当该转换是**smalldatetime**、**日期**值位于范围内[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)、 复制的日期部分和时间组成部分设置为00:00:00.000。 当**日期**值的范围超出了**smalldatetime**引发值，错误消息 242:"的日期数据类型转换为 smalldatetime 数据类型导致超出范围值。";与**smalldatetime**值设置为 NULL。 下面的代码显示将 `date` 值转换为 `smalldatetime` 值的结果。
  
```sql
DECLARE @date date= '1912-10-25';  
DECLARE @smalldatetime smalldatetime = @date;  
  
SELECT @date AS '@date', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@date      @smalldatetime  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00  
--  
--(1 row(s) affected)  
```  
  
转换为**datetimeoffset(n)**、 复制日期，并将时间设置为 00:00.0000000 + 00:00。 下面的代码显示将 `date` 值转换为 `datetimeoffset(3)` 值的结果。
  
```sql
DECLARE @date date = '1912-10-25';  
DECLARE @datetimeoffset datetimeoffset(3) = @date;  
  
SELECT @date AS '@date', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@date      @datetimeoffset  
------------ ------------------------------  
--1912-10-25 1912-10-25 00:00:00.000 +00:00  
--  
--(1 row(s) affected)  
```  
  
当该转换是**datetime2(n)**，复制的日期部分，并且时间组成部分设置为 00:00.000000。 下面的代码显示将 `date` 值转换为 `datetime2(3)` 值的结果。
  
```sql
DECLARE @date date = '1912-10-25'  
DECLARE @datetime2 datetime2(3) = @date;  
  
SELECT @date AS '@date', @datetime2 AS '@datetime2(3)';  
  
--Result  
--@date      @datetime2(3)  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-string-literals-to-date"></a>将字符串转换为日期
如果字符串所有部分的格式均有效，则允许从字符串文字转换为日期和时间类型。 否则，将引发运行时错误。 从日期和时间类型向字符串文字进行的未指定样式的隐式转换或显式转换将采用当前会话的默认格式。 下表显示了规则将字符串转换为文本**日期**数据类型。
  
|输入字符串文字|**date**|  
|---|---|
|ODBC DATE|ODBC 字符串映射到**datetime**数据类型。 从 ODBC 日期时间文本中插入任何赋值运算**日期**类型将导致之间的隐式转换**datetime**和此类型定义的转换规则。|  
|ODBC TIME|请参阅前面的 ODBC DATE 规则。|  
|ODBC DATETIME|请参阅前面的 ODBC DATE 规则。|  
|仅 DATE|无庸赘述|  
|仅 TIME|提供默认值。|  
|仅 TIMEZONE|提供默认值。|  
|DATE + TIME|使用输入字符串的 DATE 部分。|  
|DATE + TIMEZONE|不允许。|  
|TIME + TIMEZONE|提供默认值。|  
|DATE + TIME + TIMEZONE|将使用本地 DATETIME 的 DATE 部分。|  
  
## <a name="examples"></a>示例  
下例比较了将一个字符串分别转换为各种 date 和 time 数据类型时所产生的结果。
  
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
|---------------|------------|  
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

