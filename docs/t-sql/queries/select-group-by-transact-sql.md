---
title: "GROUP BY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GROUP
- CUBE
- ROLLUP
- GROUPING_SETS_TSQL
- GROUP BY
- GROUPING SETS
- GROUP_BY_TSQL
- GROUP_TSQL
- CUBE_TSQL
- ROLLUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GROUP BY clause, about GROUP BY clause
- dividing tables into groups
- GROUPING SETS
- GROUP BY clause
- table groups [SQL Server]
- groups [SQL Server], tables divided into groups
- summary values [SQL Server]
ms.assetid: 40075914-6385-4692-b4a5-62fe44ae6cb6
caps.latest.revision: 80
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 01e2c02cade5b84f3560fe5cb415cece4f815abf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="select---group-by--transact-sql"></a>选择的组 BY-TRANSACT-SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

SELECT 语句子句，用于将查询结果划分为组的行，其目的通常是对每个组执行一个或多个聚合。 SELECT 语句返回每个组的一行。  
  
## <a name="syntax"></a>语法  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
```  
-- Syntax for SQL Server and Azure SQL Database   
-- ISO-Compliant Syntax  
  
GROUP BY {
      column-expression  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
    | GROUPING SETS ( <grouping_set> [ ,...n ]  )  
    | () --calculates the grand total 
} [ ,...n ] 
 
<group_by_expression> ::=  
      column-expression  
    | ( column-expression [ ,...n ] )    
   
<grouping_set> ::=  
      () --calculates the grand total  
    | <grouping_set_item>  
    | ( <grouping_set_item> [ ,...n ] )  
  
<grouping_set_item> ::=  
      <group_by_expression>  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
  

-- For backward compatibility only.
-- Non-ISO-Compliant Syntax for SQL Server and Azure SQL Database 
  
GROUP BY 
      [ ALL ] column-expression [ ,...n ] 
    | column-expression [ ,...n ] [ WITH { CUBE | ROLLUP } ]   

```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GROUP BY {
      column-name [ WITH (DISTRIBUTED_AGG) ]  
    | column-expression
} [ ,...n ]

```  
  
## <a name="arguments"></a>参数 
 
### <a name="column-expression"></a>*列表达式*  
在列上指定一列或非聚合计算。 此列可以属于表、 派生的表或视图。 列必须出现在 SELECT 语句的 FROM 子句，但不需要选择列表中显示。 

有关有效表达式，请参阅[表达式](~/t-sql/language-elements/expressions-transact-sql.md)。    

列必须出现在 SELECT 语句的 FROM 子句，但不需要选择列表中显示。 但是，每个表或视图中的任何非聚合表达式中的列\<选择 > 列表必须包含在 GROUP BY 列表：  
  
允许使用下面的语句：  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + ColumnB + constant FROM T GROUP BY ColumnA, ColumnB;  
    ```  
  
不允许使用下面的语句：  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + constant + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    ```  
列表达式不能包含：

- 在选择列表中定义的列别名。 它可用于在 FROM 子句中定义的派生表的列别名。
- 类型的列**文本**， **ntext**，或**映像**。 但是，你可以使用 text、 ntext 或 image 的列作为返回值为有效的数据类型的函数的自变量。 例如，表达式可以使用 substring （） 和 CAST()。 这也适用于 HAVING 子句中的表达式。
- xml 数据类型方法。 它可以包括使用 xml 数据类型方法的用户定义函数。 它可以包括的计算的列，使用 xml 数据类型方法。 
- 子查询。 返回错误 144。 
- 从索引视图列。 
 
### <a name="group-by-column-expression--n-"></a>GROUP BY*列表达式*[，...n] 

根据值列表中的一个或多个列表达式的 SELECT 语句结果进行分组。 

例如，此查询创建 Sales 表包含列的国家/地区、 区域和销售。 它可以将插入四行和两个行的国家和地区有匹配的值。  

```
CREATE TABLE Sales ( Country varchar(50), Region varchar(50), Sales int );

