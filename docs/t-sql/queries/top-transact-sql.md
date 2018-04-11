---
title: TOP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TOP_TSQL
- TOP
dev_langs:
- TSQL
helpviewer_keywords:
- TOP clause
- first set of query result rows [SQL Server]
- TOP clause, about TOP clause
- queries [SQL Server], results
ms.assetid: da983c0a-06c5-4cf8-a6a4-7f9d66f34f2c
caps.latest.revision: 60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 926de1152e7c1223441d9ac85da11246049e31ea
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
---
# <a name="top-transact-sql"></a>TOP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  将在查询结果集中返回的行数限制到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的指定行数或行的百分比。 当将 TOP 与 ORDER BY 子句结合使用时，结果集限制为已排序行的前 N 行；否则，它将以未定义的顺序返回前 N 行。 使用此子句可以指定从 SELECT 语句返回的行数，或受 INSERT、UPDATE、MERGE 或 DELETE 语句影响的行数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[   
    TOP (expression) [PERCENT]  
    [ WITH TIES ]  
]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[   
    TOP ( expression )   
    [ WITH TIES ]  
]  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 指定返回行数的数值表达式。 如果指定了 PERCENT，则 expression 将隐式转换为 float 值；否则，它将转换为 bigint。  
  
 PERCENT  
 指示查询只返回结果集中前 expression% 的行。 小数部分的值向上舍入到下一个整数值。  
  
 WITH TIES  
 当您希望返回与有限结果集中的最后一个位置相关联的两行或更多行时使用。 必须与 ORDER BY 子句一起使用。 WITH TIES 可能导致返回的行数多于在 expression 中指定的值。 例如，如果 expression 设置为 5，而 2 个其他行与第 5 行中 ORDER BY 列的值匹配，则结果集将包含 7 行。  
  
 只能在 SELECT 语句中且只有在指定了 ORDER BY 子句之后，才能指定 TOP...WITH TIES。 返回的记录关联顺序是任意的。 ORDER BY 不影响此规则。  
  
## <a name="best-practices"></a>最佳实践  
 在 SELECT 语句中，始终将 ORDER BY 子句与 TOP 语句结合使用。 这是以可预知的方式指明哪些行受 TOP 影响的唯一方法。  
  
 在 ORDER BY 子句中使用 OFFSET 和 FETCH，而不使用 TOP 子句，以实现查询分页解决方案。 使用 OFFSET 和 FETCH 子句更容易实现分页解决方案（也即，将数据块或页发送到客户端）。 有关详细信息，请参阅 [ORDER BY 子句 (Transact-SQL)](../../t-sql/queries/select-order-by-clause-transact-sql.md)。  
  
 使用 TOP（或 OFFSET 和 FETCH）而非 SET ROWCOUNT 限制返回的行数。 这些方法之所以优于使用 SET ROWCOUNT，原因包括以下各项：  
  
-   作为 SELECT 语句的一部分，查询优化器在查询优化期间可能会考虑 TOP 或 FETCH 子句中 expression 的值。 由于 SET ROWCOUNT 在执行查询的语句外使用，因此，在查询计划中不会考虑它的值。  
  
## <a name="compatibility-support"></a>兼容性支持  
 为了向后兼容，括号在 SELECT 语句中是可选的。 我们建议您始终对 SELECT 语句中的 TOP 使用括号，这样，就可以与在 INSERT、UPDATE、MERGE 和 DELETE 语句中需要使用括号保持一致（在这种情况下括号是必需的）。  
  
