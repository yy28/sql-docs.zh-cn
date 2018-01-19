---
title: "在 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/29/2016
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
- IN_TSQL
- IN
dev_langs: TSQL
helpviewer_keywords:
- values [SQL Server], matching
- NOT IN keyword
- 8623 (Database Engine error)
- matching values in subquery or list [SQL Server]
- IN keyword
- 8632 (Database Engine error)
ms.assetid: 4419de73-96b1-4dfe-8500-f4507915db04
caps.latest.revision: "37"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 610c374bb6d935495779362d8dd7f1e0a53931d8
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="in-transact-sql"></a>IN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  确定指定的值是否与子查询或列表中的值相匹配。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
test_expression [ NOT ] IN   
    ( subquery | expression [ ,...n ]  
    )   
```  
  
## <a name="arguments"></a>参数  
 *test_expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 *subquery*  
 包含某列结果集的子查询。 此列必须具有相同的数据类型作为*test_expression*。  
  
 *表达式*[ **，**...*n* ]  
 一个表达式列表，用来测试是否匹配。 所有表达式都必须与同一类型*test_expression*。  
  
## <a name="result-types"></a>结果类型  
 **Boolean**  
  
## <a name="result-value"></a>结果值  
 如果值*test_expression*相当于返回的任何值*子查询*或等同于任何*表达式*从逗号分隔列表中，结果值为 TRUE;否则，结果值为 FALSE。  
  
 使用 NOT IN 求反*子查询*值或*表达式*。  
  
> [!CAUTION]  
>  任何 null 值返回*子查询*或*表达式*可进行比较，到*test_expression*使用 IN 或不在返回未知。 将空值与 IN 或 NOT IN 一起使用会产生意外结果。  
  
## <a name="remarks"></a>注释  
 明确包含在括号里，IN 子句中的数量极大的值 （数千个用逗号分隔的值） 可以使用资源，并将返回错误 8623 或 8632。 若要解决此问题，请将项存储在表中，列表中，并使用 IN 子句中的选择子查询。  
  
 错误 8623：  
  
 `The query processor ran out of internal resources and could not produce a query plan. This is a rare event and only expected for extremely complex queries or queries that reference a very large number of tables or partitions. Please simplify the query. If you believe you have received this message in error, contact Customer Support Services for more information.`  
  
 错误 8632:  
  
 `Internal error: An expression services limit has been reached. Please look for potentially complex expressions in your query, and try to simplify them.`  
  
## <a name="examples"></a>示例  
  
### <a name="a-comparing-or-and-in"></a>A. 比较 OR 和 IN  
 以下示例选择设计工程师、工具设计人员或销售助理等雇员的姓名列表。  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle = 'Design Engineer'   
   OR e.JobTitle = 'Tool Designer'   
   OR e.JobTitle = 'Marketing Assistant';  
GO  
```  
  
 但是，也可以使用 IN 检索相同的结果：  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle IN ('Design Engineer', 'Tool Designer', 'Marketing Assistant');  
GO  
```  
  
 以下是上面任一查询的结果集。  
  
```  
FirstName   LastName      Title  
---------   ---------   ---------------------  
Sharon      Salavaria   Design Engineer                                     
Gail        Erickson    Design Engineer                                     
Jossef      Goldberg    Design Engineer                                     
Janice      Galvin      Tool Designer                                       
Thierry     D'Hers      Tool Designer                                       
Wanida      Benshoof    Marketing Assistant                                 
Kevin       Brown       Marketing Assistant                                 
Mary        Dempsey     Marketing Assistant                                 
  
(8 row(s) affected)  
```  
  
### <a name="b-using-in-with-a-subquery"></a>B. 带子查询使用 IN  
 以下示例查找 `SalesPerson` 表中所有销售人员的 ID 以获得当年销售额超过 $250,000 的雇员，然后从 `Employee` 表中选择 `EmployeeID` 与 `SELECT` 子查询的结果相匹配的所有雇员的姓名。  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
FirstName   LastName                                             
---------   --------   
Tsvi         Reiter                                              
Michael      Blythe                                              
Tete         Mensa-Annan                                         
  
(3 row(s) affected)  
```  
  
### <a name="c-using-not-in-with-a-subquery"></a>C. 带子查询使用 NOT IN  
 以下示例查找销售额不超过 $250,000 的销售人员。 `NOT IN` 查找与值列表中的项不匹配的销售人员。  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID NOT IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-in-and-not-in"></a>D. 在和中不使用  
 下面的示例查找中的所有条目`FactInternetSales`表匹配`SalesReasonKey`中值`DimSalesReason`表。  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
IN (SELECT SalesReasonKey FROM DimSalesReason);   
```  
  
 下面的示例查找中的所有条目`FactInternetSalesReason`不匹配的表`SalesReasonKey`中值`DimSalesReason`表。  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
NOT IN (SELECT SalesReasonKey FROM DimSalesReason);  
```  
  
### <a name="e-using-in-with-an-expression-list"></a>E. 使用使用表达式列表  
 下面的示例中的销售人员的查找所有 Id`DimEmployee`表员工都使用第一个名称，它是或者`Mike`或`Michael`。  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM DimEmployee  
WHERE FirstName IN ('Mike', 'Michael');  
```  
  
## <a name="see-also"></a>另请参阅  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [所有 &#40;Transact SQL &#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [某些 &#124;任何 &#40;Transact SQL &#41;](../../t-sql/language-elements/some-any-transact-sql.md)  
  
  



