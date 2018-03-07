---
title: "与 common_table_expression (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2017
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
- WITH common_table_expression
- WITH_TSQL
- WITH
- common table expression
dev_langs:
- TSQL
helpviewer_keywords:
- WITH common_table_expression clause
- CTEs
- hierarchical queries [SQL Server], WITH common_table_expression
- recursive CTEs [SQL Server]
- recursive queries [SQL Server]
- common table expressions
- MAXRECURSION hint
- clauses [SQL Server], WITH common_table_expression
ms.assetid: 27cfb819-3e8d-4274-8bbe-cbbe4d9c2e23
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8c77e9c97fd3d31b63e6e3938cbdab134554dd1c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="with-commontableexpression-transact-sql"></a>WITH common_table_expression (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定临时命名的结果集，这些结果集称为公用表表达式 (CTE)。 该表达式源自简单查询，并且在单条 SELECT、INSERT、UPDATE 或 DELETE 语句的执行范围内定义。 该子句也可用在 CREATE VIEW 语句中，作为该语句的 SELECT 定义语句的一部分。 公用表表达式可以包括对自身的引用。 这种表达式称为递归公用表表达式。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
[ WITH <common_table_expression> [ ,...n ] ]  
  
<common_table_expression>::=  
    expression_name [ ( column_name [ ,...n ] ) ]  
    AS  
    ( CTE_query_definition )  
```  
  
## <a name="arguments"></a>参数  
 *expression_name*  
是公用表表达式的有效标识符。 *expression_name*必须与任何其他公用表表达式在相同 WITH 中定义的名称不同\<common_table_expression > 子句，但*expression_name*可以是相同的名称基表或视图。 任何引用*expression_name*在查询中使用公用表表达式和不是基对象。
  
 column_name  
 在公用表表达式中指定列名。 在一个 CTE 定义中不允许出现重复的名称。 指定的列名称的数量必须与匹配的结果集中的列数*CTE_query_definition*。 只有在查询定义中为所有结果列都提供了不同的名称时，列名列表才是可选的。  
  
 *CTE_query_definition*  
 指定一个其结果集填充公用表表达式的 SELECT 语句。 SELECT 语句，以*CTE_query_definition*必须满足与创建视图，但 CTE 不能定义另一个 CTE 相同的要求。 有关详细信息，请参阅备注部分和[创建的视图 &#40;Transact SQL &#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
 如果多个*CTE_query_definition*是定义，查询定义必须通过联接其中一种集运算符： UNION ALL、 UNION、 EXCEPT 或 INTERSECT。  
  
## <a name="remarks"></a>注释  
  
## <a name="guidelines-for-creating-and-using-common-table-expressions"></a>创建和使用公用表表达式的准则  
 下面的准则适用于非递归公用表表达式。 有关适用于递归公用表表达式的准则，请参阅后面的“定义和使用递归公用表表达式的准则”。  
  
-   CTE 之后必须跟随引用部分或全部 CTE 列的单条 SELECT、INSERT、UPDATE 或 DELETE 语句。 也可以在 CREATE VIEW 语句中将 CTE 指定为视图中 SELECT 定义语句的一部分。  
  
-   可以在非递归 CTE 中定义多个 CTE 查询定义。 定义必须与以下集合运算符之一结合使用：UNION ALL、UNION、INTERSECT 或 EXCEPT。  
  
-   CTE 可以引用自身，也可以引用在同一 WITH 子句中预先定义的 CTE。 不允许前向引用。  
  
-   不允许在一个 CTE 中指定多个 WITH 子句。 例如，如果*CTE_query_definition*包含子查询，该子查询不能包含嵌套带有定义另一个 CTE 的子句。  
  
-   不能用于以下子句*CTE_query_definition*:  
  
    -   ORDER BY（除非指定了 TOP 子句）  
  
    -   INTO  
  
    -   带有查询提示的 OPTION 子句  
  
    -   FOR BROWSE  
  
-   如果将 CTE 用在属于批处理的一部分的语句中，那么在它之前的语句必须以分号结尾。  
  
-   可以使用引用 CTE 的查询来定义游标。  
  
-   可以在 CTE 引用远程服务器上的表。  
  
-   在执行 CTE 时，任何引用 CTE 的提示都可能与该 CTE 访问其基础表时发现的其他提示相冲突，这种冲突与引用查询中的视图的提示所发生的冲突相同。 发生这种情况时，查询将返回错误。  
  
## <a name="guidelines-for-defining-and-using-recursive-common-table-expressions"></a>定义和使用递归公用表表达式的准则  
 下面的准则适用于定义递归公用表表达式：  
  
-   递归 CTE 定义至少必须包含两个 CTE 查询定义，一个定位点成员和一个递归成员。 可以定义多个定位点成员和递归成员；但必须将所有定位点成员查询定义置于第一个递归成员定义之前。 所有 CTE 查询定义都是定位点成员，但它们引用 CTE 本身时除外。  
  
-   定位点成员必须与以下集合运算符之一结合使用：UNION ALL、UNION、INTERSECT 或 EXCEPT。 在最后一个定位点成员和第一个递归成员之间，以及组合多个递归成员时，只能使用 UNION ALL 集合运算符。  
  
-   定位点成员和递归成员中的列数必须一致。  
  
-   递归成员中列的数据类型必须与定位点成员中相应列的数据类型一致。  
  
-   FROM 子句的递归成员必须引用一次 CTE *expression_name*。  
  
-   中不允许以下各项*CTE_query_definition*的递归成员：  
  
    -   SELECT DISTINCT  
  
    -   GROUP BY  
  
    -   PIVOT（当数据库兼容级别为 110 或更高级别时。 请参阅[中 SQL Server 2016 数据库引擎功能的重大更改](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。)  
  
    -   HAVING  
  
    -   标量聚合  
  
    -   返回页首  
  
    -   LEFT、RIGHT、OUTER JOIN（允许出现 INNER JOIN）  
  
    -   子查询  
  
    -   提示应用于对内部 CTE 的递归引用*CTE_query_definition*。  
  
 下面的准则适用于使用递归公用表表达式：  
  
-   无论参与的 SELECT 语句返回的列的为 Null 性如何，递归 CTE 返回的全部列都可以为空。  
  
-   如果递归 CTE 组合不正确，可能会导致无限循环。 例如，如果递归成员查询定义对父列和子列返回相同的值，则会造成无限循环。 可以使用 MAXRECURSION 提示以及在 INSERT、UPDATE、DELETE 或 SELECT 语句的 OPTION 子句中的一个 0 到 32,767 之间的值，来限制特定语句所允许的递归级数，以防止出现无限循环。 这样就能够在解决产生循环的代码问题之前控制语句的执行。 服务器范围的默认值为 100。 如果指定 0，则没有限制。 每一个语句只能指定一个 MAXRECURSION 值。 有关详细信息，请参阅[查询提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-query.md)。  
  
-   不能使用包含递归公用表表达式的视图来更新数据。  
  
-   可以使用 CTE 在查询上定义游标。 CTE 是*select_statement*定义游标的结果集的自变量。 递归 CTE 只允许使用快速只进游标和静态（快照）游标。 如果在递归 CTE 中指定了其他游标类型，则该类型将转换为静态游标类型。  
  
-   可以在 CTE 中引用远程服务器中的表。 如果在 CTE 的递归成员中引用了远程服务器，那么将为每个远程表创建一个假脱机，这样就可以在本地反复访问这些表。 如果为 CTE 查询，Index Spool/Lazy Spool 则显示在查询计划中，并具有额外的 WITH STACK 谓词。 这是一种确认正确递归的方法。  
  
-   CTE 递归部分中的分析和聚合函数适用于当前递归级别的集合而不适用于 CTE 集合。 ROW_NUMBER 之类的函数仅对当前递归级别传递给它们的数据子集执行运算，而不对传递给 CTE 的递归部分的整个数据集合执行运算。 有关详细信息，请参阅示例 k。 使用分析中的函数递归 CTE 后面。  
  
## <a name="features-and-limitations-of-common-table-expressions-in-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>功能和限制的通用表中的表达式[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 中的 Cte 的当前实现[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]具有以下功能和限制：  
  
-   可以在中指定 CTE**选择**语句。  
  
-   可以在中指定 CTE **CREATE VIEW**语句。  
  
-   可以在中指定 CTE **CREATE TABLE AS SELECT** (CTAS) 语句。  
  
-   可以在中指定 CTE**远程 TABLE AS SELECT** (CRTAS) 语句。  
  
-   可以在中指定 CTE **EXTERNAL TABLE AS SELECT** (CETAS) 语句。  
  
-   可以从 CTE 引用远程表。  
  
-   可以从 CTE 引用外部表。  
  
-   可以在 CTE 中定义多个 CTE 查询定义。  
  
-   CTE 后面必须跟一个**选择**语句。 **插入**，**更新**，**删除**，和**合并**中不支持语句。  
  
-   不支持公用表表达式包含对自身 （递归公用表表达式） 的引用。  
  
-   指定多个**WITH**中 CTE 子句不允许。 例如，如果 CTE_query_definition 包含子查询，该子查询不能包含嵌套**WITH**定义另一个 CTE 的子句。  
  
-   **ORDER BY**子句不能在 CTE_query_definition，除非**顶部**指定子句。  
  
-   如果将 CTE 用在属于批处理的一部分的语句中，那么在它之前的语句必须以分号结尾。  
  
-   在准备的语句中使用时**sp_prepare**，Cte 的行为方式不同于其他**选择**PDW 中的语句。 但是，如果 Cte 用作的 CETAS 准备的一部分**sp_prepare**，可以延迟其他行为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并且由于方式绑定其他 PDW 语句实现为**sp_prepare**。 如果**选择**，引用 CTE 使用错误的列不存在 CTE， **sp_prepare**将通过而无需检测错误，但该错误将引发期间**sp_execute**相反。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-simple-common-table-expression"></a>A. 创建一个简单公用表表达式  
 下例显示 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 的每名销售代表每年的销售订单总数。  
  
```  
  
-- Define the CTE expression name and column list.  
WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
AS  
-- Define the CTE query.  
(  
    SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
)  
-- Define the outer query referencing the CTE name.  
SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
FROM Sales_CTE  
GROUP BY SalesYear, SalesPersonID  
ORDER BY SalesPersonID, SalesYear;  
GO  
  
```  
  
### <a name="b-using-a-common-table-expression-to-limit-counts-and-report-averages"></a>B. 使用公用表表达式来限制次数和报告平均数  
 以下示例显示销售代表在所有年度内的平均销售订单数。  
  
```  
WITH Sales_CTE (SalesPersonID, NumberOfOrders)  
AS  
(  
    SELECT SalesPersonID, COUNT(*)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
    GROUP BY SalesPersonID  
)  
SELECT AVG(NumberOfOrders) AS "Average Sales Per Person"  
FROM Sales_CTE;  
GO  
```  
  
### <a name="c-using-multiple-cte-definitions-in-a-single-query"></a>C. 在单个查询中使用多个 CTE 定义  
 下面的示例显示如何在单个查询中定义多个 CTE。 注意，其中使用逗号分隔 CTE 查询定义。 SQL Server 2012 和更高版本中提供 FORMAT 函数，用于以货币格式显示货币金额。  
  
```  
  
WITH Sales_CTE (SalesPersonID, TotalSales, SalesYear)  
AS  
-- Define the first CTE query.  
(  
    SELECT SalesPersonID, SUM(TotalDue) AS TotalSales, YEAR(OrderDate) AS SalesYear  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
       GROUP BY SalesPersonID, YEAR(OrderDate)  
  
)  
,   -- Use a comma to separate multiple CTE definitions.  
  
-- Define the second CTE query, which returns sales quota data by year for each sales person.  
Sales_Quota_CTE (BusinessEntityID, SalesQuota, SalesQuotaYear)  
AS  
(  
       SELECT BusinessEntityID, SUM(SalesQuota)AS SalesQuota, YEAR(QuotaDate) AS SalesQuotaYear  
       FROM Sales.SalesPersonQuotaHistory  
       GROUP BY BusinessEntityID, YEAR(QuotaDate)  
)  
  
-- Define the outer query by referencing columns from both CTEs.  
SELECT SalesPersonID  
  , SalesYear  
  , FORMAT(TotalSales,'C','en-us') AS TotalSales  
  , SalesQuotaYear  
  , FORMAT (SalesQuota,'C','en-us') AS SalesQuota  
  , FORMAT (TotalSales -SalesQuota, 'C','en-us') AS Amt_Above_or_Below_Quota  
FROM Sales_CTE  
JOIN Sales_Quota_CTE ON Sales_Quota_CTE.BusinessEntityID = Sales_CTE.SalesPersonID  
                    AND Sales_CTE.SalesYear = Sales_Quota_CTE.SalesQuotaYear  
ORDER BY SalesPersonID, SalesYear;  
GO  
  
```  
  
 以下为部分结果集。  
  
```  
  
SalesPersonID SalesYear   TotalSales    SalesQuotaYear SalesQuota  Amt_Above_or_Below_Quota  
------------- ---------   -----------   -------------- ---------- ----------------------------------   
  
274           2005        $32,567.92    2005           $35,000.00  ($2,432.08)  
274           2006        $406,620.07   2006           $455,000.00 ($48,379.93)  
274           2007        $515,622.91   2007           $544,000.00 ($28,377.09)  
274           2008        $281,123.55   2008           $271,000.00  $10,123.55  
  
```  
  
### <a name="d-using-a-recursive-common-table-expression-to-display-multiple-levels-of-recursion"></a>D. 使用递归公用表表达式显示递归的多个级别  
 以下示例显示经理以及向经理报告的雇员的层次列表。 该示例首先创建并填充 `dbo.MyEmployees` 表。  
  
```  
-- Create an Employee table.  
CREATE TABLE dbo.MyEmployees  
(  
EmployeeID smallint NOT NULL,  
FirstName nvarchar(30)  NOT NULL,  
LastName  nvarchar(40) NOT NULL,  
Title nvarchar(50) NOT NULL,  
DeptID smallint NOT NULL,  
ManagerID int NULL,  
 CONSTRAINT PK_EmployeeID PRIMARY KEY CLUSTERED (EmployeeID ASC)   
);  
-- Populate the table with values.  
INSERT INTO dbo.MyEmployees VALUES   
 (1, N'Ken', N'Sánchez', N'Chief Executive Officer',16,NULL)  
,(273, N'Brian', N'Welcker', N'Vice President of Sales',3,1)  
,(274, N'Stephen', N'Jiang', N'North American Sales Manager',3,273)  
,(275, N'Michael', N'Blythe', N'Sales Representative',3,274)  
,(276, N'Linda', N'Mitchell', N'Sales Representative',3,274)  
,(285, N'Syed', N'Abbas', N'Pacific Sales Manager',3,273)  
,(286, N'Lynn', N'Tsoflias', N'Sales Representative',3,285)  
,(16,  N'David',N'Bradley', N'Marketing Manager', 4, 273)  
,(23,  N'Mary', N'Gibson', N'Marketing Specialist', 4, 16);  
```  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(ManagerID, EmployeeID, Title, EmployeeLevel) AS   
(  
    SELECT ManagerID, EmployeeID, Title, 0 AS EmployeeLevel  
    FROM dbo.MyEmployees   
    WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT e.ManagerID, e.EmployeeID, e.Title, EmployeeLevel + 1  
    FROM dbo.MyEmployees AS e  
        INNER JOIN DirectReports AS d  
        ON e.ManagerID = d.EmployeeID   
)  
SELECT ManagerID, EmployeeID, Title, EmployeeLevel   
FROM DirectReports  
ORDER BY ManagerID;  
GO  
```  
  
### <a name="e-using-a-recursive-common-table-expression-to-display-two-levels-of-recursion"></a>E. 使用递归公用表表达式显示递归的两个级别  
 以下示例显示经理以及向经理报告的雇员。 将返回的级别数目限制为两个。  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(ManagerID, EmployeeID, Title, EmployeeLevel) AS   
(  
    SELECT ManagerID, EmployeeID, Title, 0 AS EmployeeLevel  
    FROM dbo.MyEmployees   
    WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT e.ManagerID, e.EmployeeID, e.Title, EmployeeLevel + 1  
    FROM dbo.MyEmployees AS e  
        INNER JOIN DirectReports AS d  
        ON e.ManagerID = d.EmployeeID   
)  
SELECT ManagerID, EmployeeID, Title, EmployeeLevel   
FROM DirectReports  
WHERE EmployeeLevel <= 2 ;  
GO  
  
```  
  
### <a name="f-using-a-recursive-common-table-expression-to-display-a-hierarchical-list"></a>F. 使用递归公用表表达式显示层次列表  
 以下示例在示例 D 的基础上添加经理和雇员的名称，以及他们各自的头衔。 通过缩进各个级别，突出显示经理和雇员的层次结构。  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(Name, Title, EmployeeID, EmployeeLevel, Sort)  
AS (SELECT CONVERT(varchar(255), e.FirstName + ' ' + e.LastName),  
        e.Title,  
        e.EmployeeID,  
        1,  
        CONVERT(varchar(255), e.FirstName + ' ' + e.LastName)  
    FROM dbo.MyEmployees AS e  
    WHERE e.ManagerID IS NULL  
    UNION ALL  
    SELECT CONVERT(varchar(255), REPLICATE ('|    ' , EmployeeLevel) +  
        e.FirstName + ' ' + e.LastName),  
        e.Title,  
        e.EmployeeID,  
        EmployeeLevel + 1,  
        CONVERT (varchar(255), RTRIM(Sort) + '|    ' + FirstName + ' ' +   
                 LastName)  
    FROM dbo.MyEmployees AS e  
    JOIN DirectReports AS d ON e.ManagerID = d.EmployeeID  
    )  
SELECT EmployeeID, Name, Title, EmployeeLevel  
FROM DirectReports   
ORDER BY Sort;  
GO  
```  
  
### <a name="g-using-maxrecursion-to-cancel-a-statement"></a>G. 使用 MAXRECURSION 取消一条语句  
 可以使用 `MAXRECURSION` 来防止不合理的递归 CTE 进入无限循环。 下面的示例特意创建了一个无限循环，然后使用 `MAXRECURSION` 提示将递归级别限制为两级。  
  
```  
USE AdventureWorks2012;  
GO  
--Creates an infinite loop  
WITH cte (EmployeeID, ManagerID, Title) as  
(  
    SELECT EmployeeID, ManagerID, Title  
    FROM dbo.MyEmployees  
    WHERE ManagerID IS NOT NULL  
  UNION ALL  
    SELECT cte.EmployeeID, cte.ManagerID, cte.Title  
    FROM cte   
    JOIN  dbo.MyEmployees AS e   
        ON cte.ManagerID = e.EmployeeID  
)  
--Uses MAXRECURSION to limit the recursive levels to 2  
SELECT EmployeeID, ManagerID, Title  
FROM cte  
OPTION (MAXRECURSION 2);  
GO  
```  
  
 在更正代码错误之后，就不再需要 MAXRECURSION。 以下示例显示了更正后的代码。  
  
```  
USE AdventureWorks2012;  
GO  
WITH cte (EmployeeID, ManagerID, Title)  
AS  
(  
    SELECT EmployeeID, ManagerID, Title  
    FROM dbo.MyEmployees  
    WHERE ManagerID IS NOT NULL  
  UNION ALL  
    SELECT  e.EmployeeID, e.ManagerID, e.Title  
    FROM dbo.MyEmployees AS e  
    JOIN cte ON e.ManagerID = cte.EmployeeID  
)  
SELECT EmployeeID, ManagerID, Title  
FROM cte;  
GO  
```  
  
### <a name="h-using-a-common-table-expression-to-selectively-step-through-a-recursive-relationship-in-a-select-statement"></a>H. 使用公用表表达式来有选择地执行 SELECT 语句中的递归关系操作  
 以下示例显示了为 `ProductAssemblyID = 800` 生产自行车所需的产品装配和部件层次结构。  
  
```  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
SELECT AssemblyID, ComponentID, Name, PerAssemblyQty, EndDate,  
        ComponentLevel   
FROM Parts AS p  
    INNER JOIN Production.Product AS pr  
    ON p.ComponentID = pr.ProductID  
ORDER BY ComponentLevel, AssemblyID, ComponentID;  
GO  
```  
  
### <a name="i-using-a-recursive-cte-in-an-update-statement"></a>I. 在 UPDATE 语句中使用递归 CTE  
 下面的示例更新`PerAssemblyQty`值为用于生成产品道路 550 W 黄色，44 的所有部分`(ProductAssemblyID``800`)。 公用表表达式将返回用于生成 `ProductAssemblyID 800` 的部件和用于生成这些部件的组件等的层次结构列表。 只修改公用表表达式所返回的行。  
  
