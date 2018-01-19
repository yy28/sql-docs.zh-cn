---
title: "选择 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT_TSQL
- SELECT
dev_langs: TSQL
helpviewer_keywords:
- retrieving rows
- SELECT statement [SQL Server]
- SELECT statement [SQL Server], about SELECT statement
- row retrieval [SQL Server], SELECT statement
- DML [SQL Server], SELECT statement
- data manipulation language [SQL Server], SELECT statement
- row retrieval [SQL Server]
- queries [SQL Server], results
ms.assetid: dc85caea-54d1-49af-b166-f3aa2f3a93d0
caps.latest.revision: "51"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 6dba1b14498cef9e06d9bde5741cb9e37cd31633
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="select-transact-sql"></a>SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  从数据库中检索行，并启用的一个或多个行或从一个或多个表中的列选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 虽然 SELECT 语句的完整语法较复杂，但其主要子句可归纳如下：  
  
[ WITH { [ XMLNAMESPACES ,] [ \<common_table_expression> ] } ]
  
 SELECT *select_list* [ INTO *new_table* ]  
  
 [ FROM *table_source* ] [ WHERE *search_condition* ]  
  
 [ GROUP BY *group_by_expression* ]  
  
 [ HAVING *search_condition* ]  
  
 [ ORDER BY *order_expression* [ ASC | DESC ] ]  
  
 UNION、 EXCEPT 和 INTERSECT 运算符可以用于查询合并或比较其结果为一个结果集之间。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
<SELECT statement> ::=    
    [ WITH { [ XMLNAMESPACES ,] [ <common_table_expression> [,...n] ] } ]  
    <query_expression>   
    [ ORDER BY { order_by_expression | column_position [ ASC | DESC ] }   
  [ ,...n ] ]   
    [ <FOR Clause>]   
    [ OPTION ( <query_hint> [ ,...n ] ) ]   
<query_expression> ::=   
    { <query_specification> | ( <query_expression> ) }   
    [  { UNION [ ALL ] | EXCEPT | INTERSECT }  
        <query_specification> | ( <query_expression> ) [...n ] ]   