INSERT INTO sales VALUES (N'Canada', N'Alberta', 100);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 200);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 300);
INSERT INTO sales VALUES (N'United States', N'Montana', 100);
```
Sales 表包含这些行：

| Country | 地区 | Sales |
|---------|--------|-------|
| Canada | 艾伯塔 | 100 |
| Canada | 不列颠哥伦比亚 | 200 |
| Canada | 不列颠哥伦比亚 | 300 |
| United States | 蒙 | 100 |

此第二个查询分组国家和地区，并返回每个值组合的聚合总数。  
 
``` 
SELECT Country, Region, SUM(sales) AS TotalSales
FROM Sales
GROUP BY Country, Region;
```
查询结果具有 3 行，因为有 3 组合的国家和地区的值。 加拿大和不列颠哥伦比亚 TotalSales 是两个行的总数。 

| Country | 地区 | 总销售额 |
|---------|--------|-------|
| Canada | 艾伯塔 | 100 |
| Canada | 不列颠哥伦比亚 | 500 |
| United States | 蒙 | 100 |

### <a name="group-by-rollup"></a>组汇总

创建列表达式的每个组合的组。 此外，它"汇总"结果到小计和总计。 若要执行此操作，它将移动从右到左减少，它会创建组和 aggregation(s) 的列表达式的数量。 

列顺序会影响汇总输出，并可能会影响在结果集中的行数。  

例如，`GROUP BY ROLLUP (col1, col2, col3, col4)`如下表中创建的每个组合的列表达式的组。  

- col1，col2，col3，第 4 列 
- col1，col2，col3，NULL
- col1，col2，NULL NULL
- col1，NULL，NULL NULL
- NULL、 空、 NULL、 空-这是计算总和

使用上一示例中的表，此代码将运行而不是简单分组依据组的汇总操作。

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region);
```

查询结果已作为简单 GROUP BY 而无需汇总相同的聚合。 此外，它将创建的每个值的国家/地区的小计。 最后，它使所有行的总计。 结果如下所示：

| Country | 地区 | 总销售额 |
| :------ | :----- | ---------: |
| Canada | 艾伯塔 | 100 |
| Canada | 不列颠哥伦比亚 | 500 |
| Canada | NULL | 600 |
| United States | 蒙 | 100 |
| United States | NULL | 100 |
| NULL | NULL | 700 |

### <a name="group-by-cube--"></a>分组依据多维数据集 （）  

组的多维数据集创建的列的所有可能组合的组。 为组的多维数据集 (a、 b) 结果具有唯一值的组的 (a、 b)、 （NULL、 b），(a，NULL) 和 （NULL，NULL）。

使用前面示例中的表，此代码将运行在国家和地区组由多维数据集操作。 

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

查询结果具有唯一值的 （国家/地区，区域），组 （NULL、 区域），（Country、 NULL） 和 （NULL，NULL）。 结果如下所示：

| Country | 地区 | 总销售额 |
|---------|--------|-------|
| Canada | 艾伯塔 | 100 |
| NULL | 艾伯塔 | 100 |
| Canada | 不列颠哥伦比亚 | 500 |
| NULL | 不列颠哥伦比亚 | 500 |
| United States | 蒙 | 100 |
| NULL | 蒙 | 100 |
| NULL | NULL | 700
| Canada | NULL | 600 |
| United States | NULL | 100 |
   
 ### <a name="group-by-grouping-sets--"></a>通过将分组集 （） 的组  
 
GROUPING SETS 选项使你能够将多个 GROUP BY 子句组合到一个 GROUP BY 子句。 其结果与针对指定的组执行 UNION ALL 运算等效。 

例如，`GROUP BY ROLLUP (Country, Region)`和`GROUP BY GROUPING SETS ( ROLLUP (Country, Region) )`返回相同的结果。 

当 GROUPING SETS 具有两个或多个元素时，则结果是元素的联合。 此示例返回国家/地区和区域汇总和多维数据集结果的联合。

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( ROLLUP (Country, Region), CUBE (Country, Region) );
```

结果将是此查询将返回两个 GROUP BY 语句的并集相同。

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region)
UNION ALL
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region)
;
```

SQL 不会合并为 GROUPING SETS 列表生成的重复组。 例如，在`GROUP BY ( (), CUBE (Country, Region) )`，这两个元素返回总计的行并将结果中列出这两个行。 

 ### <a name="group-by-"></a>GROUP BY ()  
指定生成计算总和的空组。 这可以作为一个分组集的元素。 例如，此语句将授予的总销售额的每个国家/地区，然后将授予的所有国家/地区的总计。

```
SELECT Country, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( Country, () );
```

### <a name="group-by--all--column-expression--n-"></a>GROUP BY [全部] 列表达式 [，...n] 