```  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
UPDATE Production.BillOfMaterials  
SET PerAssemblyQty = c.PerAssemblyQty * 2  
FROM Production.BillOfMaterials AS c  
JOIN Parts AS d ON c.ProductAssemblyID = d.AssemblyID  
WHERE d.ComponentLevel = 0;  
```  
  
### <a name="j-using-multiple-anchor-and-recursive-members"></a>J. 使用多个定位点和递归成员  
 以下示例使用多个定位点和递归成员来返回指定的人的所有祖先。 创建了一个表，并在表中插入值，以建立由递归 CTE 返回的宗谱。  
  
```  
-- Genealogy table  
IF OBJECT_ID('dbo.Person','U') IS NOT NULL DROP TABLE dbo.Person;  
GO  
CREATE TABLE dbo.Person(ID int, Name varchar(30), Mother int, Father int);  
GO  
INSERT dbo.Person   
VALUES(1, 'Sue', NULL, NULL)  
      ,(2, 'Ed', NULL, NULL)  
      ,(3, 'Emma', 1, 2)  
      ,(4, 'Jack', 1, 2)  
      ,(5, 'Jane', NULL, NULL)  
      ,(6, 'Bonnie', 5, 4)  
      ,(7, 'Bill', 5, 4);  
GO  
-- Create the recursive CTE to find all of Bonnie's ancestors.  
WITH Generation (ID) AS  
(  
-- First anchor member returns Bonnie's mother.  
    SELECT Mother   
    FROM dbo.Person  
    WHERE Name = 'Bonnie'  
UNION  
-- Second anchor member returns Bonnie's father.  
    SELECT Father   
    FROM dbo.Person  
    WHERE Name = 'Bonnie'  
UNION ALL  
-- First recursive member returns male ancestors of the previous generation.  
    SELECT Person.Father  
    FROM Generation, Person  
    WHERE Generation.ID=Person.ID  
UNION ALL  
-- Second recursive member returns female ancestors of the previous generation.  
    SELECT Person.Mother  
    FROM Generation, dbo.Person  
    WHERE Generation.ID=Person.ID  
)  
SELECT Person.ID, Person.Name, Person.Mother, Person.Father  
FROM Generation, dbo.Person  
WHERE Generation.ID = Person.ID;  
GO  
```  
  