<query_specification> ::=   
SELECT [ ALL | DISTINCT ]   
    [TOP ( expression ) [PERCENT] [ WITH TIES ] ]   
    < select_list >   
    [ INTO new_table ]   
    [ FROM { <table_source> } [ ,...n ] ]   
    [ WHERE <search_condition> ]   
    [ <GROUP BY> ]   
    [ HAVING < search_condition > ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[ WITH <common_table_expression> [ ,...n ] ]  
SELECT <select_criteria>  
[;]  
  
<select_criteria> ::=  
    [ TOP ( top_expression ) ]   
    [ ALL | DISTINCT ]   
    { * | column_name | expression } [ ,...n ]   
    [ FROM { table_source } [ ,...n ] ]  
    [ WHERE <search_condition> ]   
    [ GROUP BY <group_by_clause> ]   
    [ HAVING <search_condition> ]   
    [ ORDER BY <order_by_expression> ]  
    [ OPTION ( <query_option> [ ,...n ] ) ]  
  
```  
  
## <a name="remarks"></a>注释  
 由于 SELECT 语句的复杂性，下面按子句说明详细的语法元素和参数：  
  
|||  
|-|-|  
|[WITH XMLNAMESPACES](../../t-sql/xml/with-xmlnamespaces.md)<br /><br /> [WITH common_table_expression](../../t-sql/queries/with-common-table-expression-transact-sql.md)|[HAVING](../../t-sql/queries/select-having-transact-sql.md)|  
|[SELECT 子句](../../t-sql/queries/select-clause-transact-sql.md)|[联合](../../t-sql/language-elements/set-operators-union-transact-sql.md)|  
|[INTO 子句](../../t-sql/queries/select-into-clause-transact-sql.md)|[EXCEPT 和 INTERSECT](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)|  
|[FROM](../../t-sql/queries/from-transact-sql.md)|[ORDER BY](../../t-sql/queries/select-order-by-clause-transact-sql.md)|  
|[WHERE](../../t-sql/queries/where-transact-sql.md)|[FOR 子句](../../t-sql/queries/select-for-clause-transact-sql.md)|  
|[分组依据](../../t-sql/queries/select-group-by-transact-sql.md)|[OPTION 子句](../../t-sql/queries/option-clause-transact-sql.md)|  
  
 SELECT 语句中的子句顺序非常重要。 可以省略可选子句，但这些子句在使用时必须按适当的顺序出现。  
  
 只有当这些语句的选择列表包含给函数的局部变量赋值的表达式时，在用户定义函数中才允许有 SELECT 语句。  
  
 因为的服务器名称部分可以用作表源，只要一个表名只能出现在 SELECT 语句中使用 OPENDATASOURCE 函数构造一个由四部分构成名称。 一个由四部分构成的名称不能为指定[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 某些应用于 SELECT 语句的语法限制涉及到远程表。  
  
## <a name="logical-processing-order-of-the-select-statement"></a>SELECT 语句的逻辑处理顺序  
 以下步骤显示 SELECT 语句的逻辑处理顺序（即绑定顺序）。 此顺序确定在一个步骤中定义的对象何时可用于后续步骤中的子句。 例如，如果查询处理器可以绑定到（访问）在 FROM 子句中定义的表或视图，则这些对象及其列可用于所有后续步骤。 相反，因为 SELECT 子句处于步骤 8，所以，在该子句中定义的任何列别名或派生列都无法被之前的子句引用。 不过，它们可由 ORDER BY 子句之类的后续子句引用。 该语句的实际物理执行由查询处理器，并从该列表的顺序可能会有所变化。  
  
1.  FROM  
2.  ON  
3.  JOIN  
4.  WHERE  
5.  GROUP BY  
6.  WITH CUBE 或 WITH ROLLUP  
7.  HAVING  
8.  SELECT  
9. DISTINCT  
10. ORDER BY  
11. 返回页首  

> [!WARNING]
> 上述顺序是通常如此。 但是，有个不同的序列可能不常见的情况。
>
> 例如，假设对视图，具有聚集的索引和视图不包括某些表行，并且该视图的所选列列表使用更改中的数据类型的转换*varchar*到*整数*。 在此情况下，可能在 WHERE 子句执行前执行转换。 常见确实。 通常是一种方法来修改视图以避免不同的序列中，如果它在你的示例很重要。 

## <a name="permissions"></a>权限  
 选择数据要求对表或视图具有 **SELECT** 权限，该权限可从更高级别的权限继承，例如针对架构的 **SELECT** 权限或针对表的 **CONTROL** 权限。 要求的成员身份或**db_datareader**或**db_owner**固定数据库角色的成员，或**sysadmin**固定的服务器角色。 创建新表使用**SELECTINTO**还要求同时**CREATETABLE**权限，与**ALTERSCHEMA**拥有新的表的架构的权限。  
  
## <a name="examples"></a>示例：   
下面的示例使用 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 数据库。
  
### <a name="a-using-select-to-retrieve-rows-and-columns"></a>A. 使用 SELECT 检索行和列  
 本部分说明了三个代码示例。 此第一个代码示例返回所有行 （没有 WHERE 子句中指定），所有列 (使用`*`) 从`DimEmployee`表。  
  
```sql  
SELECT *  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
 下一个示例使用表别名来实现相同的结果。  
  
```sql  
SELECT e.*  
FROM DimEmployee AS e  
ORDER BY LastName;  
```  
  
 此示例返回所有行 （没有 WHERE 子句中指定） 和列的子集 (`FirstName`， `LastName`， `StartDate`) 从`DimEmployee`表中`AdventureWorksPDW2012`数据库。 第三个列标题已重命名为`FirstDay`。  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
ORDER BY LastName;  
```  
  
 此示例返回仅的行`DimEmployee`具有`EndDate`不为 NULL 和`MaritalStatus`的是 （已婚）。  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
WHERE EndDate IS NOT NULL   
AND MaritalStatus = 'M'  
ORDER BY LastName;  
```  
  
### <a name="b-using-select-with-column-headings-and-calculations"></a>B. 将 SELECT 与列标题和列计算一起使用  
 下面的示例返回所有行从`DimEmployee`表，并为基于每个员工计算税前其`BaseRate`和 40 小时工作周。  
  
```sql  
SELECT FirstName, LastName, BaseRate, BaseRate * 40 AS GrossPay  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
### <a name="c-using-distinct-with-select"></a>C. 将 DISTINCT 与 SELECT 一起使用  
 下面的示例使用`DISTINCT`以便生成一个列表中的所有唯一标题`DimEmployee`表。  
  
```sql  
SELECT DISTINCT Title  
FROM DimEmployee  
ORDER BY Title;  
```  
  
### <a name="d-using-group-by"></a>D. 使用 GROUP BY  
 下面的示例查找每天所有销售的总金额。  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
 由于`GROUP BY`子句，只有一个包含所有销售额的总和的行返回的每一天。  
  
### <a name="e-using-group-by-with-multiple-groups"></a>E. 对多个组使用 GROUP BY  
 下面的示例查找平均价格和 Internet sales 总和的每一天，按订单日期和促销密钥分组。  
  
```sql  

SELECT OrderDateKey, PromotionKey, AVG(SalesAmount) AS AvgSales, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey, PromotionKey  
ORDER BY OrderDateKey;   
```  
  
### <a name="f-using-group-by-and-where"></a>F. 使用 GROUP BY 和 WHERE  
 下面的示例检索仅包含订单日期晚于 2002 年 8 月 1 日的行后将结果放入组。  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
WHERE OrderDateKey > '20020801'  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="g-using-group-by-with-an-expression"></a>G. 将 GROUP BY 与表达式一起使用  
 以下示例按表达式进行分组。 如果表达式不包含聚合函数，则可以按表达式进行分组。  
  
```sql  
SELECT SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY (OrderDateKey * 10);  
```  
  
### <a name="h-using-group-by-with-order-by"></a>H. 将 GROUP BY 与 ORDER BY 一起使用  
 下面的示例查找按天列出的每日和订单的销售额的总和。  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-the-having-clause"></a>I. 使用 HAVING 子句  
 此查询使用`HAVING`子句来限制结果。  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
HAVING OrderDateKey > 20010000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>另请参阅  
 [选择示例 &#40;Transact SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)  
 [提示 &#40;Transact SQL &#41;](../../t-sql/queries/hints-transact-sql.md)
  

