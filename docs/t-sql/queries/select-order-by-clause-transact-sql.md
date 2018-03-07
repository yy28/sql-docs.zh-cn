---
title: "ORDER BY 子句 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORDER_TSQL
- BY
- ORDER_BY_TSQL
- BY_TSQL
- ORDER
- ORDER BY
dev_langs:
- TSQL
helpviewer_keywords:
- ad-hoc query paging
- OFFSET clause
- SELECT statement [SQL Server], FETCH clause
- clauses [SQL Server], ORDER BY
- SELECT statement [SQL Server], limiting the rows returned
- data [SQL Server], limiting the rows returned
- data [SQL Server], ad-hoc query paging
- sort orders [SQL Server]
- SELECT statement [SQL Server], OFFSET clause
- ORDER BY clause [Transact-SQL]
- LIMIT
- limiting result sets
- SELECT statement [SQL Server], ORDER BY clause
- query paging
- data [SQL Server], sorting
- limiting data returned in a query
- sort orders [SQL Server], ORDER BY clause
- FETCH clause
ms.assetid: bb394abe-cae6-4905-b5c6-8daaded77742
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 08805ce7f01b11d9b87c587e543f5dae91734e68
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="select---order-by-clause-transact-sql"></a>SELECT-ORDER BY 子句 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的查询返回的数据进行排序。 可以使用此子句执行以下操作：  
  
-   按指定的列列表对查询的结果集进行排序，并有选择地将返回的行限制为指定范围。 除非指定 ORDER BY 子句，否则，不能保证在结果集中返回的行的顺序。  
  
-   确定的顺序[排名函数](../../t-sql/functions/ranking-functions-transact-sql.md)值应用到结果集。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!NOTE]  
>  在选择 / 到不支持按顺序或中的创建表 AS SELECT (CTAS) 语句[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。

## <a name="syntax"></a>语法  
  
```sql  
-- Syntax for SQL Server and Azure SQL Database  
  
ORDER BY order_by_expression  
    [ COLLATE collation_name ]   
    [ ASC | DESC ]   
    [ ,...n ]   
[ <offset_fetch> ]  
  
<offset_fetch> ::=  
{   
    OFFSET { integer_constant | offset_row_count_expression } { ROW | ROWS }  
    [  
      FETCH { FIRST | NEXT } {integer_constant | fetch_row_count_expression } { ROW | ROWS } ONLY  
    ]  
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[ ORDER BY   
    {  
    order_by_expression   
    [ ASC | DESC ]   
    } [ ,...n ]   
]   
```  
  
## <a name="arguments"></a>参数  
 *order_by_expression*  
 指定用于对查询结果集进行排序的列或表达式。 可以将排序列指定为一个名称或列别名，也可以指定一个表示列在选择列表中所处位置的非负整数。  
  
 可以指定多个排序列。 别名必须是唯一的。 ORDER BY 子句中的排序列的顺序定义了排序结果集的结构。 也就是说，按第一列对结果集进行排序，然后按第二列对排序列表进行排序，依此类推。  
  
 ORDER BY 子句中引用的列名必须明确对应于选择列表中的列，或对应于 FROM 子句中指定的表中定义的列。  
  
 COLLATE *collation_name*  
 指定应根据在指定的排序规则执行 ORDER BY 运算*collation_name*，并不根据列的表或视图中定义的排序规则。 *collation_name*可以是 Windows 排序规则名称或 SQL 排序规则名称。 有关详细信息，请参阅 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。 COLLATE 是仅适用于类型的列**char**， **varchar**， **nchar**，和**nvarchar**。  
  
 **ASC** | DESC  
 指定按升序或降序排列指定列中的值。 ASC 按从最低值到最高值的顺序进行排序。 DESC 按从最高值到最低值的顺序进行排序。 ASC 是默认排序顺序。 Null 值被视为最低的可能值。  
  
 OFFSET { *integer_constant* | *offset_row_count_expression* } { ROW | ROWS }  
 指定开始从查询表达式返回行之前跳过的行数。 该值可以是大于或等于零的整数常量或表达式。  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].s 来进行  
  
 *offset_row_count_expression*可以是变量、 参数或常量标量子查询。 在使用子查询时，它无法引用在外部查询范围中定义的任何列。 也就是说，它无法与外部查询相关联。  
  
 ROW 和 ROWS 是同义词，是为了与 ANSI 兼容而提供的。  
  
 在查询执行计划的偏移量的行计数值显示在**偏移量**TOP 查询运算符的属性。  
  
 FETCH { FIRST | NEXT } { *integer_constant* | *fetch_row_count_expression* } { ROW | ROWS } ONLY  
 指定在处理 OFFSET 子句后返回的行数。 该值可以是大于或等于 1 的整数常量或表达式。  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 *fetch_row_count_expression*可以是变量、 参数或常量标量子查询。 在使用子查询时，它无法引用在外部查询范围中定义的任何列。 也就是说，它无法与外部查询相关联。  
  
 FIRST 和 NEXT 是同义词，是为了与 ANSI 兼容而提供的。  
  
 ROW 和 ROWS 是同义词，是为了与 ANSI 兼容而提供的。  
  
 在查询执行计划的偏移量的行计数值显示在**行**或**顶部**TOP 查询运算符的属性。  
  
