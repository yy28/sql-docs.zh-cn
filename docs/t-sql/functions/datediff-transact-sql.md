---
title: DATEDIFF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEDIFF_TSQL
- DATEDIFF
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATEDIFF function [SQL Server]
- time [SQL Server], crossed boundaries
- differences in date and time [SQL Server]
- counting crossed date time boundaries [SQL Server]
- date and time [SQL Server], DATEDIFF
- dates [SQL Server], crossed boundaries
- boundary differences date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- interval dates [SQL Server]
- time [SQL Server], functions
- crossing date time boundaries [SQL Server]
- calculating dates times [SQL Server]
ms.assetid: eba979f2-1a8d-4cce-9d75-b74f9b519b37
caps.latest.revision: 52
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cff08ca1fd9275983fa4af4a9f09efed6d3f0f0f
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43081856"
---
# <a name="datediff-transact-sql"></a>DATEDIFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函数返回指定的 startdate 和 enddate 之间所跨的指定 datepart 边界的计数（作为带符号整数值）。
  
有关处理 startdate 和 enddate 值之间较大差异的函数，请参阅 [DATEDIFF_BIG (TRANSACT-SQ)](../../t-sql/functions/datediff-big-transact-sql.md)。 有关所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和时间数据类型及函数的概述，请参阅[日期和时间数据类型及函数 (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATEDIFF ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>参数  
*datepart*  
指定所跨边界类型的 startdate 和 enddate 的一部分。 `DATEDIFF` 不接受用户定义的变量等效项。 此表列出了所有有效的 datepart 参数。
  
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
可解析为下列值之一的表达式：

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**
  
使用四位数年份可避免含糊不清。 有关两位数年份值的信息，请参阅[配置两位数年份截止服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
enddate  
请参阅 startdate。
  
## <a name="return-type"></a>返回类型  
 **int**  
  
## <a name="return-value"></a>返回值  
  
-   每个特定的 datepart 及其相应缩写将返回相同的值。  
  
若 bigint 的返回值超出范围（-2,147,483,648 到 +2,147,483,647），`DATEDIFF` 返回错误。  对于 millisecond，startdate 和 enddate 之间的最大差值为 24 天 20 小时 31 分钟 23.647 秒。 对于 second，最大差值为 68 年。
  
如果为 startdate 和 enddate 都只指定了时间值，并且 datepart 不是时间 datepart，则 `DATEDIFF` 返回 0。
  
`DATEDIFF` 不使用 startdate 或 enddate 的时区偏移量部分来计算返回值。
  
由于 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 仅精确到分钟，因此在 startdate 或 enddate 具有 smalldatetime 值时，返回值中的秒和毫秒将始终设置为 0。
  
如果只为某个日期数据类型变量指定时间值，`DATEDIFF` 会将所缺日期部分的值设置为默认值：1900-01-01。 如果只为某个时间或日期数据类型的变量指定日期值，`DATEDIFF` 会将所缺时间部分的值设置为默认值：00:00:00。 如果 startdate 和 enddate 中有一个只含时间部分，另一个只含日期部分，`DATEDIFF` 会将所缺时间和日期部分设置为各自的默认值。
  
如果 startdate 和 enddate 具有不同的日期数据类型，并且其中一个的时间部分或秒小数部分精度比另一个高，`DATEDIFF` 会将另一个的所缺部分设置为 0。
  
## <a name="datepart-boundaries"></a>datepart 边界  
以下语句具有相同的 startdate 和 enddate 值。 这些日期是相邻的，它们在时间上相差 0.0000001 秒。 每个语句中 startdate 与 enddate 之间的差跨其 datepart 的一个日历或时间边界。 每个语句都返回 1。 如果 startdate 和 enddate 的年份值不同，但它们的日历周值相同，`DATEDIFF` 将对 datepart week 返回 0。
  
```sql
SELECT DATEDIFF(year,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(quarter,     '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(month,       '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(dayofyear,   '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(day,         '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(week,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(hour,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(minute,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(second,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Remarks  
在 SELECT <list>、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中使用 `DATEDIFF`。
  
`DATEDIFF` 将字符串文字隐式转换为 datetime2 类型。 这就意味着，日期在作为字符串传递时，`DATEDIFF` 不会支持 YDM 格式。 必须先将字符串显式转换为 datetime 或 smalldatetime 类型，然后才能使用 YDM 格式。
  
指定 SET DATEFIRST 对 `DATEDIFF` 不起作用。 `DATEDIFF` 始终使用星期日作为每周的第一天，确保函数以确定性方式运行。
  
## <a name="examples"></a>示例  
以下示例使用不同类型的表达式作为 startdate 和 enddate 形参的实参。
  
### <a name="a-specifying-columns-for-startdate-and-enddate"></a>A. 为 startdate 和 enddate 指定列  
此示例计算一个表的两列中的日期之间所跨越的日边界数。
  
```sql
CREATE TABLE dbo.Duration  
    (startDate datetime2, endDate datetime2);  
    
INSERT INTO dbo.Duration(startDate, endDate)  
    VALUES ('2007-05-06 12:10:09', '2007-05-07 12:10:09');  
    
SELECT DATEDIFF(day, startDate, endDate) AS 'Duration'  
    FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="b-specifying-user-defined-variables-for-startdate-and-enddate"></a>B. 为 startdate 和 enddate 指定用户定义的变量  
在此示例中，用户定义的变量充当 startdate 和 enddate 的参数。
  
```sql
DECLARE @startdate datetime2 = '2007-05-05 12:10:09.3312722';  
DECLARE @enddate   datetime2 = '2007-05-04 12:10:09.3312722';   
SELECT DATEDIFF(day, @startdate, @enddate);  
```  
  
### <a name="c-specifying-scalar-system-functions-for-startdate-and-enddate"></a>C. 为 startdate 和 enddate 指定标量系统函数  
此示例使用标量系统函数作为 startdate 和 enddate 的参数。
  
```sql
SELECT DATEDIFF(millisecond, GETDATE(), SYSDATETIME());  
```  
  
### <a name="d-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>D. 为 startdate 和 enddate 指定标量子查询和标量函数  
此示例使用标量子查询和标量函数作为 startdate 和 enddate 的参数。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day,
    (SELECT MIN(OrderDate) FROM Sales.SalesOrderHeader),  
    (SELECT MAX(OrderDate) FROM Sales.SalesOrderHeader));  
```  
  
### <a name="e-specifying-constants-for-startdate-and-enddate"></a>E. 为 startdate 和 enddate 指定常量  
此示例使用字符常量作为 startdate 和 enddate 的参数。
  
```sql
SELECT DATEDIFF(day,
   '2007-05-07 09:53:01.0376635',
   '2007-05-08 09:53:01.0376635');  
```  
  
### <a name="f-specifying-numeric-expressions-and-scalar-system-functions-for-enddate"></a>F. 为 enddate 指定数值表达式和标量系统函数  
此示例使用数值表达式（`(GETDATE() + 1)`）和标量系统函数（`GETDATE` 和 `SYSDATETIME`）作为 enddate 的参数。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', GETDATE() + 1)   
    AS NumberOfDays  
    FROM Sales.SalesOrderHeader;  
GO  
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', DATEADD(day, 1, SYSDATETIME())) AS NumberOfDays  
    FROM Sales.SalesOrderHeader;  
GO  
```  
  
### <a name="g-specifying-ranking-functions-for-startdate"></a>G. 为 startdate 指定排名函数  
此示例使用排名函数作为 startdate 的参数。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,DATEDIFF(day, ROW_NUMBER() OVER (ORDER BY   
        a.PostalCode), SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson s   
    INNER JOIN Person.Person p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
### <a name="h-specifying-an-aggregate-window-function-for-startdate"></a>H. 为 startdate 指定聚合开窗函数  
此示例使用聚合开窗函数作为 startdate 的参数。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT soh.SalesOrderID, sod.ProductID, sod.OrderQty, soh.OrderDate,
    DATEDIFF(day, MIN(soh.OrderDate)   
        OVER(PARTITION BY soh.SalesOrderID), SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail sod  
    INNER JOIN Sales.SalesOrderHeader soh  
        ON sod.SalesOrderID = soh.SalesOrderID  
WHERE soh.SalesOrderID IN(43659, 58918);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
以下示例使用不同类型的表达式作为 startdate 和 enddate 形参的实参。
  
### <a name="i-specifying-columns-for-startdate-and-enddate"></a>I. 为 startdate 和 enddate 指定列  
此示例计算一个表的两列中的日期之间所跨越的日边界数。
  
```sql
CREATE TABLE dbo.Duration 
    (startDate datetime2, endDate datetime2);
    
INSERT INTO dbo.Duration (startDate, endDate)  
    VALUES ('2007-05-06 12:10:09', '2007-05-07 12:10:09');  
    
SELECT TOP(1) DATEDIFF(day, startDate, endDate) AS Duration  
    FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="j-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>J. 为 startdate 和 enddate 指定标量子查询和标量函数  
此示例使用标量子查询和标量函数作为 startdate 和 enddate 的参数。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day, (SELECT MIN(HireDate) FROM dbo.DimEmployee),  
    (SELECT MAX(HireDate) FROM dbo.DimEmployee))   
FROM dbo.DimEmployee;  
  
```  
  
### <a name="k-specifying-constants-for-startdate-and-enddate"></a>K. 为 startdate 和 enddate 指定常量  
此示例使用字符常量作为 startdate 和 enddate 的参数。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day,
    '2007-05-07 09:53:01.0376635',
    '2007-05-08 09:53:01.0376635') FROM DimCustomer;  
```  
  
### <a name="l-specifying-ranking-functions-for-startdate"></a>L. 为 startdate 指定排名函数  
此示例使用排名函数作为 startdate 的参数。
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName,
    DATEDIFF(day, ROW_NUMBER() OVER (ORDER BY   
        DepartmentName), SYSDATETIME()) AS RowNumber  
FROM dbo.DimEmployee;  
```  
  
### <a name="m-specifying-an-aggregate-window-function-for-startdate"></a>M. 为 startdate 指定聚合开窗函数  
此示例使用聚合开窗函数作为 startdate 的参数。
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, DepartmentName,
    DATEDIFF(year, MAX(HireDate)  
        OVER (PARTITION BY DepartmentName), SYSDATETIME()) AS SomeValue  
FROM dbo.DimEmployee  
```  
  
## <a name="see-also"></a>另请参阅
[DATEDIFF_BIG (Transact-SQL)](../../t-sql/functions/datediff-big-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