###  <a name="bkmkUsingAnalyticalFunctionsInARecursiveCTE"></a> K. 在递归 CTE 中使用分析函数  
 以下示例显示在 CTE 的递归部分中使用分析或聚合函数时可能出现的问题。  
  
```  
DECLARE @t1 TABLE (itmID int, itmIDComp int);  
INSERT @t1 VALUES (1,10), (2,10);   
  
DECLARE @t2 TABLE (itmID int, itmIDComp int);   
INSERT @t2 VALUES (3,10), (4,10);   
  
WITH vw AS  
 (  
    SELECT itmIDComp, itmID  
    FROM @t1  
  
    UNION ALL  
  
    SELECT itmIDComp, itmID  
    FROM @t2  
)   
,r AS  
 (  
    SELECT t.itmID AS itmIDComp  
           , NULL AS itmID  
           ,CAST(0 AS bigint) AS N  
           ,1 AS Lvl  
    FROM (SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4) AS t (itmID)   
  
UNION ALL  
  
SELECT t.itmIDComp  
    , t.itmID  
    , ROW_NUMBER() OVER(PARTITION BY t.itmIDComp ORDER BY t.itmIDComp, t.itmID) AS N  
    , Lvl + 1  
FROM r   
    JOIN vw AS t ON t.itmID = r.itmIDComp  
)   
  
SELECT Lvl, N FROM r;  
```  
  
 以下结果是查询的预期结果。  
  