## <a name="best-practices"></a>最佳实践  
 避免将 ORDER BY 子句中的整数指定为选择列表中的列位置表示形式 例如，虽然 `SELECT ProductID, Name FROM Production.Production ORDER BY 2` 等语句是有效的，但与指定实际列名相比，其他人并不容易理解该语句。 此外，对选择列表中，如更改列顺序更改或添加新列，则需要修改 ORDER BY 子句，以避免意外的结果。  
  
 在选择前 (*N*) 语句，始终使用 ORDER BY 子句。 这是以可预知的方式指明哪些行受 TOP 影响的唯一方法。 有关详细信息，请参阅[顶部 &#40;Transact SQL &#41;](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="interoperability"></a>互操作性  
 在与 SELECT…INTO 语句一起使用以从另一来源插入行时，ORDER BY 子句不能保证按指定的顺序插入这些行。  
  
 在视图中使用 OFFSET 和 FETCH 并不会更改该视图的 Updateability 属性。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 ORDER BY 子句中的列数没有限制；但是，在 ORDER BY 子句中指定的列的总大小不能超过 8,060 个字节。  
  
 类型的列**ntext**，**文本**，**映像**， **geography**，**几何图形**，和**xml**不能在 ORDER BY 子句。  
  
 不能为整数或常量时指定*order_by_expression*出现在排名函数。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 如果已在 FROM 子句中指定了表名的别名，则在 ORDER BY 子句中只能使用该别名来限定其列。  
  
 如果 SELECT 语句包含以下子句或运算符之一，则必须在选择列表中定义在 ORDER BY 子句中指定的列名和别名：  
  
-   UNION 运算符  
  
-   EXCEPT 运算符  
  
-   INTERSECT 运算符  
  
-   SELECT DISTINCT  
  
 此外，当语句中包含联合，除外，也 INTERSECT 运算符、 列名称或列别名必须指定第一个 （左侧） 查询选择列表中。  
  
 在使用 UNION、EXCEPT 或 INTERSECT 运算符的查询中，只允许在语句末尾使用 ORDER BY。 此限制仅适用于你指定两个联合，除外、 时和 INTERSECT 顶级查询中，不能在子查询。 请参阅后面的“示例”一节。  
  
 除非还指定了 TOP 子句或 OFFSET 和 FETCH 子句，否则，视图、内联函数、派生表和子查询中的 ORDER BY 子句无效。 在这些对象中使用 ORDER BY 时，该子句仅用于确定由 TOP 子句或 OFFSET 和 FETCH 子句返回的行。 ORDER BY 不保证在查询这些构造时得到有序结果，除非在查询本身中也指定了 ORDER BY。  
  
 索引视图或使用 CHECK OPTION 子句定义的视图中不支持 OFFSET 和 FETCH。  
  
 可以在允许 TOP 和 ORDER BY 的任何查询中使用 OFFSET 和 FETCH，但具有以下限制：  
  
-   OVER 子句不支持 OFFSET 和 FETCH。  
  
-   无法在 INSERT、UPDATE、MERGE 和 DELETE 语句中直接指定 OFFSET 和 FETCH，但可以在这些语句定义的子查询中指定 OFFSET 和 FETCH。 例如，在 INSERT INTO SELECT 语句中，可以在 SELECT 语句中指定 OFFSET 和 FETCH。  
  
-   在使用 UNION、EXCEPT 或 INTERSECT 运算符的查询中，只能在指定查询结果顺序的最终查询中指定 OFFSET 和 FETCH。  
  
-   TOP 不能与 OFFSET 和 FETCH 在同一个查询表达式（同一个查询作用域）中结合使用。  
  
## <a name="using-offset-and-fetch-to-limit-the-rows-returned"></a>使用 OFFSET 和 FETCH 限制返回的行数  
 建议您使用 OFFSET 和 FETCH 子句而不是 TOP 子句实现查询分页解决方案，并限制发送到客户端应用程序的行数。  
  
 如果将 OFFSET 和 FETCH 作为分页解决方案，则需要为返回到客户端应用程序的每“页”数据运行一次查询。 例如，要以 10 行为增量返回查询结果，您必须执行一次查询以返回 1-10 行，然后再次运行查询以返回 11- 20 行，依此类推。 每个查询都是独立的，不会以任何方式与其他查询相关联。 这意味着，与使用执行一次查询并在服务器上保持状态的游标不同，将由客户端应用程序负责跟踪状态。 若要使用 OFFSET 和 FETCH 在查询请求之间获得稳定的结果，必须满足以下条件：  
  
1.  查询使用的基础数据不能发生变化。 即，不会更新查询处理的行，也不会在单个事务中使用快照或可序列化事务隔离执行查询中的所有页面请求。 有关这些事务隔离级别的详细信息，请参阅[SET TRANSACTION ISOLATION LEVEL &#40;Transact SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
2.  ORDER BY 子句包含保证是唯一的列或列组合。  
  
 请参阅本主题后面的“示例”部分中的“在单个事务中运行多个查询”示例。  
  
 如果一致的执行计划在分页解决方案中至关重要，应考虑使用 OFFSET 和 FETCH 参数的 OPTIMIZE FOR 查询提示。 请参阅本主题后面的“示例”部分中的“指定 OFFSET 和 FETCH 值的表达式”。 有关 OPTIMZE 有关的详细信息，请参阅[查询提示 &#40;Transact SQL &#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="examples"></a>示例  
  
|类别|作为特征的语法元素|  
|--------------|------------------------------|  
|[基本语法](#BasicSyntax)|ORDER BY|  
|[指定升序和降序顺序](#SortOrder)|DESC • ASC|  
|[指定的排序规则](#Collation)|COLLATE|  
|[指定条件的顺序](#Case)|CASE 表达式|  
|[使用 ORDER BY 中排名函数](#Rank)|排名函数|  
|[限制返回的行数](#Offset)|OFFSET • FETCH|  
|[使用联合的 ORDER BY，除非和 INTERSECT](#Union)|UNION|  
  
###  <a name="BasicSyntax"></a>基本语法  
 本节中的示例说明了使用最低要求的语法的 ORDER BY 子句的基本功能。  
  
#### <a name="a-specifying-a-single-column-defined-in-the-select-list"></a>A. 指定在选择列表中定义的单个列  
 以下示例按数值 `ProductID` 列对结果集进行顺序。 由于未指定特定的排序顺序，将使用默认顺序（升序）。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY ProductID;  
```  
  
#### <a name="b-specifying-a-column-that-is-not-defined-in-the-select-list"></a>B. 指定未在选择列表中定义的列  
 以下示例按未包含在选择列表中的列对结果集进行排序，但 FROM 子句中指定的表中定义了该列。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
ORDER BY ListPrice;  
  
```  
  
#### <a name="c-specifying-an-alias-as-the-sort-column"></a>C. 将别名指定为排序列  
 以下示例将列别名 `SchemaName` 指定为排序顺序列。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT name, SCHEMA_NAME(schema_id) AS SchemaName  
FROM sys.objects  
WHERE type = 'U'  
ORDER BY SchemaName;  
  
```  
  
#### <a name="d-specifying-an-expression-as-the-sort-column"></a>D. 将表达式指定为排序列  
 以下示例将表达式作为排序列。 表达式是使用 DATEPART 函数定义的，以便按员工的雇用年份对结果集进行排序。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY DATEPART(year, HireDate);  
  
```  
  
###  <a name="SortOrder"></a>指定的升序和降序排序  
  
#### <a name="a-specifying-a-descending-order"></a>A. 指定降序  
 以下示例按 `ProductID` 数值列降序对结果集进行排序。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY ProductID DESC;  
  
```  
  
#### <a name="b-specifying-an-ascending-order"></a>B. 指定按升序进行排序  
 以下示例按 `Name` 列升序对结果集进行排序。 字符进行排序，按字母顺序、 不按数字顺序。 也就是说，10 排在 2 之前。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY Name ASC ;  
  
```  
  
#### <a name="c-specifying-both-ascending-and-descending-order"></a>C. 同时指定升序和降序  
 以下示例按两个列对结果集进行排序。 先按 `FirstName` 列升序对查询结果集进行排序，然后按 `LastName` 列降序进行排序。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT LastName, FirstName FROM Person.Person  
WHERE LastName LIKE 'R%'  
ORDER BY FirstName ASC, LastName DESC ;  
  
```  
  
###  <a name="Collation"></a>指定的排序规则  
 以下示例说明如何在 ORDER BY 子句中指定排序规则以更改查询结果的返回顺序。 将创建一个表，其中包含一个使用不区分大小写和重音的排序规则定义的列。 插入一些具有不同大小写和重音的值。 由于未在 ORDER BY 子句中指定排序规则，在对值进行排序时，第一个查询将使用列排序规则。 在第二个查询中，在 ORDER BY 子句中指定了区分大小写和重音的排序规则，这将改变行的返回顺序。  
  
```  
USE tempdb;  
GO  
CREATE TABLE #t1 (name nvarchar(15) COLLATE Latin1_General_CI_AI)  
GO  
INSERT INTO #t1 VALUES(N'Sánchez'),(N'Sanchez'),(N'sánchez'),(N'sanchez');  
  
-- This query uses the collation specified for the column 'name' for sorting.  
SELECT name  
FROM #t1  
ORDER BY name;  
-- This query uses the collation specified in the ORDER BY clause for sorting.  
SELECT name  
FROM #t1  
ORDER BY name COLLATE Latin1_General_CS_AS;  
  
```  
  
###  <a name="Case"></a>指定条件的顺序  
 下面的示例在 ORDER BY 子句中使用 CASE 表达式，来有条件地确定基于给定的列的值的行的排序顺序。 在第一个示例中，会计算 `SalariedFlag` 表中 `HumanResources.Employee` 列的值。 `SalariedFlag` 设置为 1 的员工将按 `BusinessEntityID` 以降序顺序返回。 `SalariedFlag` 设置为 0 的员工将按 `BusinessEntityID` 以升序顺序返回。 在第二个示例中，当 `TerritoryName` 列等于“United States”时，结果集会按 `CountryRegionName` 列排序，对于所有其他行则按 `CountryRegionName` 排序。  
  
```  
SELECT BusinessEntityID, SalariedFlag  
FROM HumanResources.Employee  
ORDER BY CASE SalariedFlag WHEN 1 THEN BusinessEntityID END DESC  
        ,CASE WHEN SalariedFlag = 0 THEN BusinessEntityID END;  
GO  
  
```  
  
```  
SELECT BusinessEntityID, LastName, TerritoryName, CountryRegionName  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL  
ORDER BY CASE CountryRegionName WHEN 'United States' THEN TerritoryName  
         ELSE CountryRegionName END;  
  
```  
  
###  <a name="Rank"></a>使用 ORDER BY 中排名函数  
 以下示例在 ROW_NUMBER、RANK、DENSE_RANK 和 NTILE 排名函数中使用 ORDER BY 子句。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,ROW_NUMBER() OVER (ORDER BY a.PostalCode) AS "Row Number"  
    ,RANK() OVER (ORDER BY a.PostalCode) AS "Rank"  
    ,DENSE_RANK() OVER (ORDER BY a.PostalCode) AS "Dense Rank"  
    ,NTILE(4) OVER (ORDER BY a.PostalCode) AS "Quartile"  
    ,s.SalesYTD, a.PostalCode  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL AND SalesYTD <> 0;  
  
```  
  
###  <a name="Offset"></a>限制返回的行数  
 以下示例使用 OFFSET 和 FETCH 限制查询返回的行数。  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
#### <a name="a-specifying-integer-constants-for-offset-and-fetch-values"></a>A. 指定整数常量以提供 OFFSET 和 FETCH 值  
 以下示例将一个整数常量指定为 OFFSET 和 FETCH 子句的值。 第一个查询返回所有按 `DepartmentID` 列排序的行。 将此查询返回的结果与后面的两个查询的结果进行比较。 下一个查询使用 `OFFSET 5 ROWS` 子句跳过前 5 行，然后返回所有其余行。 最终查询使用 `OFFSET 0 ROWS` 子句从第一行开始，然后使用 `FETCH NEXT 10 ROWS ONLY` 将返回的行限制为排序的结果集中的 10 行。  
  
```  
USE AdventureWorks2012;  
GO  
-- Return all rows sorted by the column DepartmentID.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID;  
  
-- Skip the first 5 rows from the sorted result set and return all remaining rows.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID OFFSET 5 ROWS;  
  
-- Skip 0 rows and return only the first 10 rows from the sorted result set.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID   
    OFFSET 0 ROWS  
    FETCH NEXT 10 ROWS ONLY;  
  
```  
  
#### <a name="b-specifying-variables-for-offset-and-fetch-values"></a>B. 指定变量以提供 OFFSET 和 FETCH 值  
 下面的示例声明 `@StartingRowNumber` 和 `@FetchRows` 变量，并在 OFFSET 和 FETCH 子句中指定这些变量。  
  
```  
USE AdventureWorks2012;  
GO  
-- Specifying variables for OFFSET and FETCH values    
DECLARE @StartingRowNumber tinyint = 1  
      , @FetchRows tinyint = 8;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber ROWS   
    FETCH NEXT @FetchRows ROWS ONLY;  
  
```  
  
#### <a name="c-specifying-expressions-for-offset-and-fetch-values"></a>C. 指定表达式以提供 OFFSET 和 FETCH 值  
 下面的示例使用 `@StartingRowNumber - 1` 表达式指定 OFFSET 值，并使用 `@EndingRowNumber - @StartingRowNumber + 1` 表达式指定 FETCH 值。 另外，还指定了查询提示 OPTIMIZE FOR。 在编译和优化查询时，可以使用此提示为局部变量提供特定的值。 仅在查询优化期间使用该值，在查询执行期间不使用该值。 有关详细信息，请参阅[查询提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-query.md)。  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Specifying expressions for OFFSET and FETCH values      
DECLARE @StartingRowNumber tinyint = 1  
      , @EndingRowNumber tinyint = 8;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber - 1 ROWS   
    FETCH NEXT @EndingRowNumber - @StartingRowNumber + 1 ROWS ONLY  
OPTION ( OPTIMIZE FOR (@StartingRowNumber = 1, @EndingRowNumber = 20) );  
  
```  
  
#### <a name="d-specifying-a-constant-scalar-subquery-for-offset-and-fetch-values"></a>D. 指定常数标量子查询以提供 OFFSET 和 FETCH 值  
 以下示例使用常数标量子查询定义 FETCH 子句的值。 该子查询从 `PageSize` 表的 `dbo.AppSettings` 列中返回单个值。  
  
```  
-- Specifying a constant scalar subquery  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.AppSettings (AppSettingID int NOT NULL, PageSize int NOT NULL);  
GO  
INSERT INTO dbo.AppSettings VALUES(1, 10);  
GO  
DECLARE @StartingRowNumber tinyint = 1;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber ROWS   
    FETCH NEXT (SELECT PageSize FROM dbo.AppSettings WHERE AppSettingID = 1) ROWS ONLY;  
  
```  
  
#### <a name="e-running-multiple-queries-in-a-single-transaction"></a>E. 在单个事务中运行多个查询  
 以下示例说明一种实现分页解决方案的方法，以确保在查询的所有请求中返回稳定的结果。 在单个事务使用快照隔离级别，执行查询和 ORDER BY 子句中指定的列可确保列唯一性。  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Ensure the database can support the snapshot isolation level set for the query.  
IF (SELECT snapshot_isolation_state FROM sys.databases WHERE name = N'AdventureWorks2012') = 0  
    ALTER DATABASE AdventureWorks2012 SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
  
-- Set the transaction isolation level  to SNAPSHOT for this query.  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
  
-- Beging the transaction  
BEGIN TRANSACTION;  
GO  
-- Declare and set the variables for the OFFSET and FETCH values.  
DECLARE @StartingRowNumber int = 1  
      , @RowCountPerPage int = 3;  
  
-- Create the condition to stop the transaction after all rows have been returned.  
WHILE (SELECT COUNT(*) FROM HumanResources.Department) >= @StartingRowNumber  
BEGIN  
  
-- Run the query until the stop condition is met.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber - 1 ROWS   
    FETCH NEXT @RowCountPerPage ROWS ONLY;  
  
-- Increment @StartingRowNumber value.  
SET @StartingRowNumber = @StartingRowNumber + @RowCountPerPage;  
CONTINUE  
END;  
GO  
COMMIT TRANSACTION;  
GO  
  
```  
  
###  <a name="Union"></a>使用联合的 ORDER BY，除非和 INTERSECT  
 当查询使用 UNION、EXCEPT 或 INTERSECT 运算符时，必须在语句末尾指定 ORDER BY 子句，并对合并的查询结果进行排序。 以下示例返回所有红色或黄色的产品，并按 `ListPrice` 列对合并的列表进行排序。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Color, ListPrice  
FROM Production.Product  
WHERE Color = 'Red'  
-- ORDER BY cannot be specified here.  
UNION ALL  
SELECT Name, Color, ListPrice  
FROM Production.Product  
WHERE Color = 'Yellow'  
ORDER BY ListPrice ASC;  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例演示排序结果集通过数字`EmployeeKey`升序排序的列。  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY EmployeeKey;  
```  
  
 下面的示例进行排序的结果集通过数字`EmployeeKey`降序排序的列。  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY EmployeeKey DESC;  
```  
  
 下面的示例进行排序的结果集`LastName`列。  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY LastName;  
```  
  
 按两列下面的示例订单。 此查询首先按升序进行排序的`FirstName`列，然后排序常见`FirstName`值以降序排序依据`LastName`列。  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY LastName, FirstName;  
```  
  
## <a name="see-also"></a>另请参阅  
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [排名函数 &#40;Transact SQL &#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [顶部 &#40;Transact SQL &#41;](../../t-sql/queries/top-transact-sql.md)   
 [查询提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-query.md)   
 [除和 INTERSECT &#40;Transact SQL &#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [联合 &#40;Transact SQL &#41;](../../t-sql/language-elements/set-operators-union-transact-sql.md)   
 [CASE (Transact-SQL)](../../t-sql/language-elements/case-transact-sql.md)  
  
  

