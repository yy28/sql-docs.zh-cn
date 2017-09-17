---
title: "最小值 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MIN
- MIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MIN function [Transact-SQL]
- minimum values [SQL Server]
- values [SQL Server], minimum
ms.assetid: 56cf6ec5-34f5-47e3-a402-7129039d4429
caps.latest.revision: 49
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: eff0ef5388cd1f26053187a3ac06847214f3abf0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="min-transact-sql"></a>MIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回表达式中的最小值。 后面可能跟随[OVER 子句](../../t-sql/queries/select-over-clause-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
    
MIN ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregation Function Syntax  
MIN ( [ ALL | DISTINCT ] expression )  
  
-- Aggregation Function Syntax   
MIN ( expression ) OVER ( [ <partition_by_clause> ] [ <order_by_clause> ] )  
```  
  
## <a name="arguments"></a>参数  
 **ALL**  
 向所有值应用此聚合函数。 ALL 为默认值。  
  
 DISTINCT  
 指定考虑每一个唯一值。 DISTINCT 对于 MIN 无意义，使用它仅仅是为了符合 ISO 标准。  
  
 *expression*  
 常量、列名、函数以及算术运算符、位运算符和字符串运算符的任意组合。 MIN 可以用于**数值**， **char**， **varchar**， **uniqueidentifier**，或**datetime**列，但不是能与**位**列。 不允许使用聚合函数和子查询。  
  
 有关详细信息，请参阅[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 通过**(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause*将划分为分区函数应用到的 FROM 子句生成的结果集。 如果未指定，则此函数将查询结果集的所有行视为单个组。 *order_by_clause*确定在其中执行该操作的逻辑顺序。 *order_by_clause*是必需的。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>返回类型  
 返回一个值与相同*表达式*。  
  
## <a name="remarks"></a>注释  
 MIN 忽略任何 Null 值。  
  
 对于字符数据列，MIN 查找排序序列的最低值。  
  
 MIN 不与 OVER 和 ORDER BY 子句配合使用时为确定性函数。 与 OVER 和 ORDER BY 子句一同指定时，它具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-example"></a>A. 简单示例  
 以下示例返回最低（最小）税率。 该示例使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库  
  
```  
SELECT MIN(TaxRate)  
FROM Sales.SalesTaxRate;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `-------------------`  
  
 `5.00`  
  
 `(1 row(s) affected)`  
  
### <a name="b-using-the-over-clause"></a>B. 使用 OVER 子句  
 以下示例将 MIN、MAX、AVG 和 COUNT 函数与 OVER 子句结合使用，以便为 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `HumanResources.Department` 表中的每个部门提供聚合值。  
  
```  
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
  
```  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-min"></a>C. 使用最小值  
 下面的示例使用 MIN 聚合函数可返回销售订单的指定集中最便宜的 （最小值） 产品的价格。  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT MIN(UnitPrice)  
FROM dbo.FactResellerSales   
WHERE SalesOrderNumber IN (N'SO43659', N'SO43660', N'SO43664');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `------`  
  
 `5.1865`  
  
### <a name="d-using-min-with-over"></a>D. 通过使用最小值  
 下面的示例使用 MIN OVER() 分析函数以返回每个销售订单中的最便宜的产品的价格。 结果集进行分区`SalesOrderID`列。  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT MIN(UnitPrice) OVER(PARTITION BY SalesOrderNumber) AS LeastExpensiveProduct,  
       SalesOrderNumber  
FROM dbo.FactResellerSales    
WHERE SalesOrderNumber IN (N'SO43659', N'SO43660', N'SO43664')  
ORDER BY SalesOrderNumber;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `LeastExpensiveProduct SalesOrderID`  
  
 `--------------------- ----------`  
  
 `5.1865                SO43659`  
  
 `419.4589              SO43660`  
  
 `28.8404               SO43664`  
  
## <a name="see-also"></a>另请参阅  
 [聚合函数 &#40;Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [最大 &#40;Transact SQL &#41;](../../t-sql/functions/max-transact-sql.md)   
 [通过子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  


