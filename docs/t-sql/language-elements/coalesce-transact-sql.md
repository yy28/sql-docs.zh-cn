---
title: "将合并 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/30/2017
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
- COALESCE
- COALESCE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- expressions [SQL Server], nonnull
- COALESCE function
- first nonnull expressions [SQL Server]
- nonnull expressions
ms.assetid: fafc0dba-f8a8-4aad-9b7f-908e34b74d88
caps.latest.revision: "52"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: fddb9a8535472c153adf036b5afed9584cfbd3d7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="coalesce-transact-sql"></a>COALESCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

计算自变量的顺序并返回最初计算结果不是第一个表达式的当前值`NULL`。 例如，`SELECT COALESCE(NULL, NULL, 'third_value', 'fourth_value');`返回的第三个值，因为第三个值是第一个不为 null 的值。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
COALESCE ( expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何类型。  
  
## <a name="return-types"></a>返回类型  
 返回的数据类型*表达式*具有最高的数据类型优先级。 如果所有表达式都不可为 Null，则结果的类型也不可为 Null。  
  
## <a name="remarks"></a>注释  
 如果所有参数都均`NULL`，`COALESCE`返回`NULL`。 至少一个 null 值必须是类型化`NULL`。  
  
## <a name="comparing-coalesce-and-case"></a>比较 COALESCE 和 CASE  
 `COALESCE`表达式是的语法快捷方式`CASE`表达式。  即代码`COALESCE`(*expression1*，*...n*) 重写的查询优化器按如下所示`CASE`表达式：  
  
 ```sql  
 CASE  
 WHEN (expression1 IS NOT NULL) THEN expression1  
 WHEN (expression2 IS NOT NULL) THEN expression2  
 ...  
 ELSE expressionN  
 END  
 ```  
  
 这意味着，输入的值 (*expression1*， *expression2*，*表达式*等) 计算多次。 此外，为了符合 SQL 标准，包含子查询的值表达式被视为不确定的且子查询被计算两次。 在每种情况中，第一次计算和后续计算可能返回不同的结果。  
  
 例如，执行代码 `COALESCE((subquery), 1)` 时，计算子查询两次。 因此，您可能得到不同的结果，具体取决于查询的隔离级别。 例如，代码可以返回`NULL`下`READ COMMITTED`多用户环境中的隔离级别。 若要确保稳定的结果返回，使用`SNAPSHOT ISOLATION`隔离级别或替换`COALESCE`与`ISNULL`函数。 或者，您可以重新编写查询以将子查询推入嵌套 select 语句，如下面的示例中所示：  
  
```sql  
SELECT CASE WHEN x IS NOT NULL THEN x ELSE 1 END  
from  
(  
SELECT (SELECT Nullable FROM Demo WHERE SomeCol = 1) AS x  
) AS T;  
  
```  
  
## <a name="comparing-coalesce-and-isnull"></a>比较 COALESCE 和 ISNULL  
 `ISNULL`函数和`COALESCE`表达式具有类似的目的，但可以以不同方式行为。  
  
1.  因为`ISNULL`是一个函数，它只计算一次。  如上所述，输入值`COALESCE`表达式可计算多次。  
  
2.  确定结果表达式的数据类型方式不同。 `ISNULL`使用的第一个参数的数据类型`COALESCE`遵循`CASE`表达式规则，并返回具有最高优先级的值的数据类型。  
  
3.  结果表达式的为 Null 是不同的`ISNULL`和`COALESCE`。 `ISNULL`返回值始终被认为是不可以为 Null （假定返回的值一个不可为 null） 而`COALESCE`具有非 null 参数被视为可`NULL`。 因此表达式`ISNULL(NULL, 1)`和`COALESCE(NULL, 1)`，等效，但具有不同可为 null 值。 如果你在计算列中使用这些表达式，创建键约束或使的标量 UDF 的返回值的确定性，以便可以在下面的示例所示进行索引，这会有所不同：  
  
    ```sql  
    USE tempdb;  
    GO  
    -- This statement fails because the PRIMARY KEY cannot accept NULL values  
    -- and the nullability of the COALESCE expression for col2   
    -- evaluates to NULL.  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0) PRIMARY KEY,   
    col3 AS ISNULL(col1, 0)   
    );   
  
    -- This statement succeeds because the nullability of the   
    -- ISNULL function evaluates AS NOT NULL.  
  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0),   
    col3 AS ISNULL(col1, 0) PRIMARY KEY   
    );  
    ```  
  
4.  验证`ISNULL`和`COALESCE`还有不同。 例如，`NULL`值`ISNULL`转换为**int**而为`COALESCE`，你必须提供一种数据类型。  
  
5.  `ISNULL`采用只有两个参数，而`COALESCE`采用数量可变的参数。  
  
## <a name="examples"></a>示例  
  
### <a name="a-running-a-simple-example"></a>A. 运行简单示例  
 下面的示例演示 `COALESCE` 如何从第一个具有非 Null 值的列中选择数据。 此示例使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库。  
  
```sql  
SELECT Name, Class, Color, ProductNumber,  
COALESCE(Class, Color, ProductNumber) AS FirstNotNull  
FROM Production.Product;  
```  
  
### <a name="b-running-a-complex-example"></a>B. 运行复杂示例  
 在以下示例中，`wages` 表中包括以下三列，它们包含有关雇员的年薪的信息：hourly wage、salary 和 commission。 但是，每个雇员只能接受一种付款方式。 若要确定支付给所有雇员的金额总数，请使用 `COALESCE` 仅接受在 `hourly_wage`、`salary` 和 `commission` 中找到的非 Null 值。  
  
```sql  
SET NOCOUNT ON;  
GO  
USE tempdb;  
IF OBJECT_ID('dbo.wages') IS NOT NULL  
    DROP TABLE wages;  
GO  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   identity,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
GO  
INSERT dbo.wages (hourly_wage, salary, commission, num_sales)  
VALUES  
    (10.00, NULL, NULL, NULL),  
    (20.00, NULL, NULL, NULL),  
    (30.00, NULL, NULL, NULL),  
    (40.00, NULL, NULL, NULL),  
    (NULL, 10000.00, NULL, NULL),  
    (NULL, 20000.00, NULL, NULL),  
    (NULL, 30000.00, NULL, NULL),  
    (NULL, 40000.00, NULL, NULL),  
    (NULL, NULL, 15000, 3),  
    (NULL, NULL, 25000, 2),  
    (NULL, NULL, 20000, 6),  
    (NULL, NULL, 14000, 4);  
GO  
SET NOCOUNT OFF;  
GO  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS money) AS 'Total Salary'   
FROM dbo.wages  
ORDER BY 'Total Salary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Total Salary  
 ------------  
 10000.00  
 20000.00  
 20800.00  
 30000.00  
 40000.00  
 41600.00  
 45000.00  
 50000.00  
 56000.00  
 62400.00  
 83200.00  
 120000.00  
  
 (12 row(s) affected)
 ```  
  
### <a name="c-simple-example"></a>C： 简单的示例  
 下面的示例演示如何`COALESCE`从具有非 null 值的第一列中选择数据。 对于此示例假定，`Products`表包含此数据：  
  
 ```  
 Name         Color      ProductNumber  
 ------------ ---------- -------------  
 Socks, Mens  NULL       PN1278  
 Socks, Mens  Blue       PN1965  
 NULL         White      PN9876
 ```  
  
 我们然后运行以下 COALESCE 查询：  
  
```sql  
SELECT Name, Color, ProductNumber, COALESCE(Color, ProductNumber) AS FirstNotNull   
FROM Products ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Name         Color      ProductNumber  FirstNotNull  
 ------------ ---------- -------------  ------------  
 Socks, Mens  NULL       PN1278         PN1278  
 Socks, Mens  Blue       PN1965         Blue  
 NULL         White      PN9876         White
 ```  
  
 请注意，在第一行中，`FirstNotNull`值是`PN1278`，而不`Socks, Mens`。 这是因为`Name`的参数未指定列`COALESCE`在示例中。  
  
### <a name="d-complex-example"></a>D： 复杂的示例  
 下面的示例使用`COALESCE`比较三个列中的值并返回列中找到的非 null 值。  
  
```sql  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   NULL,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (1, 10.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (2, 20.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (3, 30.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (4, 40.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (5, NULL, 10000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (6, NULL, 20000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (7, NULL, 30000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (8, NULL, 40000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (9, NULL, NULL, 15000, 3);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (10,NULL, NULL, 25000, 2);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (11, NULL, NULL, 20000, 6);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (12, NULL, NULL, 14000, 4);  
  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS decimal(10,2)) AS TotalSalary   
FROM dbo.wages  
ORDER BY TotalSalary;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Total Salary  
 ------------  
 10000.00  
 20000.00  
 20800.00  
 30000.00  
 40000.00  
 41600.00  
 45000.00  
 50000.00  
 56000.00  
 62400.00  
 83200.00  
 120000.00
 ```  
  
## <a name="see-also"></a>另请参阅  
 [ISNULL &#40;Transact SQL &#41;](../../t-sql/functions/isnull-transact-sql.md)   
 [CASE (Transact-SQL)](../../t-sql/language-elements/case-transact-sql.md)  
  
  