```  
Lvl  N  
1    0  
1    0  
1    0  
1    0  
2    4  
2    3  
2    2  
2    1  
```  
  
 以下结果是查询的实际结果。  
  
```  
Lvl  N  
1    0  
1    0  
1    0  
1    0  
2    1  
2    1  
2    1  
2    1  
```  
  
 `N` 为 CTE 递归部分的每次传递返回 1，这是因为只向 `ROWNUMBER` 传递了该递归级别的数据子集。 对于查询递归部分的每次迭代，只向 `ROWNUMBER` 传递了一行。  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="l-using-a-common-table-expression-within-a-ctas-statement"></a>L. 使用 CTAS 语句中的公用表表达式  
 下面的示例创建一个包含每年的销售订单的总数在每个销售代表的新表[!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]。  
  
```  
-- Uses AdventureWorks  
  
CREATE TABLE SalesOrdersPerYear  
WITH  
(  
    DISTRIBUTION = HASH(SalesPersonID)  
)  
AS  
    -- Define the CTE expression name and column list.  
    WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
    AS  
    -- Define the CTE query.  
    (  
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
        FROM Sales.SalesOrderHeader  
        WHERE SalesPersonID IS NOT NULL  
    )  
    -- Define the outer query referencing the CTE name.  
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
    FROM Sales_CTE  
    GROUP BY SalesYear, SalesPersonID  
    ORDER BY SalesPersonID, SalesYear;  
GO  
```  
  
