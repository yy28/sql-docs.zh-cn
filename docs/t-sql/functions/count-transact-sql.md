---
title: COUNT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
- COUNT_TSQL
- COUNT
dev_langs:
- TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT function
- totals [SQL Server]
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT function [Transact-SQL]
ms.assetid: 28d39da6-bc2e-46c7-858c-b1721c938830
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0342e593b0bf13b5e5a9b53600aae5f3c39ae59d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="count-transact-sql"></a>COUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回组中的项数。 COUNT 与 [COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md) 函数类似。 两个函数唯一的差别是它们的返回值。 COUNT 始终返回 int 数据类型值。 COUNT_BIG 始终返回 bigint 数据类型值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )   
    [ OVER (   
        [ partition_by_clause ]   
        [ order_by_clause ]   
        [ ROW_or_RANGE_clause ]  
    ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregation Function Syntax  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )  

-- Analytic Function Syntax  
COUNT ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>参数  
**ALL**  
向所有值应用此聚合函数。 ALL 为默认值。
  
DISTINCT  
指定 COUNT 返回唯一非 Null 值的数量。
  
*expression*  
任意类型（text、image 或 ntext 除外）的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。 不允许使用聚合函数和子查询。
  
\*  
指定应该计算所有行以返回表中行的总数。 COUNT(\*) 不需要任何参数，而且不能与 DISTINCT 一起使用。 COUNT(\*) 不需要 expression 参数，因为根据定义，该函数不使用有关任何特定列的信息。 COUNT(*) 返回指定表中行数而不删除副本。 它对各行分别计数。 包括包含空值的行。
  
OVER **(** [ *partition_by_clause* ] [ *order_by_clause* ] [ *ROW_or_RANGE_clause* ] **)**  
partition_by_clause 将 FROM 子句生成的结果集划分为要应用函数的分区。 如果未指定，则此函数将查询结果集的所有行视为单个组。 order_by_clause 确定执行操作的逻辑顺序。 有关详细信息，请参阅 [OVER 子句 (Transact-SQL)](../../t-sql/queries/select-over-clause-transact-sql.md)。
  
## <a name="return-types"></a>返回类型
 **int**  
  
## <a name="remarks"></a>Remarks  
COUNT(*) 返回组中的项数。 包括 NULL 值和重复项。
  
COUNT(ALL expression) 计算组中每行的 expression，然后返回非 null 值的数量。
  
COUNT (DISTINCT expression) 计算组中每行的 expression，然后返回独一无二的非 null 值的数量。
  
对于大于 2^31-1 的返回值，COUNT 生成一个错误。 这时应使用 COUNT_BIG。
  
COUNT 不与 OVER 和 ORDER BY 子句配合使用时为确定性函数。 与 OVER 和 ORDER BY 子句一同指定时，它具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。
  
## <a name="examples"></a>示例  
  
### <a name="a-using-count-and-distinct"></a>A. 使用 COUNT 和 DISTINCT  
以下示例列出了在 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 工作的雇员可以拥有的不同职位的数量。
  
```sql
SELECT COUNT(DISTINCT Title)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
67  
  
(1 row(s) affected)
```
  
### <a name="b-using-count"></a>B. 使用 COUNT(*)  
以下示例计算 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 的雇员总数。
  
```sql
SELECT COUNT(*)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
290  
  
(1 row(s) affected)
```
  
### <a name="c-using-count-with-other-aggregates"></a>C. 组合使用 COUNT(*) 和其他聚合函数  
以下示例显示可以组合使用 `COUNT(*)` 和选择列表中的其他聚合函数。 该示例使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库。
  
```sql
SELECT COUNT(*), AVG(Bonus)  
FROM Sales.SalesPerson  
WHERE SalesQuota > 25000;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
----------- ---------------------
14            3472.1428
  
(1 row(s) affected)
```
  
### <a name="d-using-the-over-clause"></a>D. 使用 OVER 子句  
以下示例将 MIN、MAX、AVG 和 COUNT 函数与 OVER 子句结合使用，以便为 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `HumanResources.Department` 表中的每个部门提供聚合值。
  
```sql
SELECT DISTINCT Name  
       , MIN(Rate) OVER (PARTITION BY edh.DepartmentID) AS MinSalary  
       , MAX(Rate) OVER (PARTITION BY edh.DepartmentID) AS MaxSalary  
       , AVG(Rate) OVER (PARTITION BY edh.DepartmentID) AS AvgSalary  
       ,COUNT(edh.BusinessEntityID) OVER (PARTITION BY edh.DepartmentID) AS EmployeesPerDept  
FROM HumanResources.EmployeePayHistory AS eph  
JOIN HumanResources.EmployeeDepartmentHistory AS edh  
     ON eph.BusinessEntityID = edh.BusinessEntityID  
JOIN HumanResources.Department AS d  
ON d.DepartmentID = edh.DepartmentID
WHERE edh.EndDate IS NULL  
ORDER BY Name;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Name                          MinSalary             MaxSalary             AvgSalary             EmployeesPerDept  
----------------------------- --------------------- --------------------- --------------------- ----------------  
Document Control              10.25                 17.7885               14.3884               5  
Engineering                   32.6923               63.4615               40.1442               6  
Executive                     39.06                 125.50                68.3034               4  
Facilities and Maintenance    9.25                  24.0385               13.0316               7  
Finance                       13.4615               43.2692               23.935                10  
Human Resources               13.9423               27.1394               18.0248               6  
Information Services          27.4038               50.4808               34.1586               10  
Marketing                     13.4615               37.50                 18.4318               11  
Production                    6.50                  84.1346               13.5537               195  
Production Control            8.62                  24.5192               16.7746               8  
Purchasing                    9.86                  30.00                 18.0202               14  
Quality Assurance             10.5769               28.8462               15.4647               6  
Research and Development      40.8654               50.4808               43.6731               4  
Sales                         23.0769               72.1154               29.9719               18  
Shipping and Receiving        9.00                  19.2308               10.8718               6  
Tool Design                   8.62                  29.8462               23.5054               6  
  
(16 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-count-and-distinct"></a>E. 使用 COUNT 和 DISTINCT  
以下示例列出了在一家特定公司任职的雇员可以拥有的不同职位的数量。
  
```sql
USE ssawPDW;  
  
SELECT COUNT(DISTINCT Title)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
67
```  
  
### <a name="f-using-count"></a>F. 使用 COUNT(*)  
下面的示例返回 `dbo.DimEmployee` 表中的总行数。
  
```sql
USE ssawPDW;  
  
SELECT COUNT(*)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-------------
296
```  
  
### <a name="g-using-count-with-other-aggregates"></a>G. 组合使用 COUNT(*) 和其他聚合函数  
下面的示例组合使用 `COUNT(*)` 和 SELECT 列表中的其他聚合函数。 该查询返回年度销售配额大于 $500,000 和平均销售配额的销售代表的人数。
  
```sql
USE ssawPDW;  
  
SELECT COUNT(EmployeeKey) AS TotalCount, AVG(SalesAmountQuota) AS [Average Sales Quota]  
FROM dbo.FactSalesQuota  
WHERE SalesAmountQuota > 500000 AND CalendarYear = 2001;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
TotalCount  Average Sales Quota
----------  -------------------
10          683800.0000
```
  
### <a name="h-using-count-with-having"></a>H. 将 COUNT 与 HAVING 配合使用  
下面的示例将 COUNT 与 HAVING 子句配合使用，返回公司中员工数超过 15 人的部门。
  
```sql
USE ssawPDW;  
  
SELECT DepartmentName,   
       COUNT(EmployeeKey)AS EmployeesInDept  
FROM dbo.DimEmployee  
GROUP BY DepartmentName  
HAVING COUNT(EmployeeKey) > 15;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
DepartmentName  EmployeesInDept
--------------  ---------------
Sales           18
Production      179
```
  
### <a name="i-using-count-with-over"></a>I. 将 COUNT 与 OVER 配合使用  
下面的示例将 COUNT 与 OVER 子句配合使用，返回指定的每个销售订单中包含的产品数。
  
```sql
USE ssawPDW;  
  
SELECT DISTINCT COUNT(ProductKey) OVER(PARTITION BY SalesOrderNumber) AS ProductCount  
    ,SalesOrderNumber  
FROM dbo.FactInternetSales  
WHERE SalesOrderNumber IN (N'SO53115',N'SO55981');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
ProductCount   SalesOrderID`
------------   -----------------
3              SO53115
1              SO55981
```
  
## <a name="see-also"></a>另请参阅
[聚合函数 (Transact-SQL)](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT_BIG (Transact-SQL)](../../t-sql/functions/count-big-transact-sql.md)  
[OVER 子句 (Transact-SQL)](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  


