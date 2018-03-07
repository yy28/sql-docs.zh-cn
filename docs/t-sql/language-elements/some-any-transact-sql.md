---
title: "某些 |任何 (Transact SQL) |Microsoft 文档"
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
- SOME
- SOME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- scalar values
- comparing scalar with single-column set
- ANY operator
- SOME | ANY keyword
- single-column set of values [SQL Server]
ms.assetid: 1f717ad6-f67b-4980-9397-577ecb0e5789
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d81a0d9fb87a11aa7bc109c003d7b723c20c8e77
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="some--any-transact-sql"></a>SOME | ANY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  比较标量值和单列集中的值。 SOME 和 ANY 是等效的。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
scalar_expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
     { SOME | ANY } ( subquery )   
```  
  
## <a name="arguments"></a>参数  
 *scalar_expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 任何有效的比较运算符。  
  
 SOME | ANY  
 指定应进行比较。  
  
 *subquery*  
 包含某列结果集的子查询。 返回的列的数据类型必须是与相同的数据类型*scalar_expression*。  
  
## <a name="result-types"></a>结果类型  
 **Boolean**  
  
## <a name="result-value"></a>结果值  
 部分或任何返回**TRUE**时指定比较为 TRUE 时为的任何对 (*scalar_expression***，***x*) 其中*x*是中的值单列集;否则，返回**FALSE**。  
  
## <a name="remarks"></a>注释  
 某些需要*scalar_expression*要产生积极与至少一个子查询返回的值进行比较。 对于需要的语句， *scalar_expression*要产生积极与子查询返回的每个值进行比较，请参阅[所有 &#40;Transact SQL &#41;](../../t-sql/language-elements/all-transact-sql.md). 例如，如果子查询将返回值为 2 和 3， *scalar_expression* = 一些 （子查询），则计算结果为 TRUE 作为*scalar_express*为 2。 如果子查询将返回值为 2 和 3， *scalar_expression* = 所有 （子查询），则计算结果为 FALSE，因为某些子查询 （3 的值） 的值将不满足的条件表达式。  
  
## <a name="examples"></a>示例  
  
### <a name="a-running-a-simple-example"></a>A. 运行简单示例  
 以下语句创建一个简单表，并向 `1` 列添加值 `2`、`3`、`4` 和 `ID`。  
  
```  
CREATE TABLE T1  
(ID int) ;  
GO  
INSERT T1 VALUES (1) ;  
INSERT T1 VALUES (2) ;  
INSERT T1 VALUES (3) ;  
INSERT T1 VALUES (4) ;  
```  
  
 以下查询返回 `TRUE`，因为 `3` 小于表中的某些值。  
  
```  
IF 3 < SOME (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
 以下查询返回 `FALSE`，因为 `3` 并不小于表中的所有值。  
  
```  
IF 3 < ALL (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
### <a name="b-running-a-practical-example"></a>B. 运行实际示例  
 下面的示例创建存储的过程，用于确定是否指定的所有组件`SalesOrderID`中`AdventureWorks2012`可以在指定的天数内生产数据库。 该示例使用子查询为具有特定 `DaysToManufacture` 的所有组件创建 `SalesOrderID` 值的列表，然后测试子查询返回的值中是否有大于指定天数的值。 如果返回的所有 `DaysToManufacture` 的值都小于规定的天数，则条件为 TRUE，并输出第一个消息。  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE ManyDaysToComplete @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays < SOME  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'At least one item for this order cannot be manufactured in specified number of days.'  
ELSE   
PRINT 'All items for this order can be manufactured in the specified number of days or less.' ;  
  
```  
  
 若要测试的过程，执行过程，通过使用`SalesOrderID``49080`，具有需要的一个组件`2`天数和需要 0 天的两个组件。 第一个语句符合条件。 第二个查询不符合条件。  
  
```  
EXECUTE ManyDaysToComplete 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in the specified number of days or less.`  
  
```  
EXECUTE ManyDaysToComplete 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `At least one item for this order cannot be manufactured in specified number of days.`  
  
## <a name="see-also"></a>另请参阅  
 [所有 &#40;Transact SQL &#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  
