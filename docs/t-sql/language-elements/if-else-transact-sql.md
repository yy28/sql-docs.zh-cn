---
title: IF...ELSE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/11/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IF_TSQL
- IF
dev_langs:
- TSQL
helpviewer_keywords:
- IF...ELSE keyword
- ELSE (IF...ELSE) keyword
- ELSE keyword
- IF keyword
ms.assetid: 676c881f-dee1-417a-bc51-55da62398e81
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 34a14f617d5eed0b56d6ffb44134f03efa96d2c2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="ifelse-transact-sql"></a>IF...ELSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的执行条件。 如果满足条件，则在 IF 关键字及其条件之后执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：布尔表达式返回 TRUE。 可选的 ELSE 关键字引入另一个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，当不满足 IF 条件时就执行该语句：布尔表达式返回 FALSE。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
IF Boolean_expression   
     { sql_statement | statement_block }   
[ ELSE   
     { sql_statement | statement_block } ]   
```  
  
## <a name="arguments"></a>参数  
 *Boolean_expression*  
 返回 TRUE 或 FALSE 的表达式。 如果布尔表达式中含有 SELECT 语句，则必须用括号将 SELECT 语句括起来。  
  
 { *sql_statement*| *statement_block* }  
 任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或用语句块定义的语句分组。 除非使用语句块，否则 IF 或 ELSE 条件只能影响一个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的性能。  
  
 若要定义语句块，请使用控制流关键字 BEGIN 和 END。  
  
## <a name="remarks"></a>注释  
 IF...ELSE 构造可用于批处理、存储过程和即席查询。 当此构造用于存储过程时，通常用于测试某个参数是否存在。  
  
 可以在其他 IF 之后或在 ELSE 下面，嵌套另一个 IF 测试。 嵌套级数的限制取决于可用内存。  
  
## <a name="example"></a>示例  
  
```  
IF DATENAME(weekday, GETDATE()) IN (N'Saturday', N'Sunday')
       SELECT 'Weekend';
ELSE 
       SELECT 'Weekday';
```  
  
 有关更多示例，请参阅[ELSE &#40; 如果...其他 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/else-if-else-transact-sql.md).  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例使用`IF…ELSE`根据中的项的权重来确定这两个响应以向用户，`DimProduct`表。  
  
```  
-- Uses AdventureWorksDW  
  
DECLARE @maxWeight float, @productKey integer  
SET @maxWeight = 100.00  
SET @productKey = 424  
IF @maxWeight <= (SELECT Weight from DimProduct 
                  WHERE ProductKey = @productKey)   
    (SELECT @productKey AS ProductKey, EnglishDescription, Weight, 
    'This product is too heavy to ship and is only available for pickup.' 
        AS ShippingStatus
    FROM DimProduct WHERE ProductKey = @productKey);  
ELSE  
    (SELECT @productKey AS ProductKey, EnglishDescription, Weight, 
    'This product is available for shipping or pickup.' 
        AS ShippingStatus
    FROM DimProduct WHERE ProductKey = @productKey);  
```  
  
## <a name="see-also"></a>另请参阅  
 [BEGIN...END &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [END &#40;BEGIN...END&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/end-begin-end-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [虽然 &#40;Transact SQL &#41;](../../t-sql/language-elements/while-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [控制流语言 &#40;Transact SQL &#41;](~/t-sql/language-elements/control-of-flow.md) [ELSE &#40; 如果...其他 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/else-if-else-transact-sql.md) 
  
  



