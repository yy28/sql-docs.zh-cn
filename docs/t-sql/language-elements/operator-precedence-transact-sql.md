---
title: "运算符优先级 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- operators [Transact-SQL], precedence
- operator precedence [Transact-SQL]
- order of operator execution [Transact-SQL]
- precedence [SQL Server], operators
ms.assetid: f04d2439-6fff-4e4c-801f-cc62faef510a
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c534653bb383fbbfcd069cb98bb72519d3d02987
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="operator-precedence-transact-sql"></a>运算符优先级 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  当一个复杂的表达式有多个运算符时，运算符优先级决定执行运算的先后次序。 执行顺序可能对结果值有明显的影响。  
  
 运算符的优先级别如下表中所示。 在较低级别的运算符之前先对较高级别的运算符进行求值。  
  
|Level|运算符|  
|-----------|---------------|  
|1|~（位非）|  
|2|* （乘） / （除），%（取模）|  
|3|+ （正）、-（负号），+ （加）、 （+ 串联），-（减） （& a) (按位 AND)、 ^ (按位异或)，&#124;（位或）|  
|4|=、 >， \<，> =、 < =、 <>，！ =、 ！ >，！ < （比较运算符）|  
|5|NOT|  
|6|和|  
|7|ALL、ANY、BETWEEN、IN、LIKE、OR、SOME|  
|8|=（赋值）|  
  
 当一个表达式中的两个运算符有相同的运算符优先级别时，将按照它们在表达式中的位置对其从左到右进行求值。 例如，在下面的 `SET` 语句所使用的表达式中，在加运算符之前先对减运算符进行求值。  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 4 - 2 + 27;  
-- Evaluates to 2 + 27 which yields an expression result of 29.  
SELECT @MyNumber;  
```  
  
 在表达式中使用括号替代所定义的运算符的优先级。 首先对括号中的内容进行求值，从而产生一个值，然后括号外的运算符才可以使用这个值。  
  
 例如，在下面的 `SET` 语句所使用的表达式中，乘运算符具有比加运算符更高的优先级别。 因此，先对它进行求值；此表达式的结果为 `13`。  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * 4 + 5;  
-- Evaluates to 8 + 5 which yields an expression result of 13.  
SELECT @MyNumber;  
```  
  
 在下面的 `SET` 语句所使用的表达式中，括号使加运算先执行。 此表达式的结果为 `18`。  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + 5);  
-- Evaluates to 2 * 9 which yields an expression result of 18.  
SELECT @MyNumber;  
```  
  
 如果表达式有嵌套的括号，那么首先对嵌套最深的表达式求值。 以下示例中包含嵌套的括号，其中表达式 `5 - 3` 在嵌套最深的那对括号中。 该表达式产生一个值 `2`。 然后，加运算符 (`+`) 将此结果与 `4` 相加。 这将生成一个值 `6`。 最后将 `6` 与 `2` 相乘，生成表达式的结果 `12`。  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + (5 - 3) );  
-- Evaluates to 2 * (4 + 2) which then evaluates to 2 * 6, and   
-- yields an expression result of 12.  
SELECT @MyNumber;  
```  
  
## <a name="see-also"></a>另请参阅  
 [逻辑运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/logical-operators-transact-sql.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)  
  
  
