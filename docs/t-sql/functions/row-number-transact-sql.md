---
title: "方式 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROW_NUMBER
- ROW_NUMBER_TSQL
- ROW_NUMBER()_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ROW_NUMBER function
- row numbers [SQL Server]
- sequential row numbers [SQL Server]
ms.assetid: 82fa9016-77db-4b42-b4c8-df6095b81906
caps.latest.revision: "50"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 6ddb3472f19ce2fda8bc368cd07f7ea602d74a02
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="rownumber-transact-sql"></a>ROW_NUMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  设置数字结果的输出。 更具体地说，返回的顺序中分区的结果集，从每个分区中的第一行的 1 开始的行数。 
  
`ROW_NUMBER`和`RANK`类似。 `ROW_NUMBER`所有数字按顺序都行 （例如 1、 2、 3、 4、 5）。 `RANK`对于版本号 （例如 1、 2、 2、 4、 5） 提供的数值相同。   
  
> [!NOTE]
> `ROW_NUMBER`运行查询时计算的临时值。 若要保存在表中的数字，请参阅[标识属性](../../t-sql/statements/create-table-transact-sql-identity-property.md)和[序列](../../t-sql/statements/create-sequence-transact-sql.md)。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
  
## <a name="syntax"></a>语法  
  
```  
ROW_NUMBER ( )   
    OVER ( [ PARTITION BY value_expression , ... [ n ] ] order_by_clause )  
```  
  
## <a name="arguments"></a>参数  
 PARTITION BY *value_expression*  
 将通过生成的结果集划分[FROM](../../t-sql/queries/from-transact-sql.md)方式函数应用到分区到子句。 *value_expression*指定结果集进行分区所依据的列。 如果`PARTITION BY`未指定，则该函数将所有行的查询结果集作为一个组。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 *order_by_clause*  
 `ORDER BY`子句用于确定其唯一分配利用行序列`ROW_NUMBER`中指定的分区。 它是必需的。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>返回类型  
 **bigint**  
  
## <a name="general-remarks"></a>一般备注  
 返回的行不能保证查询使用`ROW_NUMBER()`将进行排序完全相同，但有每次执行除非下列条件为真。  
  
1.  分区列的值是唯一的。  
  
2.  值的`ORDER BY`列是唯一的。  
  
3.  分区列的值的组合和`ORDER BY`列是唯一的。  
  
 `ROW_NUMBER()`具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-examples"></a>A. 简单的示例 

以下查询按字母顺序返回四个系统表。

```sql
SELECT 
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5
ORDER BY name ASC;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|NAME    |recovery_model_desc |  
|-----------  |------------ |  
|master |SIMPLE |
|model |FULL |
|msdb |SIMPLE |
|tempdb |SIMPLE |

若要添加的每一行的前面行号列，添加具有的列`ROW_NUMBER`函数，在这种情况下名为`Row#`。 你必须将移动`ORDER BY`达子句`OVER`子句。

```sql
SELECT 
  ROW_NUMBER() OVER(ORDER BY name ASC) AS Row#,
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|行号 |NAME    |recovery_model_desc |  
|------- |-----------  |------------ |  
|@shouldalert |master |SIMPLE |
|2 |model |FULL |
|3 |msdb |SIMPLE |
|4 |tempdb |SIMPLE |

添加`PARTITION BY`上的子句`recovery_model_desc`列中，将重新启动时的编号`recovery_model_desc`值更改。 
 
```sql
SELECT 
  ROW_NUMBER() OVER(PARTITION BY recovery_model_desc ORDER BY name ASC) 
    AS Row#,
  name, recovery_model_desc
FROM sys.databases WHERE database_id < 5;
```  

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|行号 |NAME    |recovery_model_desc |  
|------- |-----------  |------------ |  
|@shouldalert |model |FULL |
|@shouldalert |master |SIMPLE |
|2 |msdb |SIMPLE |
|3 |tempdb |SIMPLE |


### <a name="b-returning-the-row-number-for-salespeople"></a>B. 返回销售人员的行号  
 以下示例根据销售人员年初至今的销售额，计算 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 中销售人员的行号。  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT ROW_NUMBER() OVER(ORDER BY SalesYTD DESC) AS Row,   
    FirstName, LastName, ROUND(SalesYTD,2,1) AS "Sales YTD"   
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Row FirstName    LastName               SalesYTD  
--- -----------  ---------------------- -----------------  
1   Linda        Mitchell               4251368.54  
2   Jae          Pak                    4116871.22  
3   Michael      Blythe                 3763178.17  
4   Jillian      Carson                 3189418.36  
5   Ranjit       Varkey Chudukatil      3121616.32  
6   José         Saraiva                2604540.71  
7   Shu          Ito                    2458535.61  
8   Tsvi         Reiter                 2315185.61  
9   Rachel       Valdez                 1827066.71  
10  Tete         Mensa-Annan            1576562.19  
11  David        Campbell               1573012.93  
12  Garrett      Vargas                 1453719.46  
13  Lynn         Tsoflias               1421810.92  
14  Pamela       Ansman-Wolfe           1352577.13  
```  
  
