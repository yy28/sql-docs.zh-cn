---
title: "别名 （Azure SQL 数据仓库，并行数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b3a5c74-05cf-4385-8ee6-6176d003cb8a
caps.latest.revision: "11"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 65d5799c33afabe8ebbdb212c13661699b9fea9e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="aliasing-azure-sql-data-warehouse-parallel-data-warehouse"></a>别名 （Azure SQL 数据仓库，并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  别名允许临时替换的替代中的表或列名称的简短并易于记住字符串[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)][!INCLUDE[DWsql](../../includes/dwsql-md.md)]查询。 联接查询中通常使用表别名，因为联接语法引用列时需要完全限定的对象名称。  
  
 别名必须是单个词符合对象命名规则。 有关详细信息，请参阅"对象命名规则" [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。 别名不能包含空格，并且不能包含在单引号或双引号。  
  
## <a name="syntax"></a>语法  
  
```  
object_source [ AS ] alias  
```  
  
## <a name="arguments"></a>参数  
 *object_source*  
 源表或列的名称。  
  
 AS  
 可选别名介词。 在使用范围变量别名，禁止 AS 关键字。  
  
 *alias*  
 表或列的所需的临时引用名称。 可以使用任何有效对象名称。 有关详细信息，请参阅"对象命名规则" [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例演示具有多个联接的查询。 在此示例演示了表和列别名。  
  
-   列别名： 这两个列和涉及的选择列表中的列的表达式是在此示例中的有别名。 `SalesTerritoryRegion AS SalesTR`演示一个简单的列别名。 `Sum(SalesAmountQuota) AS TotalSales`演示  
  
-   表别名：`dbo.DimSalesTerritory AS st`演示创建`st`别名`dbo.DimSalesTerritory`表。  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion AS SalesTR,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
  
```  
  
 AS 关键字可以排除，如下所示，但通常包括以提高可读性。  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) TotalSales, SalesTerritoryRegion SalesTR,  
RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) RankResult  
FROM dbo.DimEmployee e  
INNER JOIN dbo.FactSalesQuota sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
## <a name="see-also"></a>另请参阅  
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)  
  
  
