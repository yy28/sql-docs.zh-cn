---
title: "联合 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UNION
- UNION_TSQL
dev_langs: TSQL
helpviewer_keywords:
- UNION queries
- combining query results
- UNION operator [SQL Server]
ms.assetid: 607c296f-8a6a-49bc-975a-b8d0c0914df7
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 04f90ae1f5976e29a8281cab3638b63f0525f454
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="set-operators---union-transact-sql"></a>集运算符的联合 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  将两个或更多个查询的结果合并为单个结果集，该结果集包含联合查询中的所有查询的全部行。 UNION 运算不同于使用联接合并两个表中的列的运算。  
  
 下面列出了使用 UNION 合并两个查询结果集的基本规则：  
  
-   所有查询中的列数和列的顺序必须相同。  
  
-   数据类型必须兼容。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
    { <query_specification> | ( <query_expression> ) }   
  UNION [ ALL ]   
  <query_specification | ( <query_expression> )   
 [ UNION [ ALL ] <query_specification> | ( <query_expression> )   
    [ ...n ] ]   
```  
  
## <a name="arguments"></a>参数  
\<query_specification > |( \<query_expression >) 是一个查询规范或查询表达式返回数据，另一个查询规范或查询表达式中的数据组合在一起。 作为 UNION 运算的一部分的列定义可以不相同，但它们必须通过隐式转换实现兼容。 如果数据类型不相同，生成的数据类型可根据确定的规则进行[数据类型优先级](../../t-sql/data-types/data-type-precedence-transact-sql.md)。 如果类型相同，但精度、小数位数或长度不同，则根据用于合并表达式的相同规则来确定结果。 有关详细信息，请参阅[精度、小数位数和长度 (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
 列的**xml**数据类型必须为等效。 所有的列必须类型化为 XML 架构或是非类型化的。 如果要类型化，这些列必须类型化为相同的 XML 架构集合。  
  
 UNION  
 指定合并多个结果集并将其作为单个结果集返回。  
  
 ALL  
 将全部行并入结果中。 其中包括重复行。 如果未指定该参数，则删除重复行。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-a-simple-union"></a>A. 使用简单 UNION  
 在下面的示例中，结果集同时包含 `ProductModelID` 和 `Name` 表中的 `ProductModel` 与 `Gloves` 列中的内容。  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Here is the simple union.  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
```  
  
### <a name="b-using-select-into-with-union"></a>B. 将 SELECT INTO 与 UNION 一起使用  
 在下面的示例中，第二个 `INTO` 语句中的 `SELECT` 子句指定名为 `ProductResults` 的表保存 `ProductModel` 和 `Gloves` 表中的指定列的并集（最终结果集）。 注意，`Gloves` 表是由第一个 `SELECT` 语句创建的。  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.ProductResults', 'U') IS NOT NULL  
DROP TABLE dbo.ProductResults;  
GO  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
INTO dbo.ProductResults  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
SELECT ProductModelID, Name   
FROM dbo.ProductResults;  
  
```  
  
### <a name="c-using-union-of-two-select-statements-with-order-by"></a>C. 将 ORDER BY 与两个 SELECT 语句的 UNION 一起使用  
 在 UNION 子句中使用的某些参数的顺序非常重要。 下面的示例通过两个 `UNION` 语句说明 `SELECT` 的错误用法和正确用法（在这两个语句的输出中将重命名一个列）。  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
/* INCORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
ORDER BY Name  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
/* CORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
  
```  
  
### <a name="d-using-union-of-three-select-statements-to-show-the-effects-of-all-and-parentheses"></a>D. 使用三个 SELECT 语句的 UNION 来说明 ALL 和括号的作用  
 下列示例使用 `UNION` 来组合具有相同 5 行数据的三个表的结果。 第一个示例使用 `UNION ALL` 显示重复记录，返回所有的 15 行。 第二个示例使用不带 `UNION` 的 `ALL`，删除三个 `SELECT` 语句的组合结果中的重复行，返回 5 行。  
  
 第三个示例将 `ALL` 用于第一个 `UNION`，并用括号将第二个没有使用 `UNION` 的 `ALL` 括起来。 第二个 `UNION` 因位于括号内而首先得到处理，并且因为没有使用 `ALL` 选项，所以重复行被删除而返回 5 行。 通过使用 `SELECT` 关键字将这 5 行与第一个 `UNION ALL` 的结果组合在一起。 这不会删除两个 5 行结果集之间的重复行。 最终结果有 10 行。  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.EmployeeOne', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeOne;  
GO  
IF OBJECT_ID ('dbo.EmployeeTwo', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeTwo;  
GO  
IF OBJECT_ID ('dbo.EmployeeThree', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeThree;  
GO  
  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeOne  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeTwo  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeThree  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
-- Union ALL  
SELECT LastName, FirstName, JobTitle  
FROM dbo.EmployeeOne  
UNION ALL  
SELECT LastName, FirstName ,JobTitle  
FROM dbo.EmployeeTwo  
UNION ALL  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle  
FROM dbo.EmployeeOne  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeOne  
UNION ALL  
(  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree  
);  
GO  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-simple-union"></a>E. 使用简单 UNION  
 在下面的示例中，结果集中包括的内容`CustomerKey`的这两列`FactInternetSales`和`DimCustomer`表。 由于未使用的所有关键字，从结果中排除重复项。  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="f-using-union-of-two-select-statements-with-order-by"></a>F. 将 ORDER BY 与两个 SELECT 语句的 UNION 一起使用  
 当在联合语句中任何 SELECT 语句包含 ORDER BY 子句时，该子句应置于之后所有 SELECT 语句中。 下面的示例演示如何正确和错误使用`UNION`在两个`SELECT`语句在其中一列进行排序使用 ORDER BY。  
  
```  
-- Uses AdventureWorks  
  
-- INCORRECT  
SELECT CustomerKey   
FROM FactInternetSales    
ORDER BY CustomerKey  
UNION   
SELECT CustomerKey   
FROM DimCustomer  
ORDER BY CustomerKey;  
  
-- CORRECT   
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="g-using-union-of-two-select-statements-with-where-and-order-by"></a>G. 使用联合的两个 SELECT 语句的位置和 ORDER BY  
 下面的示例演示如何正确和错误使用`UNION`在两个`SELECT`语句在其中并且需要 ORDER BY。  
  
```  
-- Uses AdventureWorks  
  
-- INCORRECT   
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
ORDER BY CustomerKey   
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
  
-- CORRECT  
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="h-using-union-of-three-select-statements-to-show-effects-of-all-and-parentheses"></a>H. 使用联合的三个 SELECT 语句以显示所有的效果和括号  
 下面的示例使用`UNION`来合并结果**同一个表**为了演示所有效果和括号，使用时`UNION`。  
  
 第一个示例使用`UNION ALL`以显示重复记录，并返回每行的源表三次。 第二个示例使用`UNION`而无需`ALL`以消除重复的行从合并的结果的三个`SELECT`语句并返回仅无重复的行从源表。  
  
 第三个示例使用`ALL`与第一个`UNION`和括号内包含第二个`UNION`不使用`ALL`。 第二个`UNION`第一次处理，因为它位于括号中。 它从表返回仅无重复的行，因为`ALL`不使用选项并删除重复项。 与第一个结果相结合，这些行`SELECT`使用`UNION ALL`关键字。 这不会删除两个集之间的重复项。  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL  
(  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
);  
```  
  
## <a name="see-also"></a>另请参阅  
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [选择示例 &#40;Transact SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)  
  
  

