---
title: "DATEPART (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 05547f2dd50d7f130438d6a07b6952b8c29ec816
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回一个整数，表示指定*datepart*指定*日期*。
  
有关的所有概述[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和时间数据类型和函数，请参阅[日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>参数  
*datepart*  
是的一部分*日期*（日期或时间值） 为其**整数**将返回。 下表列出所有有效*datepart*自变量。 用户定义的变量等效项是无效的。
  
|*datepart*|缩写形式|  
|---|---|
|**年**|**yy**， **yyyy**|  
|**季度**|**qq**， **q**|  
|**月**|**mm**， **m**|  
|**dayofyear**|**dy**， **y**|  
|**一天**|**dd**， **d**|  
|**周**|**wk**， **ww**|  
|**工作日**|**dw**|  
|**小时**|**hh**|  
|**分钟**|**mi、 n**|  
|**第二个**|**ss**， **s**|  
|**毫秒**|**ms**|  
|**微秒**|**mcs**|  
|**纳秒为**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**isowk**， **isoww**|  
  
*date*  
是可被解析为一个表达式**时间**，**日期**， **smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。 *日期*可以是表达式、 列表达式、 用户定义变量或字符串文本。  
为避免不确定性，请使用四位数年份。 两位数年份的相关信息，请参阅[配置两位数年份截止服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
## <a name="return-type"></a>返回类型  
 **int**  
  
## <a name="return-value"></a>返回值  
每个*datepart*和其缩写返回相同的值。
  
返回的值取决于使用设置的语言环境[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)和[配置默认语言服务器配置选项](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)的登录名。 如果*日期*是一个字符串某些格式的文本，则返回值依赖于通过使用指定的格式[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)。 当日期为日期或时间数据类型的列表达式时，SET DATEFORMAT 不影响返回值。
  
下表列出了所有*datepart*具有相应的自变量返回值为语句`SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')`。 数据类型*日期*自变量是**datetimeoffset(7)**。 **纳秒为***datepart*返回值具有小数位数为 9 (。 123456700)，并且最后两个位置总是 00。
  
|*datepart*|返回值|  
|---|---|
|**年，yyyy yy**|2007|  
|**季度、 qq、 q**|4|  
|**月、 mm、 m**|10|  
|**dayofyear，dy，y**|303|  
|**天、 dd、 d**|30|  
|**每周、 wk、 ww**|45|  
|**工作日 dw**|1|  
|**小时 hh**|12|  
|**分钟、 n**|15|  
|**第二个、 ss、 s**|32|  
|**millisecond、 ms**|123|  
|**微秒 mcs**|123456|  
|**毫微秒 ns**|123456700|  
|**TZoffset tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>一周和工作日日期部分参数
当*datepart*是**周**(**wk**， **ww**) 或**工作日**(**dw**)，返回的值取决于使用设置的值[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)。
  
任何每年的 1 月 1 日定义的起始编号**周***datepart*，例如： DATEPART (**wk**，年 1 月 1 日*xxx*x) = 1，其中*xxxx*为任何年。
  
下表列出的返回值**周**和**工作日***datepart*为"2007年-04-21 为每个 SET DATEFIRST 参数。 1 月 1 日在 2007 年是星期一。 4 月 21 日在 2007 年是星期六。 SET DATEFIRST 7, Sunday 是美国英语的默认值。
  
|SET DATEFIRST<br /><br /> 参数|week<br /><br /> 返回|weekday<br /><br /> 返回|  
|---|---|---|
|1|16|6|  
|2|17|5|  
|3|17|4|  
|4|17|3|  
|5|17|2|  
|6|17|1|  
|7|16|7|  
  
## <a name="year-month-and-day-datepart-arguments"></a>年、月和日日期部分参数  
为 DATEPART 返回的值 (**年**，*日期*)，日期部分 (**月**，*日期*)，和 DATEPART (**天**，*日期*) 方式与函数返回相同[年](../../t-sql/functions/year-transact-sql.md)，[月](../../t-sql/functions/month-transact-sql.md)，和[天](../../t-sql/functions/day-transact-sql.md)，f分别。
  
## <a name="isoweek-datepart"></a>ISO_WEEK datepart  
ISO 8601 包括 ISO 周-日期系统，即周的编号系统。 每周都与该周内星期四所在的年份关联。 例如，2004 年的第一周 (2004W01) 是指从 2003 年 12 月 29 日（星期一）到 2004 年 1 月 4 日（星期日）。 一年中最大的周编号可能是 52 或 53。 此样式的编号通常用于欧洲国家/地区，其他地方很少使用。
  
不同的国家/地区的编号系统可能不符合 ISO 标准。 现在至少可能存在六种编号系统，如下表所示：
  
|一周中的第一天|一年的第一周包含|分配两次的周|使用的国家/地区|  
|---|---|---|---|
|星期日|1 月 1 日，<br /><br /> 第一个星期六，<br /><br /> 其中有 1–7 天属于此年|是|United States|  
|星期一|1 月 1 日，<br /><br /> 第一个星期日，<br /><br /> 其中有 1–7 天属于此年|是|大多数欧洲国家和英国|  
|星期一|4 年 1 月，<br /><br /> 第一个星期四，<br /><br /> 每年的 4-7 天|是|ISO 8601，挪威和瑞典|  
|星期一|7 月<br /><br /> 第一个星期一，<br /><br /> 7 天均属于此年|是||  
|星期三|1 月 1 日，<br /><br /> 第一个星期二，<br /><br /> 其中有 1–7 天属于此年|是||  
|星期六|1 月 1 日，<br /><br /> 第一个星期五，<br /><br /> 其中有 1–7 天属于此年|是||  
  
## <a name="tzoffset"></a>TZoffset  
**TZoffset** (**tz**) 将作为 （签名） 的分钟数。 下面的语句返回了 310 分钟的时区偏移量。
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
TZoffset 值呈现，如下所示：
- 对于 datetimeoffset datetime2，TZoffset 返回的时间偏移量以分钟为单位，datetime2 的偏移量始终为 0 分钟。
- 对于数据类型可以隐式转换为 datetimeoffset 或 datetime2，除了其他日期/时间数据类型，它返回以分钟为单位的时间偏移量。
- 所有其他类型的参数将导致错误。
  
  
## <a name="smalldatetime-date-argument"></a>smalldatetime 日期参数  
当*日期*是[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)，秒返回为 00。
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>日期部分这不是日期自变量中的默认返回  
如果的数据类型*日期*参数没有指定*datepart*，该默认*datepart*仅当为指定文本时，将返回*日期*。
  
例如，默认年-月-日任何**日期**数据类型为 1900年-01-01。 以下语句具有日期部分参数*datepart*的时间参数*日期*，并返回`1900, 1, 1, 1, 2`。
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
如果*日期*被指定为变量或表列和数据类型，变量或列没有指定*datepart*，返回错误 9810。 以下代码示例失败，因为日期一部分年不是有效的**时间**声明变量的数据类型 *@t* 。
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>秒的小数部分
返回的秒的小数形式如下面的语句所示：
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>注释  
DATEPART 可用于选择列表 WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，DATEPART 隐式强制转换为字符串文本**datetime2**类型。 这就意味着，日期在作为字符串传递时，DATEPART 不会支持 YDM 格式。 必须显式强制转换为字符串**datetime**或**smalldatetime**要使用的 YDM 格式类型。
  
## <a name="examples"></a>示例  
下面的示例返回基准年。 基准年对于日期计算非常有用。 在下面的示例中，日期将指定为数字。 请注意，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将 0 解释为 1900 年 1 月 1 日。
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
下面的示例返回日期的日部分`12/20/1974`。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`--------`
  
 `20`  
  
下面的示例返回日期的年份部分`12/20/1974`。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (year,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`--------`
  
 `1974`  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

