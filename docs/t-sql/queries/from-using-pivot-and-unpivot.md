---
title: "使用透视和逆透视 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PIVOT_TSQL
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
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5ee91826fe19979d411c10baf2ab4c60f225d0bb
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="from---using-pivot-and-unpivot"></a>从-使用数据透视和逆透视
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  你可以使用`PIVOT`和`UNPIVOT`关系运算符，若要更改到另一个表的表值的表达式。 `PIVOT`将表值的表达式旋转到多个列在输出中，表达式中打开某一列中的唯一值，并执行聚合中需要的任何想最终输出中的剩余列值。 `UNPIVOT`通过旋转列到列的值的表值表达式中执行相反操作为透视。  
  
 语法`PIVOT`提供更简单且更具可读性，否则可能在一系列复杂的中指定的语法比`SELECT...CASE`语句。 有关语法的完整说明`PIVOT`，请参阅[(Transact SQL) 从](../../t-sql/queries/from-transact-sql.md)。  
  
## <a name="syntax"></a>语法  
 以下语法总结了如何使用`PIVOT`运算符。  
  
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

## <a name="remarks"></a>注释  
中的列标识符`UNPIVOT`子句按照目录排序规则。 有关[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，排序规则是始终`SQL_Latin1_General_CP1_CI_AS`。 有关[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]部分包含的数据库，排序规则是始终`Latin1_General_100_CI_AS_KS_WS_SC`。 如果与其他列，然后 collate 子句结合使用的列 (`COLLATE DATABASE_DEFAULT`) 要求，以避免冲突。  

  
## <a name="basic-pivot-example"></a>简单 PIVOT 示例  
 下面的代码示例生成一个两列四行的表。  
  
```  
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
  
```  
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
  
```  
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
  
```  
SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM PurchaseOrderHeader;  
```  
  
 这意味着 `EmployeeID` 列返回的唯一值自行变成了最终结果集中的字段。 因此，在透视子句中指定的每个 `EmployeeID` 号都有相应的一列：在本例中为雇员 `164`、`198`、`223`、`231` 和 `233`。 `PurchaseOrderID` 列作为值列，将根据此列对最终输出中返回的列（称为分组列）进行分组。 在本例中，通过 `COUNT` 函数聚合分组列。 请注意，将显示一条警告消息，指出为每个雇员计算 `PurchaseOrderID` 时未考虑显示在 `COUNT` 列中的任何空值。  
  
> [!IMPORTANT]  
>  当与使用聚合函数`PIVOT`，计算一个聚合时，不会考虑在值列中所有 null 值的状态。  
  
 `UNPIVOT`执行的反向操作几乎`PIVOT`，通过旋转到行的列。 假设以上示例中生成的表在数据库中存储为 `pvt`，并且您需要将列标识符 `Emp1`、`Emp2`、`Emp3`、`Emp4` 和 `Emp5` 旋转为对应于特定供应商的行值。 这意味着必须标识另外两个列。 包含要旋转的列值（`Emp1`、`Emp2`...）的列将被称为 `Employee`，将保存当前位于待旋转列下的值的列被称为 `Orders`。 这些列对应于*pivot_column*和*value_column*分别在[!INCLUDE[tsql](../../includes/tsql-md.md)]定义。 以下为该查询。  
  
```  
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
  
 请注意，`UNPIVOT`不是完全相反的`PIVOT`。 `PIVOT`执行聚合，并因此，可能多个会将行合并为单个行在输出中。 `UNPIVOT`因为行有合并，则不会重现原始表值的表达式的结果。 此外，null 值的输入中`UNPIVOT`消失在输出中，而可能进行了原始的 null 值的输入`PIVOT`操作。  
  
 `Sales.vSalesPersonSalesByFiscalYears`中查看[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]示例数据库使用`PIVOT`要为每个会计年度中返回每个销售人员的总销售额。 若要编写脚本中的视图[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中**对象资源管理器**，找到下的视图**视图**文件夹[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库。 右键单击该视图名称，然后选择**视图脚本为**。  
  
## <a name="see-also"></a>另请参阅  
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [CASE (Transact-SQL)](../../t-sql/language-elements/case-transact-sql.md)  
  
  
