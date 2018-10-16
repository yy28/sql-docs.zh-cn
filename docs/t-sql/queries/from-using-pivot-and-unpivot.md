---
title: 使用 PIVOT 和 UNPIVOT | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PIVOT_TSQL
helpviewer_keywords:
- FROM clause, UNPIVOT operator
- unpivoting tables
- table pivoting [SQL Server]
- UNPIVOT operator
- crosstab query
- PIVOT operator
- rotating table-valued expressions
- pivoting tables
- FROM clause, PIVOT operator
- rotating columns
ms.assetid: 24ba54fc-98f7-4d35-8881-b5158aac1d66
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d07dc597f293414c2c4fae2704085ac4449038cf
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48905768"
---
# <a name="from---using-pivot-and-unpivot"></a>FROM - 使用 PIVOT 和 UNPIVOT
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  可以使用 `PIVOT` 和 `UNPIVOT` 关系运算符将表值表达式更改为另一个表。 `PIVOT` 通过将表达式某一列中的唯一值转换为输出中的多个列来旋转表值表达式，并在必要时对最终输出中所需的任何其余列值执行聚合。 `UNPIVOT` 与 PIVOT 执行相反的操作，将表值表达式的列转换为列值。  
  
 `PIVOT` 提供的语法比一系列复杂的 `SELECT...CASE` 语句中所指定的语法更简单和更具可读性。 有关 `PIVOT` 语法的完整说明，请参阅 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)。  
  
## <a name="syntax"></a>语法  
 以下语法总结了如何使用 `PIVOT` 运算符。  
  
```  
SELECT <non-pivoted column>,  
    [first pivoted column] AS <column name>,  
    [second pivoted column] AS <column name>,  
    ...  
    [last pivoted column] AS <column name>  
FROM  
    (<SELECT query that produces the data>)   
    AS <alias for the source query>  
PIVOT  
(  
    <aggregation function>(<column being aggregated>)  
FOR   
[<column that contains the values that will become column headers>]   
    IN ( [first pivoted column], [second pivoted column],  
    ... [last pivoted column])  
) AS <alias for the pivot table>  
<optional ORDER BY clause>;  
```  

## <a name="remarks"></a>Remarks  
`UNPIVOT` 子句中的列标识符需遵循目录排序规则。 对于 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，排序规则始终是 `SQL_Latin1_General_CP1_CI_AS`。 对于 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 部分包含的数据库，排序规则始终是 `Latin1_General_100_CI_AS_KS_WS_SC`。 如果将该列与与其他列合并，则需要 collate 子句 (`COLLATE DATABASE_DEFAULT`) 以避免冲突。  

  
## <a name="basic-pivot-example"></a>简单 PIVOT 示例  
 下面的代码示例生成一个两列四行的表。  
  
```sql
USE AdventureWorks2014 ;  
GO  
SELECT DaysToManufacture, AVG(StandardCost) AS AverageCost   
FROM Production.Product  
GROUP BY DaysToManufacture;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 DaysToManufacture AverageCost
 ----------------- -----------
 0                 5.0885
 1                 223.88
 2                 359.1082
 4                 949.4105
 ```
  
 没有定义 `DaysToManufacture` 为 3 的产品。  
  
 以下代码显示相同的结果，该结果经过透视以使 `DaysToManufacture` 值成为列标题。 提供一个列表示三 `[3]` 天，即使结果为 `NULL`。  
  
```sql
-- Pivot table with one row and five columns  
SELECT 'AverageCost' AS Cost_Sorted_By_Production_Days,   
[0], [1], [2], [3], [4]  
FROM  
(SELECT DaysToManufacture, StandardCost   
    FROM Production.Product) AS SourceTable  
PIVOT  
(  
AVG(StandardCost)  
FOR DaysToManufacture IN ([0], [1], [2], [3], [4])  
) AS PivotTable;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Cost_Sorted_By_Production_Days 0           1           2           3           4         
------------------------------ ----------- ----------- ----------- ----------- -----------
AverageCost                    5.0885      223.88      359.1082    NULL        949.4105
```
  
## <a name="complex-pivot-example"></a>复杂 PIVOT 示例  
 可能会用到 `PIVOT` 的常见情况是：需要生成交叉表格报表以汇总数据。 例如，假设需要在 `PurchaseOrderHeader` 示例数据库中查询 `AdventureWorks2014` 表以确定由某些特定雇员所下的采购订单数。 以下查询提供了此报表（按供应商排序）。  
  