适用于： SQL Server 和 Azure SQL 数据库

注意： 此语法进行向后兼容性。 未来版本中，将删除它。 避免在新的开发工作中使用此语法，并计划修改当前使用此语法的应用程序。

指定要包括的结果而不考虑它们是否达到 WHERE 子句中的搜索条件中的所有组。 不能满足搜索条件的组的聚合中具有 NULL。 

所有组：
- 如果还 WHERE 子句中没有查询访问远程表的查询中不支持。
- 具有 FILESTREAM 属性的列上将失败。
  
### <a name="with-distributedagg"></a>使用 (DISTRIBUTED_AGG)
适用范围： Azure SQL 数据仓库和并行数据仓库

DISTRIBUTED_AGG 查询提示将强制大规模并行处理 (MPP) 系统在执行聚合之前重新分发的特定列上的表。 GROUP BY 子句中的只有一个列可以具有 DISTRIBUTED_AGG 查询提示。 查询完成后，删除重新分发的表。 原始表不会更改。  

注意： DISTRIBUTED_AGG 查询提示为了向后兼容早期并行数据仓库版本，并且不会提高对于大多数查询的性能。 默认情况下，MPP 已时会将重新分配数据根据需要以提高聚合的性能。 
  
## <a name="general-remarks"></a>一般备注

### <a name="how-group-by-interacts-with-the-select-statement"></a>GROUP BY 与交互的方式的 SELECT 语句
选择列表：
- 向量的聚合函数。 如果聚合函数包括在选择列表中，GROUP BY 将计算每个组的汇总值。 这些函数称为矢量聚合。 
- Distinct 聚合。 聚合 AVG (DISTINCT *column_name*)，计数 (DISTINCT *column_name*)，和总和 (DISTINCT *column_name*) 与汇总、 多维数据集和 GROUPING SETS 支持。
  
WHERE 子句：
- SQL 中删除任何分组操作执行前不满足 WHERE 子句中的条件的行。  
  
HAVING 子句：
- SQL 使用 having 子句为结果集中筛选组。 
  
ORDER BY 子句：
- 使用 ORDER BY 子句可以对结果集进行排序。 GROUP BY 子句不能对结果集进行排序。 
  
NULL 值：
- 如果分组列包含 NULL 值，所有 NULL 值被都视为相等，它们是收集到单个组。   
  
## <a name="limitations-and-restrictions"></a>限制和局限

适用于： SQL Server （从 2008年开始） 和 Azure SQL 数据仓库

### <a name="maximum-capacity"></a>最大容量

为 GROUP BY 子句使用 ROLLUP、 CUBE 或 GROUPING SETS，表达式的最大数目为 32。 最大组数为 4096 (2<sup>12</sup>)。 下面的示例失败，因为 GROUP BY 子句有多个 4096 组。  
 
-   下面的示例生成 4097 (2<sup>12</sup> + 1) 对集进行分组，并且将失败。  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), b )  
    ```  
  
-   下面的示例生成 4097 (2<sup>12</sup> + 1) 分组，并将失败。 `CUBE ()` 和 `()` 分组集会生成一个总计行，而且将不删除重复的分组集。  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), ())  
    ```  

-   此示例使用向后兼容语法。 它会生成 8192 (2<sup>13</sup>) 对集进行分组，并且将失败。  
  
    ```  
    GROUP BY CUBE (a1, ..., a13)   
    GROUP BY a1, ..., a13 WITH CUBE   
    ```    
    向后兼容 GROUP BY 子句不包含 CUBE 或 ROLLUP，分组依据的项的数目受到分组依据列的大小，聚合的列，并在查询中涉及的聚合值。 该限制从 8,060 字节的限制开始，对保存中间查询结果所需的中间级工作表有 8,060 字节的限制。 如果指定了 CUBE 或 ROLLUP，则最多只能有 12 个分组表达式。

### <a name="support-for-iso-and-ansi-sql-2006-group-by-features"></a>对 ISO 和 ANSI SQL-2006 GROUP BY 功能的支持

GROUP BY 子句支持使用以下语法例外的 SQL 2006 标准中包含的所有 GROUP BY 功能：  
  
