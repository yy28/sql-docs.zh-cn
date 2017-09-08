---
title: "子查询 （Azure SQL 数据仓库，并行数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e8ebd60-1936-48c9-b2b9-e099c8269fcf
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 351d559bde6300d9f746d68a802ae0a61202f8b8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="subqueries-azure-sql-data-warehouse-parallel-data-warehouse"></a>子查询 （Azure SQL 数据仓库，并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  本主题提供了使用中的子查询的示例[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
 SELECT 语句中，请参阅[选择 &#40;Transact SQL &#41;](../../t-sql/queries/select-transact-sql.md)  
  
## <a name="contents"></a>目录  
  
-   [基础知识](#Basics)  
  
-   [示例： SQL 数据仓库和并行数据仓库](#Examples)  
  
##  <a name="Basics"></a>基础知识  
 子查询  
 子查询是一个嵌套在 SELECT、INSERT、UPDATE 或 DELETE 语句或其他子查询中的查询。 这也称为内部查询或内部的选择。  
  
 外部查询  
 包含子查询语句。 这也称为外部的选择。  
  
 相关子查询  
 外部查询中的表是指子查询。  
  
##  <a name="Examples"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 本部分提供的子查询中支持示例[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
### <a name="a-top-and-order-by-in-a-subquery"></a>A. TOP 和 ORDER BY 在子查询  
  
```  
SELECT * FROM tblA  
WHERE col1 IN  
    (SELECT TOP 100 col1 FROM tblB ORDER BY col1);  
  
```  
  
### <a name="b-having-clause-with-a-correlated-subquery"></a>B. HAVING 子句与相关子查询  
  
```  
SELECT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
GROUP BY dm.EmployeeKey, dm.FirstName, dm.LastName  
HAVING 5000 <=   
(SELECT sum(OrderQuantity)  
FROM FactResellerSales AS frs  
WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
  
```  
  
### <a name="c-correlated-subqueries-with-analytics"></a>C. 使用分析相关子查询  
  
```  
SELECT * FROM ReplA AS A   
WHERE A.ID IN   
    (SELECT sum(B.ID2) OVER() FROM ReplB AS B WHERE A.ID2 = B.ID);  
```  
  
### <a name="d-correlated-union-statements-in-a-subquery"></a>D. 在子查询的相关 union 语句  
  
```  
SELECT * FROM RA   
WHERE EXISTS   
    (SELECT 1 FROM RB WHERE RB.b1 = RA.a1   
     UNION ALL SELECT 1 FROM RC);  
```  
  
### <a name="e-join-predicates-in-a-subquery"></a>E. 在子查询中联接谓词  
  
```  
SELECT * FROM RA INNER JOIN RB   
    ON RA.a1 = (SELECT COUNT(*) FROM RC);  
```  
  
### <a name="f-correlated-join-predicates-in-a-subquery"></a>F. 在子查询相关的联接谓词  
  
```  
SELECT * FROM RA   
    WHERE RA.a2 IN   
    (SELECT 1 FROM RB INNER JOIN RC ON RA.a1=RB.b1+RC.c1);  
```  
  
### <a name="g-correlated-subselects-as-data-sources"></a>G. 作为数据源的相关嵌套 select 语句  
  
```  
SELECT * FROM RA   
    WHERE 3 = (SELECT COUNT(*)   
        FROM (SELECT b1 FROM RB WHERE RB.b1 = RA.a1) X);  
```  
  
### <a name="h-correlated-subqueries-in-the-data-values--used-with-aggregates"></a>H. 中用于聚合的数据值的相关子查询  
  
```  
SELECT Rb.b1, (SELECT RA.a1 FROM RA WHERE RB.b1 = RA.a1) FROM RB GROUP BY RB.b1;  
```  
  
### <a name="i-using-in-with-a-correlated-subquery"></a>I. 使用使用相关子查询  
 以下示例在相关或重复子查询中使用 `IN`。 该查询依赖于外部查询来查询其值。 重复运行内部查询，每个行的一次，可以选择由外部查询。 此查询检索的一个实例`EmployeeKey`加上为其每个雇员的第一个和最后一个名称`OrderQuantity`中`FactResellerSales`表是`5`和中匹配的雇员标识号`DimEmployee`和`FactResellerSales`表。  
  
```  
SELECT DISTINCT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
WHERE 5 IN   
    (SELECT OrderQuantity  
    FROM FactResellerSales AS frs  
    WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
```  
  
### <a name="j-using-exists-versus-in-with-a-subquery"></a>J. 使用子查询使用 EXISTS 与  
 下面的示例演示在语义上等效，以演示了使用之间的差异的查询`EXISTS`关键字和`IN`关键字。 都检索产品子类别是为其每个产品名称的一个实例的子查询的示例`Road Bikes`。 `ProductSubcategoryKey`匹配之间`DimProduct`和`DimProductSubcategory`表。  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE EXISTS  
    (SELECT *  
     FROM DimProductSubcategory AS dps   
     WHERE dp.ProductSubcategoryKey = dps.ProductSubcategoryKey  
           AND dps.EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
 或  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE dp.ProductSubcategoryKey IN  
    (SELECT ProductSubcategoryKey  
     FROM DimProductSubcategory   
     WHERE EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
### <a name="k-using-multiple-correlated-subqueries"></a>K. 使用多个相关子查询  
 此示例使用两个相关子查询查找售出过某种特定产品的雇员的姓名。  
  
```  
SELECT DISTINCT LastName, FirstName, e.EmployeeKey  
FROM DimEmployee e JOIN FactResellerSales s ON e.EmployeeKey = s.EmployeeKey  
WHERE ProductKey IN  
(SELECT ProductKey FROM DimProduct WHERE ProductSubcategoryKey IN  
(SELECT ProductSubcategoryKey FROM DimProductSubcategory   
 WHERE EnglishProductSubcategoryName LIKE '%Bikes'))  
ORDER BY LastName  
;  
  
```  
  
  