### <a name="c-returning-a-subset-of-rows"></a>C. 返回行的子集  
 下面的示例按 `SalesOrderHeader` 的顺序计算 `OrderDate` 表中所有行的行号，并只返回行 `50` 到 `60`（含）。  
  
```sql  
USE AdventureWorks2012;  
GO  
WITH OrderedOrders AS  
(  
    SELECT SalesOrderID, OrderDate,  
    ROW_NUMBER() OVER (ORDER BY OrderDate) AS RowNumber  
    FROM Sales.SalesOrderHeader   
)   
SELECT SalesOrderID, OrderDate, RowNumber    
FROM OrderedOrders   
WHERE RowNumber BETWEEN 50 AND 60;  
```  
  
### <a name="d-using-rownumber-with-partition"></a>D. 将 ROW_NUMBER () 与 PARTITION 一起使用  
 以下示例使用 `PARTITION BY` 参数按列 `TerritoryName` 对结果集进行分区。 在 `ORDER BY` 子句中指定的 `OVER` 子句按列 `SalesYTD` 对每个分区中的行进行排序。 `ORDER BY` 语句中的 `SELECT` 按 `TerritoryName` 子句对整个查询结果集进行排序。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FirstName, LastName, TerritoryName, ROUND(SalesYTD,2,1) AS SalesYTD,  
ROW_NUMBER() OVER(PARTITION BY TerritoryName ORDER BY SalesYTD DESC) 
  AS Row  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0  
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
FirstName  LastName             TerritoryName        SalesYTD      Row  
---------  -------------------- ------------------   ------------  ---  
Lynn       Tsoflias             Australia            1421810.92    1  
José       Saraiva              Canada               2604540.71    1  
Garrett    Vargas               Canada               1453719.46    2  
Jillian    Carson               Central              3189418.36    1  
Ranjit     Varkey Chudukatil    France               3121616.32    1  
Rachel     Valdez               Germany              1827066.71    1  
Michael    Blythe               Northeast            3763178.17    1  
Tete       Mensa-Annan          Northwest            1576562.19    1  
David      Campbell             Northwest            1573012.93    2  
Pamela     Ansman-Wolfe         Northwest            1352577.13    3  
Tsvi       Reiter               Southeast            2315185.61    1  
Linda      Mitchell             Southwest            4251368.54    1  
Shu        Ito                  Southwest            2458535.61    2  
Jae        Pak                  United Kingdom       4116871.22    1  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-returning-the-row-number-for-salespeople"></a>E. 返回销售人员的行号  
 下面的示例返回`ROW_NUMBER`销售代表基于其分配的销售定额。  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(ORDER BY SUM(SalesAmountQuota) DESC) 
    AS RowNumber,  
    FirstName, LastName,   
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName;  
```  
  
 以下为部分结果集。  

```  

RowNumber  FirstName  LastName            SalesQuota  
---------  ---------  ------------------  -------------  
1          Jillian    Carson              12,198,000.00  
2          Linda      Mitchell            11,786,000.00  
3          Michael    Blythe              11,162,000.00  
4          Jae        Pak                 10,514,000.00  
```

### <a name="f-using-rownumber-with-partition"></a>F. 将 ROW_NUMBER () 与 PARTITION 一起使用  
 以下示例显示了将 `ROW_NUMBER` 函数与 `PARTITION BY` 参数结合使用的情况。 这将导致`ROW_NUMBER`函数对行进行编号每个分区中。  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(PARTITION BY SalesTerritoryKey 
        ORDER BY SUM(SalesAmountQuota) DESC) AS RowNumber,  
    LastName, SalesTerritoryKey AS Territory,  
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName, SalesTerritoryKey;  
```  
  
 以下为部分结果集。  
 
```  
 
RowNumber  LastName            Territory  SalesQuota  
---------  ------------------  ---------  -------------  
1          Campbell            1           4,025,000.00  
2          Ansman-Wolfe        1           3,551,000.00  
3          Mensa-Annan         1           2,275,000.00  
1          Blythe              2          11,162,000.00  
1          Carson              3          12,198,000.00  
1          Mitchell            4          11,786,000.00  
2          Ito                 4           7,804,000.00  
```
  
## <a name="see-also"></a>另请参阅  
 [级别 &#40;Transact SQL &#41;](../../t-sql/functions/rank-transact-sql.md)   
 [DENSE_RANK &#40;Transact SQL &#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [NTILE &#40;Transact SQL &#41;](../../t-sql/functions/ntile-transact-sql.md)  
  
  


