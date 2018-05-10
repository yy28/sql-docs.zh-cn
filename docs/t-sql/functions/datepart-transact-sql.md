---
title: DATEPART (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEPART_TSQL
- DATEPART
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], DATEPART
- dateparts [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dateparts [SQL Server], datepart
- comparing dates times [SQL Server]
- DATEPART function [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 15f1a5bc-4c0c-4c48-848d-8ec03473e6c1
caps.latest.revision: 57
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: eee173d268af8e18343c286bda29384b2a327860
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回表示指定 date 的指定 datepart 的整数。
  
有关所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和时间数据类型及函数的概述，请参阅[日期和时间数据类型及函数 (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>参数  
*datepart*  
是将为其返回 integer 的 date（日期或时间值）的一部分。 下表列出了所有有效的 datepart 参数。 用户定义的变量等效项是无效的。
  
|*datepart*|缩写形式|  
|---|---|
|year|yy, yyyy|  
|quarter|qq, q|  
|month|mm, m|  
|dayofyear|dy, y|  
|day|dd, d|  
|week|wk, ww|  
|weekday|**dw**|  
|hour|**hh**|  
|minute|**mi, n**|  
|second|ss, s|  
|millisecond|ms|  
|microsecond|mcs|  
|nanosecond|ns|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**isowk**, **isoww**|  
  
*date*  
一个表达式，它可以解析为 time、date、smalldatetime、datetime、datetime2 或 datetimeoffset 值。 date 可以是表达式、列表达式、用户定义的变量或字符串文字。  
为避免不确定性，请使用四位数年份。 有关两位数年份的信息，请参阅[配置“two digit year cutoff”（两位数年份截止）服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
## <a name="return-type"></a>返回类型  
 **int**  
  
## <a name="return-value"></a>返回值  
每个 datepart 及其缩写都返回相同的值。
  
返回值取决于 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)和登录时选择的[配置默认语言服务器配置选项](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)设定的语言环境。 如果 date 为某些格式的字符串文字，则返回值由使用 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) 指定的格式来确定。 当日期为日期或时间数据类型的列表达式时，SET DATEFORMAT 不影响返回值。
  
下表列出了所有 datepart 参数以及 `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')` 语句返回的相应值。 date 参数的数据类型为 datetimeoffset(7)。 nanosecond datepart 返回值的小数位数为 9 位 (.123456700)，并且最后两位始终为 00。
  
|*datepart*|返回值|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|month, mm, m|10|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|45|  
|**weekday, dw**|@shouldalert|  
|hour, hh|12|  
|minute, n|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>周和工作日日期部分参数
当 datepart 为 week (wk, ww) 或 weekday (dw) 时，返回值取决于使用 [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md) 设置的值。
  
任何年份的 1 月 1 日都用来定义 week datepart 的起始数字，例如：DATEPART (wk, 'Jan 1, xxxx') = 1，其中 xxxx 为任意年份。
  
下表列出了每个 SET DATEFIRST 参数的“2007-04-21”的 week 和 weekday datepart 返回值。 1 月 1 日在 2007 年是星期一。 4 月 21 日在 2007 年是星期六。 SET DATEFIRST 7, Sunday 是美国英语的默认值。
  
|SET DATEFIRST<br /><br /> 参数|week<br /><br /> 返回|weekday<br /><br /> 返回|  
|---|---|---|
|@shouldalert|16|6|  
|2|17|5|  
|3|17|4|  
|4|17|3|  
|5|17|2|  
|6|17|@shouldalert|  
|7|16|7|  
  
## <a name="year-month-and-day-datepart-arguments"></a>年、月和日日期部分参数  
DATEPART (year, date)、DATEPART (month, date) 和 DATEPART (day, date) 的返回值分别与函数 [YEAR](../../t-sql/functions/year-transact-sql.md)、[MONTH](../../t-sql/functions/month-transact-sql.md) 和 [DAY](../../t-sql/functions/day-transact-sql.md) 的返回值相同。
  
## <a name="isoweek-datepart"></a>ISO_WEEK datepart  
ISO 8601 包括 ISO 周-日期系统，即周的编号系统。 每周都与该周内星期四所在的年份关联。 例如，2004 年的第一周 (2004W01) 是指从 2003 年 12 月 29 日（星期一）到 2004 年 1 月 4 日（星期日）。 一年中最大的周编号可能是 52 或 53。 此样式的编号通常用于欧洲国家/地区，其他地方很少使用。
  
不同的国家/地区的编号系统可能不符合 ISO 标准。 现在至少可能存在六种编号系统，如下表所示：
  
|每周的第一天|一年的第一周包含|分配两次的周|使用的国家/地区|  
|---|---|---|---|
|星期日|1 月 1 日，<br /><br /> 第一个星期六，<br /><br /> 其中有 1–7 天属于此年|是|United States|  
|星期一|1 月 1 日，<br /><br /> 第一个星期日，<br /><br /> 其中有 1–7 天属于此年|是|大多数欧洲国家和英国|  
|星期一|1 月 4 日<br /><br /> 第一个星期四，<br /><br /> 其中有 4–7 天属于此年|“否”|ISO 8601，挪威和瑞典|  
|星期一|1 月 7 日<br /><br /> 第一个星期一，<br /><br /> 7 天均属于此年|“否”||  
|星期三|1 月 1 日，<br /><br /> 第一个星期二，<br /><br /> 其中有 1–7 天属于此年|是||  
|星期六|1 月 1 日，<br /><br /> 第一个星期五，<br /><br /> 其中有 1–7 天属于此年|是||  
  
## <a name="tzoffset"></a>TZoffset  
TZoffset (tz) 返回的是分钟数（带有签名）。 下面的语句返回了 310 分钟的时区偏移量。
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
TZoffset 值的呈现方式如下：
- 对于 datetimeoffset 和 datetime2，TZoffset 返回的时间偏移量以分钟为单位，其中 datetime2 的偏移量始终为 0 分钟。
- 对于可以隐式转换为 datetimeoffset 或 datetime2 的数据类型（其他日期/时间数据类型除外），也返回以分钟为单位的时间偏移量。
- 所有其他类型的参数都会导致错误。
  
  
## <a name="smalldatetime-date-argument"></a>smalldatetime 日期参数  
当 date 为 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 时，秒的返回值为 00。
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>对不在 date 参数中的 datepart 返回默认值  
如果 date 参数的数据类型没有指定的 datepart，则仅当为 date 指定了文字值时，才返回该 datepart 的默认值。
  
例如，任意 date 数据类型的默认年-月-日都为 1900-01-01。 下面的语句具有 datepart 的日期部分参数、date 的时间参数，并返回 `1900, 1, 1, 1, 2`。
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
如果将 date 指定为变量或表列，并且该变量或列的数据类型没有指定的 datepart，则返回错误 9810。 下面的代码示例失败，因为日期部分“年”对于为变量 @t 声明的 time 数据类型无效。
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>秒的小数形式
返回的秒的小数形式如下面的语句所示：
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>Remarks  
DATEPART 可用于选择列表 WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，DATEPART 将字符串文字作为 datetime2 类型隐式转换。 这就意味着，日期在作为字符串传递时，DATEPART 不会支持 YDM 格式。 必须先将字符串显式转换为 datetime 或 smalldatetime 类型，然后才能使用 YDM 格式。
  
## <a name="examples"></a>示例  
下面的示例返回基准年。 基准年对于日期计算非常有用。 在下面的示例中，日期将指定为数字。 请注意，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将 0 解释为 1900 年 1 月 1 日。
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
以下示例返回日期 `12/20/1974` 的日期部分。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
20
```  
  
以下示例返回日期 `12/20/1974` 的年份部分。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (year,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
1974
```  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
