---
title: "级别 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/25/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RANK
- RANK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row ranking [SQL Server]
- tied rows [SQL Server]
- ranking rows
- RANK function [Transact-SQL]
ms.assetid: 2d96f6d2-5db7-4b3c-a63e-213c58e4af55
caps.latest.revision: 62
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 304ceaedefe1755c56b27a8f6e64a922a1986bc0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="rank-transact-sql"></a>RANK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回结果集的分区内每行的排名。 行的排名是相关行之前的排名数加一。  

  方式和级别很相似。 所有的方式数字按顺序行 （例如 1、 2、 3、 4、 5）。 级别对于版本号 （例如 1、 2、 2、 4、 5） 提供的数值相同。   
  
> [!NOTE]
> 级别是临时值计算运行查询时。 若要保存在表中的数字，请参阅[标识属性](../../t-sql/statements/create-table-transact-sql-identity-property.md)和[序列](../../t-sql/statements/create-sequence-transact-sql.md)。 
   
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
RANK ( ) OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
## <a name="arguments"></a>参数  
 通过**(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause*将划分为分区函数应用到的 FROM 子句生成的结果集。 如果未指定，则此函数将查询结果集的所有行视为单个组。 *order_by_clause*应用函数之前确定数据的顺序。 *Order_by_clause*是必需的。 \<行或 range 子句 > 的 OVER 子句不能为指定排名函数。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>返回类型  
 **bigint**  
  
## <a name="remarks"></a>注释  
 如果两个或多个行与一个排名关联，则每个关联行将得到相同的排名。 例如，如果两位顶尖销售员具有相同的 SalesYTD 值，则他们将并列第一。 由于已有两行排名在前，所以具有下一个最大 SalesYTD 的销售人员将排名第三。 因此，RANK 函数并不总返回连续整数。  
  
 用于整个查询的排序顺序决定了行在结果集中的显示顺序。  
  
 RANK 具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-ranking-rows-within-a-partition"></a>A. 对分区中的行进行排名  
 以下示例按照数量对指定清单位置的清单中的产品进行了排名。 结果集按 `LocationID` 分区并在逻辑上按 `Quantity` 排序。 注意，产品 494 和 495 具有相同的数量。 因为它们是关联的，所以两者均排名第一。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT i.ProductID, p.Name, i.LocationID, i.Quantity  
    ,RANK() OVER   
    (PARTITION BY i.LocationID ORDER BY i.Quantity DESC) AS Rank  
FROM Production.ProductInventory AS i   
INNER JOIN Production.Product AS p   
    ON i.ProductID = p.ProductID  
WHERE i.LocationID BETWEEN 3 AND 4  
ORDER BY i.LocationID;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
ProductID   Name                   LocationID   Quantity Rank  
----------- ---------------------- ------------ -------- ----  
494         Paint - Silver         3            49       1  
495         Paint - Blue           3            49       1  
493         Paint - Red            3            41       3  
496         Paint - Yellow         3            30       4  
492         Paint - Black          3            17       5  
495         Paint - Blue           4            35       1  
496         Paint - Yellow         4            25       2  
493         Paint - Red            4            24       3  
492         Paint - Black          4            14       4  
494         Paint - Silver         4            12       5  
 (10 row(s) affected)  
```  
  
### <a name="b-ranking-all-rows-in-a-result-set"></a>B. 对结果集中的所有行排名  
 下面的示例返回按薪金排名的前十名员工。 因为未指定 PARTITION BY 子句，所以，RANK 函数应用于结果集中的所有行。  
  
```  
USE AdventureWorks2012  
SELECT TOP(10) BusinessEntityID, Rate,   
       RANK() OVER (ORDER BY Rate DESC) AS RankBySalary  
FROM HumanResources.EmployeePayHistory AS eph1  
WHERE RateChangeDate = (SELECT MAX(RateChangeDate)   
                        FROM HumanResources.EmployeePayHistory AS eph2  
                        WHERE eph1.BusinessEntityID = eph2.BusinessEntityID)  
ORDER BY BusinessEntityID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID Rate                  RankBySalary  
---------------- --------------------- --------------------  
1                125.50                1  
2                63.4615               4  
3                43.2692               8  
4                29.8462               19  
5                32.6923               16  
6                32.6923               16  
7                50.4808               6  
8                40.8654               10  
9                40.8654               10  
10               42.4808               9  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-ranking-rows-within-a-partition"></a>C： 在一个分区内的排名行  
 下面的示例在其总销售额根据每个销售区域排名销售代表。 行集按 `SalesTerritoryGroup` 分区，按 `SalesAmountQuota` 排序。  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `LastName          TotalSales     SalesTerritoryGroup  RankResult`  
  
 `----------------  -------------  -------------------  --------`  
  
 `Tsoflias          1687000.0000   Australia            1`  
  
 `Saraiva           7098000.0000   Canada               1`  
  
 `Vargas            4365000.0000   Canada               2`  
  
 `Carson            12198000.0000  Central              1`  
  
 `Varkey Chudukatil 5557000.0000   France               1`  
  
 `Valdez            2287000.0000   Germany              1`  
  
 `Blythe            11162000.0000  Northeast            1`  
  
 `Campbell          4025000.0000   Northwest            1`  
  
 `Ansman-Wolfe      3551000.0000   Northwest            2`  
  
 `Mensa-Annan       2753000.0000   Northwest            3`  
  
 `Reiter            8541000.0000   Southeast            1`  
  
 `Mitchell          11786000.0000  Southwest            1`  
  
 `Ito               7804000.0000   Southwest            2`  
  
 `Pak               10514000.0000  United Kingdom       1`  
  
## <a name="see-also"></a>另请参阅  
 [DENSE_RANK &#40;Transact SQL &#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [方式 &#40;Transact SQL &#41;](../../t-sql/functions/row-number-transact-sql.md)   
 [NTILE &#40;Transact SQL &#41;](../../t-sql/functions/ntile-transact-sql.md)   
 [排名函数 &#40;Transact SQL &#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)  
  
  




