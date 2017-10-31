---
title: "datetimeoffset (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- datetimeoffset_TSQL
- datetimeoffset
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetimeoffset
- datetimeoffset data type [SQL Server]
- dates [SQL Server], data types
- data types [SQL Server], date and time
- time zones [SQL Server]
ms.assetid: a0455b71-ca25-476e-a7a8-0770f1860bb7
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a6c143380711d1af39a6c11f311e9ce3caf87c7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="datetimeoffset-transact-sql"></a>datetimeoffset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

用于定义一个与采用 24 小时制并可识别时区的一日内时间相组合的日期。
  
## <a name="datetimeoffset-description"></a>datetimeoffset 说明
  
|属性|值|  
|---|---|
|语法|**datetimeoffset** [(*秒的小数部分精度*)]|  
|用法|声明@MyDatetimeoffset **datetimeoffset(7)**<br /><br /> 创建表 Table1 (Column1 **datetimeoffset(7)** )|  
|默认字符串文字格式（用于下级客户端）|YYYY MM DD hh: mm: [.nnnnnnn] [{+ &#124;-} hh: mm]<br /><br /> 有关详细信息，请参阅"下层客户端向后的兼容性"下一节。|  
|日期范围|0001-01-01 到 31.12.99<br /><br /> 1 年 1 月 1 日到公元年 12 月 31 日到 9999|  
|时间范围|00:00:00 至 23:59:59.9999999 （秒的小数部分不支持在 Informatica）|  
|时区偏移量范围|-14:00 到 14:00 （Informatica 中忽略的时区偏移量）|  
|各元素的范围|YYYY 是表示年份的四位数字，范围为 0001 到 9999。<br /><br /> MM 是表示指定年份中的月份的两位数字，范围为 01 到 12。<br /><br /> DD 是表示指定月份中的某一天的两位数字，范围为 01 到 31（最高值取决于相应月份）。<br /><br /> hh 是表示小时的两位数字，范围为 00 到 23。<br /><br /> mm 是表示分钟的两位数字，范围为 00 到 59。<br /><br /> ss 是表示秒钟的两位数字，范围为 00 到 59。<br /><br /> n* 是 0 到 7 位数字，范围为 0 到 9999999，它表示秒的小数部分。 Informatica 中不支持秒的小数部分。<br /><br /> hh 是两位数，范围为 -14 到 +14。 时区偏移量是在 Informatica 中忽略。<br /><br /> mm 是两位数，范围为 00 到 59。 时区偏移量是在 Informatica 中忽略。|  
|字符长度|26 位置最小值 (YYYY MM DD hh: mm: {+ &#124;-} hh: mm) 到 34 最大 (YYYY-月-日 hh:mm:ss.nnnnnnn {+ &#124;-} hh: mm)|  
|精度、小数位数|请参阅下表。|  
|存储大小|默认值为 10 个字节的固定大小，默认的秒的小数部分精度为 100ns。|  
|精确度|100 纳秒|  
|默认值|1900-01-01 00:00:00 00:00|  
|日历|公历|  
|用户定义的秒的小数部分精度|是|  
|时区偏移量感知和保留|是|  
|夏时制感知|是|  
  
|指定的小数位数|结果 (精度, 小数位数)|列长度（以字节为单位）|秒的小数部分精度|  
|---|---|---|---|
|**datetimeoffset**|(34,7)|10|7|  
|**datetimeoffset(0)**|(26,0)|8|0-2|  
|**datetimeoffset(1)**|(28,1)|8|0-2|  
|**datetimeoffset(2)**|(29,2)|8|0-2|  
|**datetimeoffset(3)**|(30,3)|9|3-4|  
|**datetimeoffset(4)**|(31,4)|9|3-4|  
|**datetimeoffset(5)**|(32,5)|10|5-7|  
|**datetimeoffset(6)**|(33,6)|10|5-7|  
|**datetimeoffset(7)**|(34,7)|10|5-7|  
  
## <a name="supported-string-literal-formats-for-datetimeoffset"></a>支持 datetimeoffset 字符串格式
下表列出了支持的 ISO 8601 字符串文本的格式为**datetimeoffset**。 字母、 数字、 未分隔和时间格式的日期和时间部分的有关信息**datetimeoffset**，请参阅[日期 &#40;Transact SQL &#41;](../../t-sql/data-types/date-transact-sql.md)和[时间 &#40;Transact SQL &#41;](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Description|  
|---|---|
|YYYY-MM-DDThh:mm:ss [.nnnnnnn] [{+ &#124;-} hh: mm]|这两种格式不受 SET LANGUAGE 和 SET DATEFORMAT 会话的区域设置的影响。 之间不允许有空格**datetimeoffset**和**datetime**部分。|  
|YYYY-MM-DDThh:mm:ss[.nnnnnnn]Z (UTC)|此格式由 ISO 定义表明**datetime**应以协调世界时 (UTC) 表示部分。 例如，1999-12-12 12:30:30.12345 -07:00 应表示为 1999-12-12 19:30:30.12345Z。|  
  
## <a name="time-zone-offset"></a>时区偏移量
时区偏移量指定区域相对于 UTC 的偏移量**时间**或**datetime**值。 时区偏移量可以表示为 [+|-] hh:mm：
-   hh 是两位数，范围为 00 到 14，表示时区偏移量中的小时数。  
-   mm 是两位数，范围为 00 到 59，表示时区偏移量中的额外分钟数。  
-   \+（+） 或-（减） 是时区偏移量的必需符号。 这两个符号表示是在 UTC 时间的基础上加上还是从中减去时区偏移量以得出本地时间。 时区偏移量的有效范围为 -14:00 到 +14:00。  
  
时区偏移量的范围遵循 XSD 架构定义的 W3C XML 标准，与 SQL 2003 标准定义（12:59 到 +14:00）略有不同。
  
可选类型参数*秒的小数部分精度*秒的小数部分指定的位数。 该值可以是一个 0 到 7（100 纳秒）的整数。 默认值*秒的小数部分精度*为 100ns （七位数的秒的小数部分）。
  
此数据存储在数据库中，并以与 UTC 相同的方式在服务器中进行处理、比较、排序和索引。 时区偏移量将保留在数据库中以供检索。
  
给定的时区偏移量将被认为在夏令时 (DST) 感知和已调整对于任何给定**datetime** DST 时段中。
  
有关**datetimeoffset**键入，UTC 和本地 （到持久的还是转换后的时区偏移量） **datetime**期间插入、 更新、 算术、 转换或分配操作，将验证值。 任何无效的 UTC 或本地组 （到持久的还是转换后的时区偏移量） 检测**datetime**值将引发无效的值错误。 例如，9999-12-31 10:10:00 在 UTC 中有效，但在本地时间中会溢出时区偏移量 +13:50。
  
若要将日期转换为对应**datetimeoffset**值中的目标时区，请参阅[AT TIME ZONE &#40;Transact SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md).
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 和 ISO 8601 法规遵从性  
ANSI 和 ISO 8601 法规遵从性节[日期](../../t-sql/data-types/date-transact-sql.md)和[时间](../../t-sql/data-types/time-transact-sql.md)主题适用于**datetimeoffset**。
  
## <a name="backward-compatibility-for-down-level-clients"></a>向后兼容性下层客户端
不支持某些下层客户端**时间**，**日期**， **datetime2**和**datetimeoffset**数据类型。 下表显示了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上级实例与下级客户端之间的类型映射。
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型|传递给下级客户端的默认字符串文字格式|下级 ODBC|下级 OLEDB|下级 JDBC|下级 SQLCLIENT|  
|---|---|---|---|---|---|
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
|**datetimeoffset**|YYYY MM DD hh: mm: [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
  
## <a name="converting-date-and-time-data"></a>将日期和时间数据转换
当转换为日期和时间数据类型时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将会拒绝它无法识别为日期或时间的所有值。 CAST 和 CONVERT 函数中使用的日期和时间数据的信息，请参阅[CAST 和 CONVERT &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
将转换为时**日期**，复制年、 月和日。 下面的代码显示将 `datetimeoffset(4)` 值转换为 `date` 值的结果。  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10 +01:00';  
DECLARE @date date= @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @date AS 'date';  
  
--Result  
--@datetimeoffset                date  
-------------------------------- ----------  
--2025-12-10 12:32:10.0000 +01:0 2025-12-10  
--  
--(1 row(s) affected)  
  
```  
  
如果该转换是**time(n)**，则我们，分钟、 秒和秒的小数部分将复制。 时区值被截断。 时的精度**datetimeoffset(n)**值是否大于精度的**time(n)**值，则这向上舍入。 下面的代码显示将 `datetimeoffset(4)` 值转换为 `time(3)` 值的结果。
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @time time(3) = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @time AS 'time';  
  
--Result  
--@datetimeoffset                time  
-------------------------------- ------------  
-- 2025-12-10 12:32:10.1237 +01:00    12:32:10.124  
  
--  
--(1 row(s) affected)  
  
```  
  
将转换为时**datetime**、 日期和时间值将会复制，并且此时区被截断。 时的小数部分精度**datetimeoffset(n)**值是否大于三个数字，则该值被截断。 下面的代码显示将 `datetimeoffset(4)` 值转换为 `datetime` 值的结果。
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @datetime AS 'datetime';  
  
--Result  
--@datetimeoffset                datetime  
-------------------------------- -----------------------  
--2025-12-10 12:32:10.1237 +01:0 2025-12-10 12:32:10.123  
--  
--(1 row(s) affected)  
```  
  
转换到**smalldatetime**，复制的日期和时间。 分钟数会根据秒值向上舍入，秒数设置为 0。 下面的代码显示将 `datetimeoffset(3)` 值转换为 `smalldatetime` 值的结果。  
  
```sql
DECLARE @datetimeoffset datetimeoffset(3) = '1912-10-25 12:24:32 +10:0';  
DECLARE @smalldatetime smalldatetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetimeoffset                @smalldatetime  
-------------------------------- -----------------------  
--1912-10-25 12:24:32.000 +10:00 1912-10-25 12:25:00  
--  
--(1 row(s) affected)  
```  
  
如果该转换是**datetime2(n)**，日期和时间复制到**datetime2**值和时区将被截断。 时的精度**datetime2(n)**值是否大于精度的**datetimeoffset(n)**值，秒的小数部分被截断为适合。 下面的代码显示将 `datetimeoffset(4)` 值转换为 `datetime2(3)` 值的结果。
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1912-10-25 12:24:32.1277 +10:0';  
DECLARE @datetime2 datetime2(3)=@datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @datetime2 AS '@datetime2';  
  
--Result  
@datetimeoffset                    @datetime2  
---------------------------------- ----------------------  
1912-10-25 12:24:32.1277 +10:00    1912-10-25 12:24:32.12  
  
--(1 row(s) affected)  
```  
  
### <a name="converting-datetimeoffset-data-type-to-other-date-and-time-types"></a>转换 datetimeoffset 数据类型设置为其他日期和时间类型
下表描述了所发生的情况时**datetimeoffset**数据类型转换为其他日期和时间数据类型。
  
### <a name="converting-string-literals-to-datetimeoffset"></a>将字符串转换为 datetimeoffset
如果字符串所有部分的格式均有效，则允许从字符串文字转换为日期和时间类型。 否则，将引发运行时错误。 从日期和时间类型向字符串文字进行的未指定样式的隐式转换或显式转换将采用当前会话的默认格式。 下表显示了规则将字符串转换为文本**datetimeoffset**数据类型。
  
|输入字符串文字|**datetimeoffset(n)**|  
|---|---|
|ODBC DATE|ODBC 字符串映射到**datetime**数据类型。 从 ODBC 日期时间文本中插入任何赋值运算**datetimeoffset**类型将导致之间的隐式转换**datetime**和此类型定义的转换规则。|  
|ODBC TIME|请参阅前面的 ODBC DATE 规则。|  
|ODBC DATETIME|请参阅前面的 ODBC DATE 规则。|  
|仅 DATE|TIME 部分默认为 00:00:00。 TIMEZONE 默认为 +00:00。|  
|仅 TIME|DATE 部分默认为 1900-1-1。 TIMEZONE 将默认为 +00:00。|  
|仅 TIMEZONE|提供默认值|  
|DATE + TIME|TIMEZONE 默认为 +00:00。|  
|DATE + TIMEZONE|不允许|  
|TIME + TIMEZONE|DATE 部分默认为 1900-1-1。|  
|DATE + TIME + TIMEZONE|无庸赘述|  
  
## <a name="examples"></a>示例  
下面的示例强制转换到每个字符串的结果进行比较**日期**和**时间**数据类型。
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset'  
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetimeoffset(7)) AS  
        'datetimeoffset IS08601';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|数据类型|“输出”|  
|---|---|
|**Time**|12:35:29. 1234567|  
|**日期**|2007-05-08|  
|**Smalldatetime**|2007-05-08 12:35:00|  
|**日期时间**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**Datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[时区 &AMP; #40;Transact SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  

