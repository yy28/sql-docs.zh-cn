---
title: "smalldatetime (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- smalldatetime_TSQL
- smalldatetime
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- smalldatetime data type [SQL Server]
- dates [SQL Server], data types
- date and time [SQL Server], smalldatetime
- data types [SQL Server], date and time
ms.assetid: 68b74610-d54c-4c8e-b4b2-7e3747546ee0
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 07012d85a54292fa763a7b291d1b7318b6969ca4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="smalldatetime-transact-sql"></a>smalldatetime (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

定义结合了一天中的时间的日期。 此时间为 24 小时制，秒始终为零 (:00)，并且不带秒小数部分。
  
> [!NOTE]  
>  使用**时间**，**日期**， **datetime2**和**datetimeoffset**对于新的工作的数据类型。 这些类型符合 SQL 标准。 它们更易于移植。 **时间**， **datetime2**和**datetimeoffset**提供更大秒精度。 **datetimeoffset**为全局已部署的应用程序提供的时区支持。  
  
## <a name="smalldatetime-description"></a>smalldatetime 说明
  
|||  
|-|-|  
|语法|**smalldatetime**|  
|用法|声明@MySmalldatetime **smalldatetime**<br /><br /> 创建表 Table1 (Column1 **smalldatetime** )|  
|默认的字符串文字格式<br /><br /> （用于下级客户端）|不适用|  
|日期范围|1900-01-01 到 2079-06-06<br /><br /> 1900 年 1 月 1 日到 2079 年 6 月 6 日|  
|时间范围|00:00:00 到 23:59:59<br /><br /> 2007-05-09 23:59:59 将舍入为<br /><br /> 2007-05-10 00:00:00|  
|各元素的范围|YYYY 是表示年份的四位数字，范围为 1900 到 2079。<br /><br /> MM 是表示指定年份中的月份的两位数字，范围为 01 到 12。<br /><br /> DD 是表示指定月份中的某一天的两位数字，范围为 01 到 31（最高值取决于相应月份）。<br /><br /> hh 是表示小时的两位数字，范围为 00 到 23。<br /><br /> mm 是表示分钟的两位数字，范围为 00 到 59。<br /><br /> ss 是表示秒钟的两位数字，范围为 00 到 59。 小于或等于 29.998 秒的值向下舍入为最接近的分钟数；大于或等于 29.999 秒的值向上舍入为最接近的分钟数。|  
|字符长度|最高 19 位|  
|存储大小|固定 4 个字节。|  
|精确度|一分钟|  
|默认值|1900-01-01 00:00:00|  
|日历|公历<br /><br /> （不包括完整的年份范围。）|  
|用户定义的秒的小数部分精度|是|  
|时区偏移量感知和保留|是|  
|夏时制感知|是|  
  
## <a name="ansi-and-iso-8601-compliance"></a>对 ANSI 和 ISO 8601 的遵从性  
**smalldatetime**不是 ANSI 或 ISO 8601 符合。
  
## <a name="converting-date-and-time-data"></a>将日期和时间数据转换
当转换为日期和时间数据类型时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将会拒绝它无法识别为日期或时间的所有值。 CAST 和 CONVERT 函数中使用的日期和时间数据的信息，请参阅[CAST 和 CONVERT &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
### <a name="converting-smalldatetime-to-other-date-and-time-types"></a>将 smalldatetime 数据类型转换为其他日期和时间类型
本部分介绍所发生的情况时**smalldatetime**数据类型转换为其他日期和时间数据类型。
  
在转换到的情况下**日期**，复制年、 月和日。 下面的代码显示将 `smalldatetime` 值转换为 `date` 值的结果。
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @date date = @smalldatetime  
  
SELECT @smalldatetime AS '@smalldatetime', @date AS 'date';  
  
--Result  
--@smalldatetime          date  
------------------------- ----------  
--1955-12-13 12:43:00     1955-12-13  
--  
--(1 row(s) affected)  
```  
  
当该转换是**time(n)**，复制小时、 分钟和秒。 秒的小数部分设置为 0。 下面的代码显示将 `smalldatetime` 值转换为 `time(4)` 值的结果。
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @time time(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @time AS 'time';  
  
--Result  
--@smalldatetime          time  
------------------------- -------------  
--1955-12-13 12:43:00     12:43:00.0000  
--  
--(1 row(s) affected)  
```  
  
当该转换是**datetime**、 **smalldatetime**值复制到**datetime**值。 秒的小数部分设置为 0。 下面的代码显示将 `smalldatetime` 值转换为 `datetime` 值的结果。
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetime datetime = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetime AS 'datetime';  
  
--Result  
--@smalldatetime          datetime  
------------------------- -----------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.000  
--  
--(1 row(s) affected)  
```  
  
在转换到的情况下**datetimeoffset(n)**、 **smalldatetime**值复制到**datetimeoffset(n)**值。 秒的小数部分设置为 0，时区偏移量设置为 +00:0。 下面的代码显示将 `smalldatetime` 值转换为 `datetimeoffset(4)` 值的结果。
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetimeoffset datetimeoffset(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetimeoffset AS 'datetimeoffset(4)';  
  
--Result  
--@smalldatetime          datetimeoffset(4)  
------------------------- ------------------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.0000 +00:0  
--  
--(1 row(s) affected)  
```  
  
转换为**datetime2(n)**、 **smalldatetime**值复制到**datetime2(n)**值。 秒的小数部分设置为 0。 下面的代码显示将 `smalldatetime` 值转换为 `datetime2(4)` 值的结果。
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetime2 datetime2(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetime2 AS ' datetime2(4)';  
  
--Result  
--@smalldatetime           datetime2(4)  
------------------------- ------------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.0000  
--  
--(1 row(s) affected)  
```  
  
## <a name="examples"></a>示例  
  
### <a name="a-casting-string-literals-with-seconds-to-smalldatetime"></a>A. 将带秒数的字符串文字转换为 smalldatetime  
下例比较了将字符串文字中的秒数转换成 `smalldatetime` 时产生的结果。
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29'     AS smalldatetime)  
    ,CAST('2007-05-08 12:35:30'     AS smalldatetime)  
    ,CAST('2007-05-08 12:59:59.998' AS smalldatetime);  
```  
  
|输入|“输出”|  
|---|---|
|2007-05-08 12:35:29|2007-05-08 12:35:00|  
|2007-05-08 12:35:30|2007-05-08 12:36:00|  
|2007-05-08 12:59:59.998|2007-05-08 13:00:00|  
  
### <a name="b-comparing-date-and-time-data-types"></a>B. 比较日期和时间数据类型  
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
  
  

