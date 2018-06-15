---
title: UNION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- UNION
- UNION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UNION queries
- combining query results
- UNION operator [SQL Server]
ms.assetid: 607c296f-8a6a-49bc-975a-b8d0c0914df7
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 942e0613e4a3c2c540a1a01148e4d9969ff23078
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33065664"
---
# <a name="set-operators---union-transact-sql"></a>集运算符 - UNION (Transact-SQL)
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
\<query_specification> | ( \<query_expression> ) 查询规范或查询表达式，用以返回要与另一个查询规范或查询表达式所返回的数据合并的数据。 作为 UNION 运算的一部分的列定义可以不相同，但它们必须通过隐式转换实现兼容。 如果数据类型不同，则根据[数据类型优先级](../../t-sql/data-types/data-type-precedence-transact-sql.md)规则确定所产生的数据类型。 如果类型相同，但精度、小数位数或长度不同，则根据用于合并表达式的相同规则来确定结果。 有关详细信息，请参阅[精度、小数位数和长度 (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
 xml 数据类型的列必须等价。 所有的列必须类型化为 XML 架构或是非类型化的。 如果要类型化，这些列必须类型化为相同的 XML 架构集合。  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-simple-union"></a>E. 使用简单 UNION  
 在下面的示例中，结果集同时包含 `FactInternetSales` 和 `DimCustomer` 表中的 `CustomerKey` 列中的内容。 由于不使用 ALL 关键字，会从结果中排除重复项。  
  
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
 当 UNION 语句中的任何 SELECT 语句包含 ORDER BY 子句时，该子句应置于所有 SELECT 语句之后。 下面的示例通过两个 `SELECT` 语句说明 `UNION` 的错误用法和正确用法（在这两个语句中使用 ORDER BY 对一个列排序）。  
  
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
  
### <a name="g-using-union-of-two-select-statements-with-where-and-order-by"></a>G. 将 WHERE 和 ORDER BY 与两个 SELECT 语句的 UNION 一起使用  
 下面的示例通过两个 `SELECT` 语句说明 `UNION` 的错误用法和正确用法（在这两个语句中需要 WHERE 和 ORDER BY）。  
  
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
  
### <a name="h-using-union-of-three-select-statements-to-show-effects-of-all-and-parentheses"></a>H. 使用三个 SELECT 语句的 UNION 来说明 ALL 和括号的作用  
 下面的示例使用 `UNION` 来合并同一个表的结果，以演示使用 `UNION` 时 All 和括号的效果。  
  
 第一个示例使用 `UNION ALL` 显示重复记录，并三次返回源表中的每一行。 第二个示例使用不带 `ALL` 的 `UNION`，删除三个 `SELECT` 语句的组合结果中的重复行，仅返回源表中的非重复行。  
  
 第三个示例将 `ALL` 用于第一个 `UNION`，并用括号将第二个没有使用 `ALL` 的 `UNION` 括起来。 首先处理第二个 `UNION`，因为它位于括号中。 仅从表返回非重复行，因为未使用 `ALL` 选项且已删除重复项。 通过使用 `UNION ALL` 关键字将这些行与第一个 `SELECT` 的结果合并在一起。 这不会删除两个集之间的重复行。  
  
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
 [SELECT 示例 (Transact-SQL)](../../t-sql/queries/select-examples-transact-sql.md)  
  
  