-   不允许在 GROUP BY 子句中使用分组集，除非它们是显式 GROUPING SETS 列表的一部分。 例如， `GROUP BY Column1, (Column2, ...ColumnN`) 标准中但在 TRANSACT-SQL 中不允许。  TRANSACT-SQL 支持`GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))`和`GROUP BY Column1, Column2, ... ColumnN`，这在语义上等效。 这些示例与上面的 `GROUP BY` 示例在语义上等效。 这是为了避免出现的情况， `GROUP BY Column1, (Column2, ...ColumnN`) 可能被错误解释为`GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))`，哪些不是在语义上等效。  
  
-   不允许在分组集内部使用分组集。 例如， `GROUP BY GROUPING SETS (A1, A2,…An, GROUPING SETS (C1, C2, ...Cn))` SQL 2006 标准中但在 TRANSACT-SQL 中不允许。 TRANSACT-SQL 允许`GROUP BY GROUPING SETS( A1, A2,...An, C1, C2, ...Cn )`或`GROUP BY GROUPING SETS( (A1), (A2), ... (An), (C1), (C2), ... (Cn) )`，它在语义上等效于第一个 GROUP BY 示例并具有一个更清晰的语法。  
  
-   [ALL/DISTINCT] 是仅允许使用 GROUP BY 简单 GROUP BY 子句中，其中包含列表达式。 不允许使用 GROUPING SETS、 汇总、 多维数据集、 WITH CUBE 或 WITH ROLLUP 构造。 ALL 是隐式默认值。 它还仅允许用在向后兼容语法。
  
### <a name="comparison-of-supported-group-by-features"></a>对支持的 GROUP BY 功能的比较  
 下表介绍支持基于 SQL 版本和数据库兼容性级别的 GROUP BY 功能。  
  
|功能|SQL Server Integration Services|SQL Server 兼容级别 100 或更高|SQL Server 2008 或兼容级别为 90 的更高版本。|  
|-------------|-------------------------------------|--------------------------------------------------|-----------------------------------------------------------|  
|DISTINCT 聚合|WITH CUBE 或 WITH ROLLUP 不支持。|WITH CUBE、WITH ROLLUP、GROUPING SETS、CUBE 或 ROLLUP 支持。|与兼容级别 100 相同。|  
|GROUP BY 子句中具有 CUBE 或 ROLLUP 名称的用户定义函数|用户定义函数**dbo.cube (***arg1***，***...argN***)**或**dbo.rollup (***arg1***，**...*argN***)**在 GROUP BY 子句允许。<br /><br /> 例如： `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|用户定义函数**dbo.cube (***arg1***，**...argN**)**或**dbo.rollup (**arg1**，***...argN***)**在 GROUP BY 子句不允许。<br /><br /> 例如： `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`<br /><br /> 将返回以下错误消息:"关键字多维数据集 &#124; 附近有语法错误汇总。"<br /><br /> 为了避免出现此问题，请将 `dbo.cube` 替换为 `[dbo].[cube]` 或将 `dbo.rollup` 替换为 `[dbo].[rollup]`。<br /><br /> 下面的示例被允许:`SELECT SUM (x) FROM T  GROUP BY [dbo].[cube](y);`|用户定义函数**dbo.cube (***arg1***，***...argN*) 或**dbo.rollup (** *arg1***，***...argN***)**在 GROUP BY 子句允许<br /><br /> 例如： `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|  
|GROUPING SETS|不支持|是否支持|是否支持|  
|CUBE|不支持|是否支持|不支持|  
|ROLLUP|不支持|是否支持|不支持|  
|总计，如 GROUP BY ()|不支持|是否支持|是否支持|  
|GROUPING_ID 函数|不支持|是否支持|是否支持|  
|GROUPING 函数|是否支持|是否支持|是否支持|  
|WITH CUBE|是否支持|是否支持|是否支持|  
|WITH ROLLUP|是否支持|是否支持|是否支持|  
|WITH CUBE 或 WITH ROLLUP“重复”分组删除|是否支持|是否支持|是否支持| 
 
  
## <a name="examples"></a>示例  
  
### <a name="a-use-a-simple-group-by-clause"></a>A. 使用简单的 GROUP BY 子句  
 以下示例检索 `SalesOrderID` 表中各 `SalesOrderDetail` 的总数。 此示例使用 AdventureWorks。  
  
```  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail AS sod  
GROUP BY SalesOrderID  
ORDER BY SalesOrderID;  
```  
  
### <a name="b-use-a-group-by-clause-with-multiple-tables"></a>B. 多个表使用 GROUP BY 子句  
 下面的示例检索与 `City` 表联接的 `Address` 表中的各 `EmployeeAddress` 的雇员数。 此示例使用 AdventureWorks。 
  
