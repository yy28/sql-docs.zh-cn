---
title: DATEDIFF_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEDIFF_BIG
- DATEDIFF_BIG_TSQL
helpviewer_keywords:
- DATEDIFF_BIG function [SQL Server]
- dates [SQL Server]. functions
- date and time [SQL Server], DATEDIFF_BIG
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 19ac1693-3cfa-400d-bf83-20a9cb46599a
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6c0cfefde5609455f53d2afcb33659cd5c1d99bb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

返回指定的 startdate 和 enddate 之间所跨的指定 datepart 边界的计数（带符号的整数）。
  
有关所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和时间数据类型及函数的概述，请参阅[日期和时间数据类型及函数 (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>参数  
*datepart*  
是指定所跨边界类型的 startdate 和 enddate 的一部分。 下表列出了所有有效的 datepart 参数。 用户定义的变量等效项是无效的。
  
|*datepart*|缩写形式|  
|---|---|
|year|**yy, yyyy**|  
|quarter|**qq, q**|  
|month|**mm, m**|  
|dayofyear|**dy, y**|  
|day|**dd, d**|  
|week|**wk, ww**|  
|hour|**hh**|  
|minute|**mi, n**|  
|second|**ss, s**|  
|millisecond|ms|  
|microsecond|mcs|  
|nanosecond|ns|  
  
*startdate*  
一个表达式，它可以解析为 time、date、smalldatetime、datetime、datetime2 或 datetimeoffset 值。 date 可以是表达式、列表达式、用户定义的变量或字符串文字。 从 enddate 中减去 startdate。  
为避免不确定性，请使用四位数年份。 有关两位数年份的信息，请参阅[配置“two digit year cutoff”（两位数年份截止）服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
enddate  
请参阅 startdate。
  
## <a name="return-type"></a>返回类型  
 已签名   
        **bigint**  
  
## <a name="return-value"></a>返回值  
返回指定的 startdate 和 enddate 之间所跨的指定 datepart 边界的计数（带符号的 bigint）。
-   每个 datepart 及其缩写都返回相同的值。  
  
如果返回值超出 bigint 的范围（-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807），则会返回一个错误。 对于 millisecond，startdate 和 enddate 之间的最大差值为 24 天 20 小时 31 分钟 23.647 秒。 对于 second，最大差值为 68 年。
  
如果为 startdate 和 enddate 都只指定了时间值，并且 datepart 不是时间 datepart，则返回 0。
  
在计算返回值时不使用 startdate 或 endate 的时区偏移量部分。
  
由于 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 仅精确到分钟，因此将 smalldatetime 值用作 startdate 或 enddate 时，返回值中的秒和毫秒将始终设置为 0。
  
如果为某个日期数据类型的变量只指定时间值，则所缺日期部分的值将设置为默认值：1900-01-01。 如果为某个时间或日期数据类型的变量只指定日期值，则所缺时间部分的值将设置为默认值：00:00:00。 如果 startdate 和 enddate 中有一个只含时间部分，另一个只含日期部分，则所缺时间和日期部分将设置为各自的默认值。
  
如果 startdate 和 enddate 属于不同的日期数据类型，并且其中一个的时间部分或秒小数部分精度比另一个高，则另一个的所缺部分将设置为 0。
  
## <a name="datepart-boundaries"></a>datepart 边界
以下语句具有相同的 startdate 和相同的 endate。 这些日期是相邻的，在时间上相差 .0000001 秒。 每个语句中 startdate 与 endate 之间的差跨其 datepart 的一个日历或时间边界。 每个语句都返回 1。 如果本例使用不同的年份且 startdate 和 endate 都在相同的日历周内，则 week 的返回值将为 0。

```sql
SELECT DATEDIFF_BIG(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Remarks  
DATEDIFF_BIG 可用在选择列表、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
DATEPART 将字符串文字作为 datetime2 类型隐式转换。 这就意味着，日期在作为字符串传递时，DATEDIFF_BIG 不会支持 YDM 格式。 必须先将字符串显式转换为 datetime 或 smalldatetime 类型，然后才能使用 YDM 格式。
  
指定 SET DATEFIRST 对 DATEDIFF_BIG 不起作用。 DATEDIFF_BIG 始终使用星期日作为每周的第一天，以确保函数是确定性的。
  
## <a name="examples"></a>示例  
以下示例使用不同类型的表达式作为 startdate 和 enddate 形参的实参。
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>为 startdate 和 enddate 指定列  
下例计算一个表的两列中的日期之间所跨越的日边界数。
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF_BIG(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
有关更多其他示例，请参阅 [DATEDIFF (Transact-SQL)](../../t-sql/functions/datediff-transact-sql.md) 中密切相关的示例。
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF (Transact-SQL)](../../t-sql/functions/datediff-transact-sql.md)
  
  