```sql
USE AdventureWorks2014;  
GO  
SELECT VendorID, [250] AS Emp1, [251] AS Emp2, [256] AS Emp3, [257] AS Emp4, [260] AS Emp5  
FROM   
(SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM Purchasing.PurchaseOrderHeader) p  
PIVOT  
(  
COUNT (PurchaseOrderID)  
FOR EmployeeID IN  
( [250], [251], [256], [257], [260] )  
) AS pvt  
ORDER BY pvt.VendorID;  
```  
  
 以下为部分结果集。  
  
```
VendorID    Emp1        Emp2        Emp3        Emp4        Emp5  
----------- ----------- ----------- ----------- ----------- -----------
1492        2           5           4           4           4
1494        2           5           4           5           4
1496        2           4           4           5           5
1498        2           5           4           4           4
1500        3           4           4           5           4
```
  
 将在 `EmployeeID` 列上透视此嵌套 select 语句返回的结果。  
  
```sql
SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM PurchaseOrderHeader;  
```  
  
 这意味着 `EmployeeID` 列返回的唯一值自行变成了最终结果集中的字段。 因此，在透视子句中指定的每个 `EmployeeID` 号都有相应的一列：在本例中为雇员 `164`、`198`、`223`、`231` 和 `233`。 `PurchaseOrderID` 列作为值列，将根据此列对最终输出中返回的列（称为分组列）进行分组。 在本例中，通过 `COUNT` 函数聚合分组列。 请注意，将显示一条警告消息，指出为每个雇员计算 `PurchaseOrderID` 时未考虑显示在 `COUNT` 列中的任何空值。  
  
> [!IMPORTANT]  
>  如果聚合函数与 `PIVOT` 一起使用，则计算聚合时将不考虑出现在值列中的任何空值。  
  
 `UNPIVOT` 将与 `PIVOT` 执行几乎完全相反的操作，将列转换为行。 假设以上示例中生成的表在数据库中存储为 `pvt`，并且您需要将列标识符 `Emp1`、`Emp2`、`Emp3`、`Emp4` 和 `Emp5` 旋转为对应于特定供应商的行值。 这意味着必须标识另外两个列。 包含要旋转的列值（`Emp1`、`Emp2`...）的列将被称为 `Employee`，将保存当前位于待旋转列下的值的列被称为 `Orders`。 这些列分别对应于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 定义中的 pivot_column 和 value_column。 以下为该查询。  
  
```sql
-- Create the table and insert values as portrayed in the previous example.  
CREATE TABLE pvt (VendorID int, Emp1 int, Emp2 int,  
    Emp3 int, Emp4 int, Emp5 int);  
GO  
INSERT INTO pvt VALUES (1,4,3,5,4,4);  
INSERT INTO pvt VALUES (2,4,1,5,5,5);  
INSERT INTO pvt VALUES (3,4,3,5,4,4);  
INSERT INTO pvt VALUES (4,4,2,5,5,4);  
INSERT INTO pvt VALUES (5,5,1,5,5,5);  
GO  
-- Unpivot the table.  
SELECT VendorID, Employee, Orders  
FROM   
   (SELECT VendorID, Emp1, Emp2, Emp3, Emp4, Emp5  
   FROM pvt) p  
UNPIVOT  
   (Orders FOR Employee IN   
      (Emp1, Emp2, Emp3, Emp4, Emp5)  
)AS unpvt;  
GO  
```  
  
 以下为部分结果集。  
  
```
VendorID    Employee    Orders
----------- ----------- ------
1            Emp1       4
1            Emp2       3 
1            Emp3       5
1            Emp4       4
1            Emp5       4
2            Emp1       4
2            Emp2       1
2            Emp3       5
2            Emp4       5
2            Emp5       5
...
```
  
 请注意，`UNPIVOT` 并不完全是 `PIVOT` 的逆操作。 `PIVOT` 会执行一次聚合，从而将多个可能的行合并为输出中的单个行。 而 `UNPIVOT` 不会重现原始表值表达式的结果，因为行已经被合并了。 另外，`UNPIVOT` 的输入中的 null 值不会显示在输出中，而在执行 `PIVOT` 操作之前，输入中可能有原始的 null 值。  
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库中的 `Sales.vSalesPersonSalesByFiscalYears` 视图将使用 `PIVOT` 返回每个销售人员在每个会计年度的总销售额。 若要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中编写视图脚本，请在“对象资源管理器”中的“视图”文件夹下找到 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库对应的视图。 右键单击该视图名称，再选择“编写视图脚本为”。  
  
## <a name="see-also"></a>另请参阅  
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [CASE (Transact-SQL)](../../t-sql/language-elements/case-transact-sql.md)  
  
  
