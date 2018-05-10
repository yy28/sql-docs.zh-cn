---
title: DATENAME (Transact-SQL) | Microsoft Docs
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
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8cf093318d49fcf6d28777cf4381dead7110bcab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回表示指定 date 的指定 datepart 的字符串
  
有关所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和时间数据类型及函数的概述，请参阅[日期和时间数据类型及函数 (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>参数  
*datepart*  
是返回的 date 的一部分。 下表列出了所有有效的 datepart 参数。 用户定义的变量等效项是无效的。
  
|*datepart*|缩写形式|  
|---|---|
|year|**yy, yyyy**|  
|quarter|**qq, q**|  
|month|**mm, m**|  
|dayofyear|**dy, y**|  
|day|**dd, d**|  
|week|**wk, ww**|  
|weekday|**dw, w**|  
|hour|**hh**|  
|minute|**mi, n**|  
|second|**ss, s**|  
|millisecond|ms|  
|microsecond|mcs|  
|nanosecond|ns|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**ISOWK, ISOWW**|  
  
*date*  
一个表达式，它可以解析为 time、date、smalldatetime、datetime、datetime2 或 datetimeoffset 值。 date 可以是表达式、列表达式、用户定义的变量或字符串文字。  
为避免不确定性，请使用四位数年份。 有关两位数年份的信息，请参阅[配置“two digit year cutoff”（两位数年份截止）服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
## <a name="return-type"></a>返回类型  
**nvarchar**
  
## <a name="return-value"></a>返回值  
  
-   每个 datepart 及其缩写都返回相同的值。  
  
返回值取决于 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)和登录时选择的[配置默认语言服务器配置选项](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)设定的语言环境。 如果 date 是某些格式的字符串文字，则返回值由 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) 而定。 当日期为日期或时间数据类型的列表达式时，SET DATEFORMAT 不影响返回值。
  
当 date 参数具有 date 数据类型参数时，返回值取决于使用 [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md) 指定的设置。
  
## <a name="tzoffset-datepart-argument"></a>TZoffset 日期部分参数  
如果 datepart 参数为 TZoffset (tz)，并且 date 参数没有时区偏移量，则返回 0。
  
## <a name="smalldatetime-date-argument"></a>smalldatetime 日期参数  
当 date 为 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 时，秒的返回值为 00。
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>对不在日期参数中的日期部分返回默认值  
如果 date 参数的数据类型没有指定的 datepart，则仅当为 date 指定了文字值时，才返回该 datepart 的默认值。
  
例如，任意 date 数据类型的默认年-月-日都为 1900-01-01。 下面的语句具有 datepart 的日期部分参数、date 的时间参数，并返回 `1900, January, 1, 1, Monday`。
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
如果将 date 指定为变量或表列，并且该变量或列的数据类型没有指定的 datepart，则返回错误 9810。 下面的代码示例失败，因为日期部分“年”对于为变量 @t 声明的 time 数据类型无效。
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>Remarks  
DATENAME 可用于选择列表 WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，DATENAME 将字符串文字作为 datetime2 类型隐式转换。 这就意味着，日期在作为字符串传递时，DATENAME 不会支持 YDM 格式。 必须先将字符串显式转换为 datetime 或 smalldatetime 类型，然后才能使用 YDM 格式。
  
## <a name="examples"></a>示例  
下面的示例返回指定日期的日期部分。
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|返回值|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|month, mm, m|October|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|星期二|  
|hour, hh|12|  
|minute, n|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

下面的示例返回指定日期的日期部分。
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|返回值|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|month, mm, m|October|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|星期二|  
|hour, hh|12|  
|minute, n|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

