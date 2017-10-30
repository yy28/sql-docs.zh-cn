---
title: "无 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HAVING
- HAVING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restricting conditions for result set
- search conditions [SQL Server], HAVING clause
- HAVING clause
- HAVING clause, about HAVING clause
ms.assetid: 55650709-001e-42f4-902f-ead09a3c34af
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9bff75a84689090f6e416db052a2561e57fa98a6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="select---having-transact-sql"></a>SELECT-无 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定组或聚合的搜索条件。 HAVING 只能与 SELECT 语句一起使用。 HAVING 通常在 GROUP BY 子句中使用。 如果不使用 GROUP BY 子句，则 HAVING 的行为与 WHERE 子句一样。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
[ HAVING <search condition> ]  
```  
  
## <a name="arguments"></a>参数  
\<search_condition > 指定组或聚合应满足的搜索条件。  
  
 **文本**，**映像**，和**ntext**数据类型不能在 HAVING 子句。  
  
## <a name="examples"></a>示例  
 以下示例使用简单 `HAVING` 子句从 `SalesOrderID` 表中检索超过 `SalesOrderDetail` 的每个 `$100000.00` 的总计。  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID  
HAVING SUM(LineTotal) > 100000.00  
ORDER BY SalesOrderID ;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例使用`HAVING`子句来检索每个总`SalesAmount`从`FactInternetSales`表时`OrderDateKey`2004年或更高版本的年份。  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING SUM(SalesAmount) > 80000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>另请参阅  
 [GROUP BY &#40;Transact SQL &#41;](../../t-sql/queries/select-group-by-transact-sql.md)   
 [其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


