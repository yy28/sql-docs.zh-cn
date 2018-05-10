---
title: DATEADD (Transact-SQL) | Microsoft Docs
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
- DATEADD
- DATEADD_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- add interval to date or time [SQL Server]
- subtract interval from date or time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], intervals
- date and time [SQL Server], DATEADD
- DATEADD function [SQL Server]
ms.assetid: 89c5ae32-89c6-47e1-979e-15d97908b9f1
caps.latest.revision: 71
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8dcbc7ccfc8c94c28f3c8ba0df32b915440d76e4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="dateadd-transact-sql"></a>DATEADD (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回指定的 date，同时有指定数目的间隔（带符号整数）被添加到该 date 的指定 datepart（日期部分）。
  
有关所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和时间数据类型及函数的概述，请参阅[日期和时间数据类型及函数 (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATEADD (datepart , number , date )  
```  
  
## <a name="arguments"></a>参数  
*datepart*  
是要添加整数的 date 的一部分。 下表列出了所有有效的 datepart 参数。 用户定义的变量等效项是无效的。
  
|*datepart*|缩写形式|  
|---|---|
|year|yy, yyyy|  
|quarter|qq, q|  
|month|mm, m|  
|dayofyear|dy, y|  
|day|dd, d|  
|week|wk, ww|  
|weekday|dw, w|  
|hour|**hh**|  
|minute|mi, n|  
|second|ss, s|  
|millisecond|ms|  
|microsecond|mcs|  
|nanosecond|ns|  
  
*number*  
一个表达式，它可以解析为与 date 的 datepart 相加的 [int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)。 用户定义的变量是有效的。  
如果您指定一个带小数的值，则将小数截去且不进行舍入。
  
*date*  
一个表达式，它可以解析为 time、date、smalldatetime、datetime、datetime2 或 datetimeoffset 值。 date 可以是表达式、列表达式、用户定义的变量或字符串文字。 如果表达式是字符串文字，则它必须解析为一个 datetime 值。 为避免不确定性，请使用四位数年份。 有关两位数年份的信息，请参阅[配置“two digit year cutoff”（两位数年份截止）服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
## <a name="return-types"></a>返回类型
返回数据类型为 date 参数的数据类型，字符串文字除外。
字符串文字的返回数据类型为 datetime。 如果字符串文字的秒数小数位数超过三位 (.nnn) 或包含时区偏移量部分，将引发错误。
  
## <a name="return-value"></a>返回值  
  
## <a name="datepart-argument"></a>datepart 参数  
dayofyear、day 和 weekday 返回相同的值。
  
每个 datepart 及其缩写都返回相同的值。
  
如果 datepart 为 month 且 date 月份比返回月份的天数多，因而 date 中的日在返回月份中不存在，则返回返回月份的最后一天。 例如，9 月份有 30 天；因此，下面两个语句返回 2006-09-30 00:00:00.000：
  
```sql
SELECT DATEADD(month, 1, '20060830');
SELECT DATEADD(month, 1, '20060831');
```
  
## <a name="number-argument"></a>number 参数  
number 参数不能超出 int 的范围。在以下语句中，number 的参数超出 int 的范围（超出 1）。 返回以下错误消息："`Msg 8115, Level 16, State 2, Line 1. Arithmetic overflow error converting expression to data type int."`
  
```sql
SELECT DATEADD(year,2147483648, '20060731');  
SELECT DATEADD(year,-2147483649, '20060731');  
```  
  
## <a name="date-argument"></a>date 参数  
date 参数不能增加至其数据范围之外的值。 在以下语句中，添加到 date 值的 number 值超出了 date 数据类型的范围。 返回以下错误消息："`Msg 517, Level 16, State 1, Line 1 Adding a value to a 'datetime' column caused overflow`."
  
```sql
SELECT DATEADD(year,2147483647, '20060731');  
SELECT DATEADD(year,-2147483647, '20060731');  
```  
  
## <a name="return-values-for-a-smalldatetime-date-and-a-second-or-fractional-seconds-datepart"></a>date 为 smalldatetime 型、datepart 为秒或秒小数部分时的返回值  
[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 值的秒数部分始终为 00。 如果 date 为 smalldatetime，则适用以下原则：
-   如果 datepart 为 second，且 number 在 -30 和 +29 之间，则不执行其他的添加操作。  
-   如果 datepart 为 second，且 number 小于 -30 或大于 +29，则从一分钟开始添加。  
-   如果 datepart 为 millisecond，且 number 在 -30001 和 +29998 之间，则不执行其他的添加操作。  
-   如果 datepart 为 millisecond，且 number 小于 -30001 或大于 +29998，则从一分钟开始添加。  
  
## <a name="remarks"></a>Remarks  
DATEADD 可用在 SELECT \<list>、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
## <a name="fractional-seconds-precision"></a>秒的小数部分精度
对于 date 数据类型 smalldatetime、date 和 datetime，不允许执行 microsecond 或 nanosecond 的 datepart 添加操作。
  
毫秒的小数位数为 3 (.123)；微秒的小数位数为 6 (.123456)；纳秒的小数位数为 9 (.123456789)。 time、datetime2 和 datetimeoffset 数据类型的最大小数位数为 7 (.1234567)。 如果 datepart 为 nanosecond，则在 date 的秒数的小数部分增加前 number 必须为 100。 介于 1 和 49 之间的 number 向下舍入为 0，介于 50 和 99 之间的 number 向上舍入为 100。
  
以下语句添加 millisecond、microsecond 或 nanosecond 的 datepart。
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT '1 millisecond', DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT '2 milliseconds', DATEADD(millisecond,2,@datetime2)  
UNION ALL  
SELECT '1 microsecond', DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT '2 microseconds', DATEADD(microsecond,2,@datetime2)  
UNION ALL  
SELECT '49 nanoseconds', DATEADD(nanosecond,49,@datetime2)  
UNION ALL  
SELECT '50 nanoseconds', DATEADD(nanosecond,50,@datetime2)  
UNION ALL  
SELECT '150 nanoseconds', DATEADD(nanosecond,150,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1 millisecond     2007-01-01 13:10:10.1121111  
2 milliseconds    2007-01-01 13:10:10.1131111  
1 microsecond     2007-01-01 13:10:10.1111121  
2 microseconds    2007-01-01 13:10:10.1111131  
49 nanoseconds    2007-01-01 13:10:10.1111111  
50 nanoseconds    2007-01-01 13:10:10.1111112  
150 nanoseconds   2007-01-01 13:10:10.1111113  
```  
  
## <a name="time-zone-offset"></a>时区偏移量
不允许对时区偏移量执行加法。
  
## <a name="examples"></a>示例  

### <a name="a-incrementing-datepart-by-an-interval-of-1"></a>A. 以 1 为增量递增 datepart  
下面的每条语句以 1 为增量递增 datepart。
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT 'year', DATEADD(year,1,@datetime2)  
UNION ALL  
SELECT 'quarter',DATEADD(quarter,1,@datetime2)  
UNION ALL  
SELECT 'month',DATEADD(month,1,@datetime2)  
UNION ALL  
SELECT 'dayofyear',DATEADD(dayofyear,1,@datetime2)  
UNION ALL  
SELECT 'day',DATEADD(day,1,@datetime2)  
UNION ALL  
SELECT 'week',DATEADD(week,1,@datetime2)  
UNION ALL  
SELECT 'weekday',DATEADD(weekday,1,@datetime2)  
UNION ALL  
SELECT 'hour',DATEADD(hour,1,@datetime2)  
UNION ALL  
SELECT 'minute',DATEADD(minute,1,@datetime2)  
UNION ALL  
SELECT 'second',DATEADD(second,1,@datetime2)  
UNION ALL  
SELECT 'millisecond',DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT 'microsecond',DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT 'nanosecond',DATEADD(nanosecond,1,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Year         2008-01-01 13:10:10.1111111  
quarter      2007-04-01 13:10:10.1111111  
month        2007-02-01 13:10:10.1111111  
dayofyear    2007-01-02 13:10:10.1111111  
day          2007-01-02 13:10:10.1111111  
week         2007-01-08 13:10:10.1111111  
weekday      2007-01-02 13:10:10.1111111  
hour         2007-01-01 14:10:10.1111111  
minute       2007-01-01 13:11:10.1111111  
second       2007-01-01 13:10:11.1111111  
millisecond  2007-01-01 13:10:10.1121111  
microsecond  2007-01-01 13:10:10.1111121  
nanosecond   2007-01-01 13:10:10.1111111  
```  
  
### <a name="b-incrementing-more-than-one-level-of-datepart-in-one-statement"></a>B. 在一条语句中将 datepart 增加一级以上  
以下每个语句按足够大的 number（数）逐量增加 datepart，该数字应足以同时增加 date 的下一个更高的 datepart。
  
```sql
DECLARE @datetime2 datetime2;  
SET @datetime2 = '2007-01-01 01:01:01.1111111';  
--Statement                                 Result     
-------------------------------------------------------------------   
SELECT DATEADD(quarter,4,@datetime2);     --2008-01-01 01:01:01.110  
SELECT DATEADD(month,13,@datetime2);      --2008-02-01 01:01:01.110  
SELECT DATEADD(dayofyear,365,@datetime2); --2008-01-01 01:01:01.110  
SELECT DATEADD(day,365,@datetime2);       --2008-01-01 01:01:01.110  
SELECT DATEADD(week,5,@datetime2);        --2007-02-05 01:01:01.110  
SELECT DATEADD(weekday,31,@datetime2);    --2007-02-01 01:01:01.110  
SELECT DATEADD(hour,23,@datetime2);       --2007-01-02 00:01:01.110  
SELECT DATEADD(minute,59,@datetime2);     --2007-01-01 02:00:01.110  
SELECT DATEADD(second,59,@datetime2);     --2007-01-01 01:02:00.110  
SELECT DATEADD(millisecond,1,@datetime2); --2007-01-01 01:01:01.110  
```  
  
### <a name="c-using-expressions-as-arguments-for-the-number-and-date-parameters"></a>C. 使用表达式作为 number 和 date 形参的实参  
以下示例使用不同类型的表达式作为 number 和 date 形参的实参。 示例使用 AdventureWorks 数据库。
  
#### <a name="specifying-a-column-as-date"></a>将一列指定为 date  
以下示例将 `2` 天加到 `OrderDate` 列中的每个值，以派生名为 `PromisedShipDate` 的新列。
  
```sql
SELECT SalesOrderID  
    ,OrderDate   
    ,DATEADD(day,2,OrderDate) AS PromisedShipDate  
FROM Sales.SalesOrderHeader;  
```  
  
以下为部分结果集。
  
```sql
SalesOrderID OrderDate               PromisedShipDate  
------------ ----------------------- -----------------------  
43659        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43660        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43661        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
...  
43702        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43703        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43704        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43705        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43706        2005-07-03 00:00:00.000 2005-07-05 00:00:00.000  
...  
43711        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
43712        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
...  
43740        2005-07-11 00:00:00.000 2005-07-13 00:00:00.000  
43741        2005-07-12 00:00:00.000 2005-07-14 00:00:00.000  
  
```  
  
#### <a name="specifying-user-defined-variables-as-number-and-date"></a>将用户定义的变量指定为 number 和 date  
以下示例将用户定义的变量指定为 number 和 date 的参数。
  
```sql
DECLARE @days int = 365,   
        @datetime datetime = '2000-01-01 01:01:01.111'; /* 2000 was a leap year */;  
SELECT DATEADD(day, @days, @datetime);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------------------  
2000-12-31 01:01:01.110  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-system-function-as-date"></a>将标量系统函数指定为 date  
下例指定 `SYSDATETIME` 作为 date。
  
```sql
SELECT DATEADD(month, 1, SYSDATETIME());  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------  
2013-02-06 14:29:59.6727944  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-subqueries-and-scalar-functions-as-number-and-date"></a>将标量子查询和标量函数指定为 number 和 date  
下例使用标量子查询 `MAX(ModifiedDate)` 作为 number 和 date 的参数。 `(SELECT TOP 1 BusinessEntityID FROM Person.Person)` 是 number 形参的假实参，用来说明如何从值列表中选择 number 实参。
  
```sql
SELECT DATEADD(month,(SELECT TOP 1 BusinessEntityID FROM Person.Person),  
    (SELECT MAX(ModifiedDate) FROM Person.Person));  
```  
  
#### <a name="specifying-numeric-expressions-and-scalar-system-functions-as-number-and-date"></a>将数值表达式和标量系统函数指定为 number 和 date  
以下示例将数值表达式 (-`(10/2))`、[一元运算符](../../mdx/unary-operators.md) (`-`)、[算术运算符](../../mdx/arithmetic-operators.md) (`/`) 和标量系统函数 (`SYSDATETIME`) 作为 number 和 date 的参数。
  
```sql
SELECT DATEADD(month,-(10/2), SYSDATETIME());  
```  
  
#### <a name="specifying-ranking-functions-as-number"></a>将排名函数指定为 number  
下例将排名函数用作 number 的参数。
  
```sql
SELECT p.FirstName, p.LastName  
    ,DATEADD(day,ROW_NUMBER() OVER (ORDER BY  
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
#### <a name="specifying-an-aggregate-window-function-as-number"></a>将聚合开窗函数指定为 number  
下例使用聚合开窗函数作为 number 的参数。
  
```sql
SELECT SalesOrderID, ProductID, OrderQty  
    ,DATEADD(day,SUM(OrderQty)   
        OVER(PARTITION BY SalesOrderID),SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