## <a name="interoperability"></a>互操作性  
 TOP 表达式不影响由于触发器而可能执行的语句。 触发器中 inserted 和 deleted 的表中将只显示确实受 INSERT、UPDATE、MERGE 或 DELETE 语句影响的那些行。 例如，INSERT TRIGGER 作为使用 TOP 子句的 INSERT 语句的结果而激发。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许通过视图更新行。 由于 TOP 子句可能包含在视图定义中，因此，如果更新后行不再符合 TOP 表达式的要求，则可能导致某些行从视图中消失。  
  
 在 MERGE 语句中指定 TOP 子句时，会在对整个源表和整个目标表进行联接且删除了不符合插入、更新或删除操作条件的联接行“之后”应用该子句。 TOP 子句将联接行的数量进一步减少为指定值，并且以一种无序方式对其余联接行应用插入、更新或删除操作。 也就是说，在 WHEN 子句中定义的操作中，这些行是无序分布的。 例如，如果指定 TOP (10)，将会影响 10 行；在这些行中，可能会更新 7 行而插入 3 行，或者可能删除 1 行、更新 5 行并且插入 4 行，等等。 由于 MERGE 语句对源表和目标表都进行完全表扫描，因此在使用 TOP 子句通过创建多个批处理来修改大型表时，I/O 性能可能会受到影响。 在这种情况下，一定要确保所有连续批处理都以新行作为处理目标。  
  
 在包含 UNION、UNION ALL、EXCEPT 或 INTERSECT 运算符的查询中指定 TOP 子句时，应特别小心。 此时可以编写一个返回意外结果的查询，因为当在选择操作中使用这些运算符时，以逻辑方式处理 TOP 和 ORDER BY 子句的顺序并不总是直观的。 例如，给定以下表和数据，假定您要返回最便宜的红色汽车和最便宜的蓝色汽车。 也就是红色的小轿车和蓝色的货车。  
  
```sql  
CREATE TABLE dbo.Cars(Model varchar(15), Price money, Color varchar(10));  
INSERT dbo.Cars VALUES  
    ('sedan', 10000, 'red'), ('convertible', 15000, 'blue'),   
    ('coupe', 20000, 'red'), ('van', 8000, 'blue');  
```  
  
 为了实现这些结果，您可能会编写以下查询。  
  
```sql  
SELECT TOP(1) Model, Color, Price  
FROM dbo.Cars  
WHERE Color = 'red'  
UNION ALL  
SELECT TOP(1) Model, Color, Price  
FROM dbo.Cars  
WHERE Color = 'blue'  
ORDER BY Price ASC;  
GO    
```  
  
 下面是结果集：  
  
 ```
 Model         Color      Price  
 ------------- ---------- -------  
 sedan         red        10000.00  
 convertible   blue       15000.00
 ```  
  
 此时可能返回意外结果，因为从逻辑上讲，会先执行 TOP 子句，然后执行 ORDER BY 子句，这会对运算符（在这种情况下为 UNION ALL）的结果进行排序。 因此，前一个查询返回任何一辆红色汽车和任何一辆蓝色汽车，然后按价格对该联合的结果排序。 下面的示例显示了编写此查询以获得所需结果的正确方法。  
  
```sql  
SELECT Model, Color, Price  
FROM (SELECT TOP(1) Model, Color, Price  
      FROM dbo.Cars  
      WHERE Color = 'red'  
      ORDER BY Price ASC) AS a  
UNION ALL  
SELECT Model, Color, Price  
FROM (SELECT TOP(1) Model, Color, Price  
      FROM dbo.Cars  
      WHERE Color = 'blue'  
      ORDER BY Price ASC) AS b;  
GO    
```  
  
 通过在嵌套 select 操作中使用 TOP 和 ORDER BY，可确保将 ORDER BY 子句的结果应用于 TOP 子句，而不对 UNION 运算的结果排序。  
  
 下面是结果集：  
  
 ```
 Model         Color      Price  
 ------------- ---------- -------  
 sedan         red        10000.00  
 van           blue        8000.00
 ```  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 在将 TOP 与 INSERT、UPDATE、MERGE 或 DELETE 结合使用时，被引用行不按任何顺序排列，不能直接在这些语句中指定 ORDER BY 子句。 如果需要使用 TOP 来插入、删除或修改按有意义的时间顺序排列的行，您必须同时使用 TOP 和在嵌套 select 语句中指定的 ORDER BY 子句。 请参阅本主题后面的“示例”一节。  
  
 在已分区视图中，不能在 UPDATE 和 DELETE 语句中使用 TOP。  
  
 TOP 不能与 OFFSET 和 FETCH 在同一个查询表达式（同一个查询作用域）中结合使用。 有关详细信息，请参阅 [ORDER BY 子句 (Transact-SQL)](../../t-sql/queries/select-order-by-clause-transact-sql.md)。  
  
