---
title: "table (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table data type [SQL Server]
- table variables [SQL Server]
ms.assetid: 1ef0b60e-a64c-4e97-847b-67930e3973ef
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b22ecfa04f949af77df974abc3359b7bc5144a82
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="table-transact-sql"></a>表 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

一种特殊的数据类型，可用于存储结果集以进行后续处理。 **表**主要用于临时存储的一组作为表值函数的结果集返回的行。 声明函数和变量的类型为**表**。 **表**变量可在函数、 存储的过程和批处理。 若要声明类型的变量**表**，使用[DECLARE @local_variable ](../../t-sql/language-elements/declare-local-variable-transact-sql.md)。
  

**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
table_type_definition ::=   
    TABLE ( { <column_definition> | <table_constraint> } [ ,...n ] )   
  
<column_definition> ::=   
    column_name scalar_data_type   
    [ COLLATE <collation_definition> ]   
    [ [ DEFAULT constant_expression ] | IDENTITY [ ( seed , increment ) ] ]   
    [ ROWGUIDCOL ]   
    [ column_constraint ] [ ...n ]   
  
 <column_constraint> ::=   
    { [ NULL | NOT NULL ]   
    | [ PRIMARY KEY | UNIQUE ]   
    | CHECK ( logical_expression )   
    }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n ] )  
     | CHECK ( logical_expression )   
     }   
```  
  
## <a name="arguments"></a>参数  
*table_type_definition*  
与在 CREATE TABLE 中定义表时所用的信息子集相同的信息子集。 表声明包括列定义、名称、数据类型和约束。 允许的约束类型仅为 PRIMARY KEY、UNIQUE KEY 和 NULL。  
有关语法的详细信息，请参阅[CREATE TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql.md)，[创建函数 &#40;Transact SQL &#41;](../../t-sql/statements/create-function-transact-sql.md)，和[DECLARE @local_variable &#40;Transact SQL &#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  
*collation_definition*  
是组成的列的排序规则[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 区域设置和比较样式、 Windows 区域设置和二进制表示法，或[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]排序规则。 如果*collation_definition*未指定，则该列继承当前数据库的排序规则。 另外，如果将此列定义为公共语言运行时 (CLR) 用户定义类型，则它将继承用户定义类型的排序规则。
  
## <a name="remarks"></a>注释  
**表**可以按一批的 FROM 子句中的名称引用变量，如下面的示例所示：
  
```sql
SELECT Employee_ID, Department_ID FROM @MyTableVar;  
```  
  
FROM 子句，外部**表**必须使用一个别名，来引用变量，如下面的示例中所示：
  
```sql
SELECT EmployeeID, DepartmentID   
FROM @MyTableVar m  
JOIN Employee on (m.EmployeeID =Employee.EmployeeID AND  
   m.DepartmentID = Employee.DepartmentID);  
```  
  
**表**变量具有查询计划不会更改和重新编译问题何时主导的小规模查询提供了以下好处：
-   A**表**变量行为类似于本地变量。 有明确定义的作用域。 这就是在其中声明该变量的函数、存储过程或批处理。  
     在其范围内，**表**可像常规表中使用变量。 该变量可应用于 SELECT、INSERT、UPDATE 和 DELETE 语句中用到表或表的表达式的任何地方。 但是，**表**不能在以下语句：  
  
```sql
SELECT select_list INTO table_variable;
```
  
**表**会自动将变量清除末尾的函数、 存储的过程或在其中定义的批处理。
  
-   **表**存储过程中使用的变量会导致比时不会影响性能的基于开销的选项，当使用临时表较少的存储过程的重新编译。  
-   事务涉及**表**变量仅用于更新期间上次上**表**变量。 因此，**表**变量所需的小于锁定和日志记录资源。  
  
## <a name="limitations-and-restrictions"></a>限制和局限
**表**变量不具有分发统计信息，它们不会触发重新编译。 因此，在许多情况下，优化器会在假定 table 变量没有行的前提下生成查询计划。 出于这一原因，如果您预计会存在大量行（超过 100 行），那么在使用 table 变量时应小心谨慎。 这种情况下，使用临时表可能是更好的解决方案。 或者，对于加入与其他表的表变量的查询，使用 RECOMPILE 提示，这将导致优化器为表变量使用正确的基数。
  
**表**中不支持变量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]优化器的基于开销的推理模型。 因此，在需要基于成本的选择来实现高效的查询计划时，不应使用这些变量。 在需要基于成本的选择时，临时表是首选。 这通常包含具有联接、并行度决策和索引选择选项的查询。
  
修改的查询**表**变量不会生成并行查询执行计划。 时非常大，可能会影响性能**表**变量，或**表**复杂的查询中的变量进行修改。 在这种情况下，请考虑改用临时表。 有关详细信息，请参阅 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)。 读取的查询**表**仍可并行化变量，而不修改它们。
  
不能显式上创建索引**表**变量和任何统计信息保存在**表**变量。 在某些情况下，可以通过改用支持索引和统计信息的临时表来改善性能。 有关临时表的详细信息，请参阅[CREATE TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).
  
请检查约束、 默认值和计算的列中**表**类型声明不能调用用户定义的函数。
  
之间进行赋值操作**表**不支持变量。
  
因为**表**变量具有有限的范围，并不是持久的数据库的一部分，它们不受事务回滚。
  
表变量在创建后就无法更改。
  
## <a name="examples"></a>示例  
  
### <a name="a-declaring-a-variable-of-type-table"></a>A. 声明一个表类型的变量  
下例将创建一个 `table` 变量，用于储存 UPDATE 语句的 OUTPUT 子句中指定的值。 在它后面的两个 `SELECT` 语句返回 `@MyTableVar` 中的值以及 `Employee` 表中更新操作的结果。 请注意，中的结果`INSERTED.ModifiedDate`列与中的值不同`ModifiedDate`中的列`Employee`表。 这是因为对 `AFTER UPDATE` 表定义了 `ModifiedDate` 触发器，该触发器可以将 `Employee` 的值更新为当前日期。 不过，从 `OUTPUT` 返回的列可反映触发器激发之前的数据。 有关详细信息，请参阅[OUTPUT 子句 &#40;Transact SQL &#41;](../../t-sql/queries/output-clause-transact-sql.md).
  
```sql
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25   
OUTPUT INSERTED.BusinessEntityID,  
       DELETED.VacationHours,  
       INSERTED.VacationHours,  
       INSERTED.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
--Note that ModifiedDate reflects the value generated by an  
--AFTER UPDATE trigger.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. 创建内联表值函数  
下面的示例将返回内联表值函数。 它返回三列`ProductID`，`Name`和由存储为年度截止到现在总计的聚合`YTD Total`的形式销售给存储每个产品。
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```  
  
若要调用该函数，请运行此查询。
  
```sql
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
## <a name="see-also"></a>另请参阅
[COLLATE &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)  
[用户定义函数](../../relational-databases/user-defined-functions/user-defined-functions.md)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[使用表值参数 &#40; 数据库引擎 &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
[查询提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-query.md)
  
  