```  
SELECT a.City, COUNT(bea.AddressID) EmployeeCount  
FROM Person.BusinessEntityAddress AS bea   
    INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
GROUP BY a.City  
ORDER BY a.City;  
```  
  
### <a name="c-use-a-group-by-clause-with-an-expression"></a>C. 使用的表达式中使用 GROUP BY 子句  
 以下示例使用 `DATEPART` 函数检索每年的销售总额。 同一个表达式必须存在于这两`SELECT`列表和`GROUP BY`子句。  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
### <a name="d-use-a-group-by-clause-with-a-having-clause"></a>D. HAVING 子句中使用 GROUP BY 子句  
 下面的示例使用 `HAVING` 子句来指定应当将 `GROUP BY` 子句中生成的哪个组包括在结果集内。  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
HAVING DATEPART(yyyy,OrderDate) >= N'2003'  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
## <a name="examples-sql-data-warehouse-and-parallel-data-warehouse"></a>示例： SQL 数据仓库和并行数据仓库  
  
### <a name="e-basic-use-of-the-group-by-clause"></a>E. GROUP BY 子句的基本用法  
 下面的示例查找每天所有销售的总金额。 针对每一天，返回一行，其中包含的所有销售额的总和。  
  
```  
-- Uses AdventureWorksDW  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales FROM FactInternetSales  
GROUP BY OrderDateKey ORDER BY OrderDateKey;  
```  
  
### <a name="f-basic-use-of-the-distributedagg-hint"></a>F. 基本使用 DISTRIBUTED_AGG 提示  
 此示例使用 DISTRIBUTED_AGG 查询提示以强制设备可以随机表上排布`CustomerKey`之前执行聚合的列。  
  
```  
-- Uses AdventureWorksDW  
  
SELECT CustomerKey, SUM(SalesAmount) AS sas  
FROM FactInternetSales  
GROUP BY CustomerKey WITH (DISTRIBUTED_AGG)  
ORDER BY CustomerKey DESC;  
```  
  
### <a name="g-syntax-variations-for-group-by"></a>G. 通过为组的的语法变体  
 如果选择列表中不有任何聚合，选择列表中每一列必须包含在 GROUP BY 列表中。 选择列表中的计算的列可以列出，但不是必需的 GROUP BY 列表中。 这些是语法上有效的 SELECT 语句的示例：  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName FROM DimCustomer GROUP BY LastName, FirstName;  
SELECT NumberCarsOwned FROM DimCustomer GROUP BY YearlyIncome, NumberCarsOwned;  
SELECT (SalesAmount + TaxAmt + Freight) AS TotalCost FROM FactInternetSales GROUP BY SalesAmount, TaxAmt, Freight;  
SELECT SalesAmount, SalesAmount*1.10 SalesTax FROM FactInternetSales GROUP BY SalesAmount;  
SELECT SalesAmount FROM FactInternetSales GROUP BY SalesAmount, SalesAmount*1.10;  
```  
  
### <a name="h-using-a-group-by-with-multiple-group-by-expressions"></a>H. 使用 GROUP BY 与多个 GROUP BY 表达式  
 下面的示例使用多个的结果进行分组`GROUP BY`条件。 如果是，在每个`OrderDateKey`组，则有加以区分的子组`DueDateKey`，将为该结果集定义新的组合。  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, DueDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSalesGROUP BY OrderDateKey, DueDateKey   
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-a-group-by-clause-with-a-having-clause"></a>I. 将 GROUP BY 子句与 HAVING 子句一起使用  
 下面的示例使用`HAVING`子句来指定在生成的组`GROUP BY`子句应包含在结果集。 仅在 2004年或更高版本中的订单日期具有这些组将包含在结果中。  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING OrderDateKey > 20040000   
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>另请参阅  
 [GROUPING_ID &#40;Transact SQL &#41;](~/t-sql/functions/grouping-id-transact-sql.md)   
 [分组 &#40;Transact SQL &#41;](~/t-sql/functions/grouping-transact-sql.md)   
 [SELECT (Transact-SQL)](~/t-sql/queries/select-transact-sql.md)   
 [SELECT 子句 &#40;Transact SQL &#41;](~/t-sql/queries/select-clause-transact-sql.md)  
  
  





