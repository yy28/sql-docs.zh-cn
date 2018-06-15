---
title: GROUPING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GROUPING
- GROUPING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], GROUPING function
- grouping columns
- ROLLUP operator
- GROUP BY clause, GROUPING function
- GROUPING function
- CUBE operator
ms.assetid: 4efa3868-1fc4-4626-8fb1-e863cc03e422
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 513a61c37f0a885bd4f594af062ce6137b84f882
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33052860"
---
# <a name="grouping-transact-sql"></a>GROUPING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指示是否聚合 GROUP BY 列表中的指定列表达式。 在结果集中，如果 GROUPING 返回 1 则指示聚合；返回 0 则指示不聚合。 如果指定了 GROUP BY，则 GROUPING 只能用在 SELECT \<select> 列表、HAVING 和 ORDER BY 子句中。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
GROUPING ( <column_expression> )  
```  
  
## <a name="arguments"></a>参数  
 \<column_expression>  
 列或者 [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) 子句中包含列的表达式。  
  
## <a name="return-types"></a>返回类型  
 **tinyint**  
  
## <a name="remarks"></a>Remarks  
 GROUPING 用于区分标准空值和由 ROLLUP、CUBE 或 GROUPING SETS 返回的空值。 作为 ROLLUP、CUBE 或 GROUPING SETS 操作结果返回的 NULL 是 NULL 的特殊应用。 它在结果集内作为列的占位符，表示全体。  
  
## <a name="examples"></a>示例  
 以下示例将分组 `SalesQuota` 并聚合 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的 `SaleYTD` 金额。 `GROUPING` 函数应用于 `SalesQuota` 列。  
  
```  
SELECT SalesQuota, SUM(SalesYTD) 'TotalSalesYTD', GROUPING(SalesQuota) AS 'Grouping'  
FROM Sales.SalesPerson  
GROUP BY SalesQuota WITH ROLLUP;  
GO  
```  
  
 结果集在 `SalesQuota` 下面显示两个 null 值。 第一个 `NULL` 代表从表中的这一列得到的 null 值组。 第二个 `NULL` 位于 ROLLUP 操作所添加的汇总行之中。 汇总行显示所有 `SalesQuota` 组的 `TotalSalesYTD` 金额，并以 `Grouping` 列中的 `1` 进行指示。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 SalesQuota     TotalSalesYTD       Grouping  
------------   -----------------   --------  
NULL           1533087.5999          0  
250000.00      33461260.59           0  
300000.00      9299677.9445          0  
NULL           44294026.1344         1  

(4 row(s) affected)
```  
  
## <a name="see-also"></a>另请参阅  
 [GROUPING_ID (Transact-SQL)](../../t-sql/functions/grouping-id-transact-sql.md)   
 [GROUP BY (Transact-SQL)](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