## <a name="examples"></a>示例  
  
|类别|作为特征的语法元素|  
|--------------|------------------------------|  
|[基本语法](#BasicSyntax)|TOP • PERCENT|  
|[包括关联值](#tie)|WITH TIES|  
|[限制受 DELETE、INSERT 或 UPDATE 影响的行](#DML)|DELETE • INSERT • UPDATE|  
  
###  <a name="BasicSyntax"></a>基本语法  
 本节中的示例说明了使用最低要求的语法的 ORDER BY 子句的基本功能。  
  
#### <a name="a-using-top-with-a-constant-value"></a>A. 使用 TOP 以及一个常量值  
 下面的示例使用常量值以指定在查询结果集中返回的员工数。 在第一个示例中，返回前 10 个未定义的行，因为此时没有使用 ORDER BY 子句。 在第二个示例中，使用了 ORDER BY 子句来返回前 10 个最近雇用的员工。  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Select the first 10 random employees.  
SELECT TOP(10)JobTitle, HireDate  
FROM HumanResources.Employee;  
GO  
-- Select the first 10 employees hired most recently.  
SELECT TOP(10)JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY HireDate DESC;  
GO  
```  
  
#### <a name="b-using-top-with-a-variable"></a>B. 使用 TOP 以及一个变量  
 下面的示例使用变量以指定在查询结果集中返回的员工数。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @p AS int = 10;  
SELECT TOP(@p)JobTitle, HireDate, VacationHours  
FROM HumanResources.Employee  
ORDER BY VacationHours DESC;  
GO  
```  
  
#### <a name="c-specifying-a-percentage"></a>C. 指定百分比  
 下面的示例使用 PERCENT 以指定在查询结果集中返回的员工数。 `HumanResources.Employee` 表中有 290 名员工。 因为 290 的 5% 是一个小数值，因此将该值向上舍入为下一个整数。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TOP(5)PERCENT JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY HireDate DESC;  
GO    
```  
  
###  <a name="tie"></a>包括关联值  
  
#### <a name="a-using-with-ties-to-include-rows-that-match-the-values-in-the-last-row"></a>A. 使用 WITH TIES 以包含与最后一行中的值匹配的行  
 以下示例获取所有雇员中薪金最高的 `10` 个百分比的雇员，并根据其薪金按降序返回。 指定 `WITH TIES` 可确保结果集中同时包含其薪金与返回的最低薪金（最后一行）相同的所有雇员，即使这样做会超过雇员总数的 `10` 个百分比。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TOP(10)WITH TIES  
pp.FirstName, pp.LastName, e.JobTitle, e.Gender, r.Rate  
FROM Person.Person AS pp   
    INNER JOIN HumanResources.Employee AS e  
        ON pp.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeePayHistory AS r  
        ON r.BusinessEntityID = e.BusinessEntityID  
ORDER BY Rate DESC;  
GO    
```  
  
###  <a name="DML"></a>限制受 DELETE、INSERT 或 UPDATE 影响的行  
  
#### <a name="a-using-top-to-limit-the-number-of-rows-deleted"></a>A. 使用 TOP 限制删除的行数  
 当 TOP (*n*) 子句与 DELETE 结合使用，未定义所选内容上执行删除操作*n*的行数。 DELETE 语句，即选择任何 (*n*) 的满足 WHERE 子句中定义的条件的行数。 下面的示例从 `20` 表中删除其到期日期早于 2002 年 7 月 1 日的 `PurchaseOrderDetail` 行。  
  
```sql  
USE AdventureWorks2012;  
GO  
DELETE TOP (20)   
FROM Purchasing.PurchaseOrderDetail  
WHERE DueDate < '20020701';  
GO  
```  
  
 如果需要使用 TOP 来删除按有意义的时间顺序排列的行，您必须同时使用 TOP 和 ORDER BY 子句。 下面的查询从 `PurchaseOrderDetail` 表中删除了其到期日期最早的 10 行。 为了确保仅删除 10 行，嵌套 Select 语句 (`PurchaseOrderID`) 中指定的列将成为表的主键。 如果指定列包含重复的值，则在嵌套 Select 语句中使用非键列可能会导致删除的行超过 10 个。  
  
```sql  
USE AdventureWorks2012;  
GO  
DELETE FROM Purchasing.PurchaseOrderDetail  
WHERE PurchaseOrderDetailID IN  
   (SELECT TOP 10 PurchaseOrderDetailID   
    FROM Purchasing.PurchaseOrderDetail   
    ORDER BY DueDate ASC);  
GO  
```  
  
#### <a name="b-using-top-to-limit-the-number-of-rows-inserted"></a>B. 使用 TOP 限制插入的行数  
 以下示例创建 `EmployeeSales` 表，并插入 `HumanResources.Employee` 表中前 5 名员工的姓名和本年度到目前为止的销售数据。 INSERT 语句选择由满足 WHERE 子句所定义的条件的 `SELECT` 语句返回的任意 5 行。  OUTPUT 子句将显示插入 `EmployeeSales` 表中的行。 请注意，SELECT 语句中的 ORDER BY 子句不用于确定前 5 名雇员。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
IF OBJECT_ID ('dbo.EmployeeSales', 'U') IS NOT NULL  
    DROP TABLE dbo.EmployeeSales;  
GO  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   nvarchar(11) NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  YearlySales  money NOT NULL  
 );  
GO  
INSERT TOP(5)INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, inserted.LastName, inserted.YearlySales  
    SELECT sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
GO    
```  
  
 如果必须使用 TOP 来插入按有意义的时间顺序排列的行，您必须同时使用 TOP 和嵌套 select 语句中的 ORDER BY，如以下示例所示。 OUTPUT 子句将显示插入 `EmployeeSales` 表中的行。 请注意，现在基于 ORDER BY 子句的结果而非未定义的行插入前 5 名员工。  
  
```sql  
INSERT INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, inserted.LastName, inserted.YearlySales  
    SELECT TOP (5) sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
GO    
```  
  
#### <a name="c-using-top-to-limit-the-number-of-rows-updated"></a>C. 使用 TOP 限制更新的行数  
 以下示例使用 TOP 子句更新表中的行。 当 TOP (*n*) 子句用于更新，则更新操作执行的未定义的行号上。 UPDATE 语句，即选择任何 (*n*) 的满足 WHERE 子句中定义的条件的行数。 下列示例将 10 个客户从一位销售人员分配给了另一位。  
  
```sql  
USE AdventureWorks2012;  
UPDATE TOP (10) Sales.Store  
SET SalesPersonID = 276  
WHERE SalesPersonID = 275;  
GO  
```  
  
 如果需要使用 TOP 来应用按有意义的时间顺序排列的更新，您必须同时使用 TOP 和 ORDER BY 子句。 下列示例更新了雇佣最早的 10 名雇员的假期小时数。  
  
```sql  
UPDATE HumanResources.Employee  
SET VacationHours = VacationHours + 8  
FROM (SELECT TOP 10 BusinessEntityID FROM HumanResources.Employee  
     ORDER BY HireDate ASC) AS th  
WHERE HumanResources.Employee.BusinessEntityID = th.BusinessEntityID;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列示例将返回匹配查询条件的前 31 行。 使用 ORDER BY 子句可确保所返回的 31 行是按字母顺序排序的 `LastName` 列的前 31 行。  
  
 使用 TOP，且不指定关联。  
  
```sql  
SELECT TOP (31) FirstName, LastName   
FROM DimEmployee ORDER BY LastName;  
```  
  
 结果：返回 31 行。  
  
 使用 TOP，并指定 WITH TIES。  
  
```sql  
SELECT TOP (31) WITH TIES FirstName, LastName   
FROM DimEmployee ORDER BY LastName;  
```  
  
 结果：返回 33 行，因为名为 Brown 的 3 位员工与第 31 行相关联。  
  
## <a name="see-also"></a>另请参阅  
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)   
 [ORDER BY 子句 (Transact-SQL)](../../t-sql/queries/select-order-by-clause-transact-sql.md)   
 [SET ROWCOUNT (Transact-SQL)](../../t-sql/statements/set-rowcount-transact-sql.md)   
 [MERGE (Transact-SQL)](../../t-sql/statements/merge-transact-sql.md)  
  
 
