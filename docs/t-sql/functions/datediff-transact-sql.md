---
title: "DATEDIFF (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: dba834b51bab48c2bd30d1bbbb4abe11694ab321
ms.contentlocale: zh-cn
ms.lasthandoff: 10/05/2017

---
# <a name="datediff-transact-sql"></a>DATEDIFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回指定的计数 （带符号整数） *datepart*之间指定跨越边界*startdate*和*enddate*。
  
对于更大的差异，请参阅[DATEDIFF_BIG &#40;Transact SQL &#41;](../../t-sql/functions/datediff-big-transact-sql.md). 有关的所有概述[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和时间数据类型和函数，请参阅[日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATEDIFF ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>参数  
*datepart*  
是的一部分*startdate*和*enddate* ，指定删除线的边界的类型。 下表列出所有有效*datepart*自变量。 用户定义的变量等效项是无效的。
  
|*datepart*|缩写形式|  
|---|---|
|**年**|**yy、 yyyy**|  
|**季度**|**qq、 q**|  
|**月**|**mm、 m**|  
|**dayofyear**|**dy、 y**|  
|**一天**|**dd、 d**|  
|**周**|**wk、 ww**|  
|**小时**|**hh**|  
|**分钟**|**mi、 n**|  
|**第二个**|**ss、 s**|  
|**毫秒**|**ms**|  
|**微秒**|**mcs**|  
|**纳秒为**|**ns**|  
  
*startdate*  
是可被解析为一个表达式**时间**，**日期**， **smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。 *日期*可以是表达式、 列表达式、 用户定义变量或字符串文本。 *startdate*减去*enddate*。
  
为避免不确定性，请使用四位数年份。 两位数年份的相关信息，请参阅[配置两位数年份截止服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
*结束日期*  
请参阅*startdate*。
  
## <a name="return-type"></a>返回类型  
 **int**  
  
## <a name="return-value"></a>返回值  
  
-   每个*datepart*和其缩写返回相同的值。  
  
如果返回的值超出范围**int** (-2,147,483,648 到 + 2147483647 之间) 返回一个错误。 有关**毫秒**，之间的最大偏差*startdate*和*enddate*是 24 天，20 小时 31 分钟和 23.647 秒。 有关**第二个**，最大的区别是 68 年。
  
如果*startdate*和*enddate*都分配只有一个时间值与*datepart*不是时间*datepart*，则返回 0。
  
时区偏移量的组件*startdate*或*endate*不用于计算的返回值。
  
因为[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)精确到最的分钟数，仅当**smalldatetime**值用于*startdate*或*enddate*(秒）和毫秒始终设置为在返回值为 0。
  
如果仅时间值分配给日期数据类型的变量，则缺少的日期部分的值将设置为默认值： 1900年-01-01。 如果仅日期值分配给时间或日期数据类型的变量，缺少的时间部分的值将设置为默认值： 00:00:00。 如果任一*startdate*或*enddate*具有仅时间部分和其他仅日期部分、 缺少时间和日期部分设置为默认值。
  
如果*startdate*和*enddate*不同日期数据类型和一个具有更多的时间部分或比另秒的小数部分精度，缺少的其他部分将设置为 0。
  
## <a name="datepart-boundaries"></a>日期部分边界  
以下语句具有相同*startdate*和同一*endate*。 这些日期是相邻的，在时间上相差 .0000001 秒。 之间的差异*startdate*和*endate*在每个语句中跨越一个日历或时间边界的其*datepart*。 每个语句都返回 1。 如果对于此示例使用了不同年份，如果这两个*startdate*和*endate*处于同一个日历周的返回值**周**将为 0。
  
```sql
SELECT DATEDIFF(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>注释  
DATEDIFF 可用在选择列表、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
DATEDIFF 隐式强制转换为字符串文本**datetime2**类型。 这就意味着，日期在作为字符串传递时，DATEDIFF 不会支持 YDM 格式。 必须显式强制转换为字符串**datetime**或**smalldatetime**要使用的 YDM 格式类型。
  
指定 SET DATEFIRST 对 DATEDIFF 不起作用。 DATEDIFF 始终使用星期日作为每周的第一天，以确保函数是确定性的。
  
## <a name="examples"></a>示例  
下面的示例使用不同类型的表达式作为自变量为*startdate*和*enddate*参数。
  
### <a name="a-specifying-columns-for-startdate-and-enddate"></a>A. 为 startdate 和 enddate 指定列  
下例计算一个表的两列中的日期之间所跨越的日边界数。
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="b-specifying-user-defined-variables-for-startdate-and-enddate"></a>B. 为 startdate 和 enddate 指定用户定义的变量  
下面的示例使用用户定义的变量作为自变量为*startdate*和*enddate*。
  
```sql
DECLARE @startdate datetime2 = '2007-05-05 12:10:09.3312722';  
DECLARE @enddate datetime2 = '2007-05-04 12:10:09.3312722';   
SELECT DATEDIFF(day, @startdate, @enddate);  
```  
  
### <a name="c-specifying-scalar-system-functions-for-startdate-and-enddate"></a>C. 为 startdate 和 enddate 指定标量系统函数  
下面的示例使用标量系统函数作为自变量为*startdate*和*enddate*。
  
```sql
SELECT DATEDIFF(millisecond, GETDATE(), SYSDATETIME());  
```  
  
### <a name="d-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>D. 为 startdate 和 enddate 指定标量子查询和标量函数  
下面的示例使用标量子查询和标量函数作为自变量为*startdate*和*enddate*。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day,(SELECT MIN(OrderDate) FROM Sales.SalesOrderHeader),  
    (SELECT MAX(OrderDate) FROM Sales.SalesOrderHeader));  
```  
  
### <a name="e-specifying-constants-for-startdate-and-enddate"></a>E. 为 startdate 和 enddate 指定常量  
下面的示例使用字符常量作为参数*startdate*和*enddate*。
  
```sql
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635');  
```  
  
### <a name="f-specifying-numeric-expressions-and-scalar-system-functions-for-enddate"></a>F. 为 enddate 指定数值表达式和标量系统函数  
下面的示例使用数值表达式， `(GETDATE ()+ 1)`，和标量系统函数`GETDATE`和`SYSDATETIME`，作为自变量为*enddate*。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', GETDATE()+ 1)   
    AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', DATEADD(day,1,SYSDATETIME())) AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
```  
  
### <a name="g-specifying-ranking-functions-for-startdate"></a>G. 为 startdate 指定排名函数  
下面的示例使用排名函数为的自变量*startdate*。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson s   
    INNER JOIN Person.Person p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
### <a name="h-specifying-an-aggregate-window-function-for-startdate"></a>H. 为 startdate 指定聚合开窗函数  
下面的示例使用聚合开窗函数的自变量作为*startdate*。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT soh.SalesOrderID, sod.ProductID, sod.OrderQty,soh.OrderDate  
    ,DATEDIFF(day,MIN(soh.OrderDate)   
        OVER(PARTITION BY soh.SalesOrderID),SYSDATETIME() ) AS 'Total'  
FROM Sales.SalesOrderDetail sod  
    INNER JOIN Sales.SalesOrderHeader soh  
        ON sod.SalesOrderID = soh.SalesOrderID  
WHERE soh.SalesOrderID IN(43659,58918);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
下面的示例使用不同类型的表达式作为自变量为*startdate*和*enddate*参数。
  
### <a name="i-specifying-columns-for-startdate-and-enddate"></a>I. 为 startdate 和 enddate 指定列  
下例计算一个表的两列中的日期之间所跨越的日边界数。
  
```sql
CREATE TABLE dbo.Duration (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT TOP(1) DATEDIFF(day,startDate,endDate) AS Duration  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="j-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>J. 为 startdate 和 enddate 指定标量子查询和标量函数  
下面的示例使用标量子查询和标量函数作为自变量为*startdate*和*enddate*。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day,(SELECT MIN(HireDate) FROM dbo.DimEmployee),  
    (SELECT MAX(HireDate) FROM dbo.DimEmployee))   
FROM dbo.DimEmployee;  
  
```  
  
### <a name="k-specifying-constants-for-startdate-and-enddate"></a>K. 为 startdate 和 enddate 指定常量  
下面的示例使用字符常量作为参数*startdate*和*enddate*。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635') FROM DimCustomer;  
```  
  
### <a name="l-specifying-ranking-functions-for-startdate"></a>L. 为 startdate 指定排名函数  
下面的示例使用排名函数为的自变量*startdate*。
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        DepartmentName),SYSDATETIME()) AS RowNumber  
FROM dbo.DimEmployee;  
```  
  
### <a name="m-specifying-an-aggregate-window-function-for-startdate"></a>M. 为 startdate 指定聚合开窗函数  
下面的示例使用聚合开窗函数的自变量作为*startdate*。
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, DepartmentName  
    ,DATEDIFF(year,MAX(HireDate)  
             OVER (PARTITION BY DepartmentName),SYSDATETIME()) AS SomeValue  
FROM dbo.DimEmployee  
```  
  
## <a name="see-also"></a>另请参阅
[DATEDIFF_BIG &#40;Transact SQL &#41;](../../t-sql/functions/datediff-big-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  



