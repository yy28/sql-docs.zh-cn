---
title: "DATENAME (Transact SQL) |Microsoft 文档"
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
- DATENAME_TSQL
- DATENAME
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATENAME function [SQL Server
- functions [SQL Server], time
- functions [SQL Server], date and time
- dateparts [SQL Server], datename
- date and time [SQL Server], DATENAME
- comparing dates times [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 11855b56-c554-495d-aad4-ba446990153b
caps.latest.revision: 59
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d41bbf5a83f0dee8518ece6f074181b8412bad8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回表示指定的字符字符串*datepart*指定*日期*
  
有关的所有概述[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和时间数据类型和函数，请参阅[日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>参数  
*datepart*  
是的一部分*日期*返回。 下表列出所有有效*datepart*自变量。 用户定义的变量等效项是无效的。
  
|*datepart*|缩写形式|  
|---|---|
|**年**|**yy、 yyyy**|  
|**季度**|**qq、 q**|  
|**月**|**mm、 m**|  
|**dayofyear**|**dy、 y**|  
|**一天**|**dd、 d**|  
|**周**|**wk、 ww**|  
|**工作日**|**dw、 w**|  
|**小时**|**hh**|  
|**分钟**|**mi、 n**|  
|**第二个**|**ss、 s**|  
|**毫秒**|**ms**|  
|**微秒**|**mcs**|  
|**纳秒为**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**ISOWK ISOWW**|  
  
*date*  
是可被解析为一个表达式**时间**，**日期**， **smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。 *日期*可以是表达式、 列表达式、 用户定义变量或字符串文本。  
为避免不确定性，请使用四位数年份。 璝惠两位数年份，请参阅[配置两位数年份截止服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
## <a name="return-type"></a>返回类型  
**nvarchar**
  
## <a name="return-value"></a>返回值  
  
-   每个*datepart*和其缩写返回相同的值。  
  
返回的值取决于使用设置的语言环境[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)和[配置默认语言服务器配置选项](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)的登录名。 返回的值位于从属[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)如果*日期*是字符串文本的某些格式。 当日期为日期或时间数据类型的列表达式时，SET DATEFORMAT 不影响返回值。
  
当*日期*参数具有**日期**数据类型参数，返回值依赖于通过使用指定的设置[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)。
  
## <a name="tzoffset-datepart-argument"></a>TZoffset 日期部分参数  
如果*datepart*自变量是**TZoffset** (**tz**) 和*日期*自变量具有未时区偏移量，则返回 0。
  
## <a name="smalldatetime-date-argument"></a>smalldatetime 日期参数  
当*日期*是[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)，秒返回为 00。
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>对不在日期参数中的日期部分返回默认值  
如果的数据类型*日期*参数没有指定*datepart*，该默认*datepart*仅当为指定文本时，将返回*日期*。
  
例如，默认年-月-日任何**日期**数据类型为 1900年-01-01。 以下语句具有日期部分参数*datepart*的时间参数*日期*，并返回`1900, January, 1, 1, Monday`。
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
如果*日期*被指定为变量或表列和数据类型，变量或列没有指定*datepart*，返回错误 9810。 以下代码示例失败，因为日期一部分年不是有效的**时间**声明变量的数据类型 *@t* 。
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>注释  
DATENAME 可用于选择列表 WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，DATENAME 隐式强制转换为字符串文本**datetime2**类型。 这就意味着，日期在作为字符串传递时，DATENAME 不会支持 YDM 格式。 必须显式强制转换为字符串**datetime**或**smalldatetime**要使用的 YDM 格式类型。
  
## <a name="examples"></a>示例  
下面的示例返回指定日期的日期部分。
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|返回值|  
|---|---|
|**年，yyyy yy**|2007|  
|**季度、 qq、 q**|4|  
|**月、 mm、 m**|October|  
|**dayofyear，dy，y**|303|  
|**天、 dd、 d**|30|  
|**每周、 wk、 ww**|44|  
|**工作日 dw**|星期二|  
|**小时 hh**|12|  
|**分钟、 n**|15|  
|**第二个、 ss、 s**|32|  
|**millisecond、 ms**|123|  
|**微秒 mcs**|123456|  
|**毫微秒 ns**|123456700|  
|**TZoffset tz**|310|  
|**ISO_WEEK，ISOWK，ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

下面的示例返回指定日期的日期部分。
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|返回值|  
|---|---|
|**年，yyyy yy**|2007|  
|**季度、 qq、 q**|4|  
|**月、 mm、 m**|October|  
|**dayofyear，dy，y**|303|  
|**天、 dd、 d**|30|  
|**每周、 wk、 ww**|44|  
|**工作日 dw**|星期二|  
|**小时 hh**|12|  
|**分钟、 n**|15|  
|**第二个、 ss、 s**|32|  
|**millisecond、 ms**|123|  
|**微秒 mcs**|123456|  
|**毫微秒 ns**|123456700|  
|**TZoffset tz**|310|  
|**ISO_WEEK，ISOWK，ISOWW**|44|  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