### <a name="m-using-a-common-table-expression-within-a-cetas-statement"></a>M. 使用 CETAS 语句中的公用表表达式  
 下面的示例创建新的外部表包含每年的销售订单的总数在每个销售代表[!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]。  
  
```  
-- Uses AdventureWorks  
  
CREATE EXTERNAL TABLE SalesOrdersPerYear  
WITH  
(  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:5000/files/Customer',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|' )   
)  
AS  
    -- Define the CTE expression name and column list.  
    WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
    AS  
    -- Define the CTE query.  
    (  
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
        FROM Sales.SalesOrderHeader  
        WHERE SalesPersonID IS NOT NULL  
    )  
    -- Define the outer query referencing the CTE name.  
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
    FROM Sales_CTE  
    GROUP BY SalesYear, SalesPersonID  
    ORDER BY SalesPersonID, SalesYear;  
GO  
```  
  
### <a name="n-using-multiple-comma-separated-ctes-in-a-statement"></a>N. 在语句中使用多个以逗号分隔 Cte  
 下面的示例演示在单个语句中包括两个 Cte。 Cte 不能为嵌套 （不允许使用递归）。  
  
```  
WITH   
 CountDate (TotalCount, TableName) AS  
    (  
     SELECT COUNT(datekey), 'DimDate' FROM DimDate  
    ) ,  
 CountCustomer (TotalAvg, TableName) AS  
    (  
     SELECT COUNT(CustomerKey), 'DimCustomer' FROM DimCustomer  
    )  
SELECT TableName, TotalCount FROM CountDate  
UNION ALL  
SELECT TableName, TotalAvg FROM CountCustomer;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE VIEW (Transact-SQL)](../../t-sql/statements/create-view-transact-sql.md)   
 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)   
 [除和 INTERSECT &#40;Transact SQL &#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)  
  
  
