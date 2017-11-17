---
title: "所有 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- ALL_TSQL
- ALL
dev_langs:
- TSQL
helpviewer_keywords:
- single-column set of values [SQL Server]
- ALL (Transact-SQL)
ms.assetid: 4b0c002e-1ffd-4425-a980-11fdc1f24af7
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1fd1b250a30b83a3b014384aafee6c40ff4f1a5a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="all-transact-sql"></a>ALL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  比较标量值和单列集中的值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
scalar_expression { = | <> | != | > | >= | !> | < | <= | !< } ALL ( subquery )  
```  
  
## <a name="arguments"></a>参数  
 *scalar_expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 是一个比较运算符。  
  
 *子查询*  
 返回单列结果集的子查询。 返回的列的数据类型必须是相同的数据类型的数据类型作为*scalar_expression*。  
  
 受限的 SELECT 语句，其中不允许使用 ORDER BY 子句和 INTO 关键字。  
  
## <a name="result-types"></a>结果类型  
 **Boolean**  
  
## <a name="result-value"></a>结果值  
 指定比较为 TRUE 后，则返回 TRUE 的所有对 (*scalar_expression***，***x)*，当*x*是中的值单列集;否则返回 FALSE。  
  
## <a name="remarks"></a>注释  
 需要所有*scalar_expression*要与子查询返回的每个值的明确进行比较。 例如，如果子查询将返回值为 2 和 3， *scalar_expression* < = 所有 （子查询），则计算结果为 TRUE 作为*scalar_expression*为 2。 如果子查询将返回值为 2 和 3， *scalar_expression* = 所有 （子查询），则计算结果为 FALSE，因为某些子查询 （3 的值） 的值将不满足的条件表达式。  
  
 对于需要的语句， *scalar_expression*要只有一个子查询返回的值与明确进行比较，请参阅[一些 &#124;任何 &#40;Transact SQL &#41;](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 本主题讨论了 ALL 用于子查询的情况。 此外可以与使用所有[联合](../../t-sql/language-elements/set-operators-union-transact-sql.md)和[选择](../../t-sql/queries/select-transact-sql.md)。  
  
## <a name="examples"></a>示例  
 下面的示例创建存储的过程，用于确定是否指定的所有组件`SalesOrderID`中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]可以在指定的天数内生产数据库。 该示例使用子查询为具有特定 `DaysToManufacture` 的所有组件创建 `SalesOrderID` 值的列表，然后确认所有 `DaysToManufacture` 都在指定的天数内。  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE DaysToBuild @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays >= ALL  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'All items for this order can be manufactured in specified number of days or less.'  
ELSE   
PRINT 'Some items for this order cannot be manufactured in specified number of days or less.' ;  
  
```  
  
 若要测试该过程，请使用 `SalesOrderID 49080`（具有一个需要 `2` 天的组件和两个需要 0 天的组件）来执行该过程。 下面的第一个语句符合条件。 第二个查询不符合条件。  
  
```  
EXECUTE DaysToBuild 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in specified number of days or less.`  
  
```  
EXECUTE DaysToBuild 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Some items for this order cannot be manufactured in specified number of days or less.`  
  
## <a name="see-also"></a>另请参阅  
 [用例 &#40;Transact SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [如 &#40;Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40;Transact SQL &#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  

