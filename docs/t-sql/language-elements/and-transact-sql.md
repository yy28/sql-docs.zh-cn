---
title: "和 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AND_TSQL
- AND
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], TRUE
- TRUE
- AND, about AND operators
- AND
- combining expressions
ms.assetid: b61d7f8d-5a51-49b7-91dd-f6190a5a0fb9
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f21efc0360c992c3a88706a13f84f35d7026b101
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="and-transact-sql"></a>AND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  合并两个布尔表达式，并返回**TRUE**当这两个表达式均为**TRUE**。 在语句中使用多个逻辑运算符时**AND**运算符将首先计算。 可以通过使用括号改变求值顺序。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
boolean_expression AND boolean_expression  
```  
  
## <a name="arguments"></a>参数  
 *boolean_expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)返回一个布尔值： **TRUE**， **FALSE**，或**未知**。  
  
## <a name="result-types"></a>结果类型  
 **Boolean**  
  
## <a name="result-value"></a>结果值  
 当两个表达式均为 TRUE 时返回 TRUE。  
  
## <a name="remarks"></a>注释  
 下表显示了使用 AND 运算符比较 TRUE 值和 FALSE 值时的结果。  
  
||TRUE|FALSE|UNKNOWN|  
|------|----------|-----------|-------------|  
|**TRUE**|TRUE|FALSE|UNKNOWN|  
|**FALSE**|FALSE|FALSE|FALSE|  
|**未知**|UNKNOWN|FALSE|UNKNOWN|  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-the-and-operator"></a>A. 使用 AND 运算符  
 下面的示例选择与职位为 `Marketing Assistant` 且可用假期小时数超过 `41` 的员工有关的信息。  
  
```  
-- Uses AdventureWorks  
  
SELECT  BusinessEntityID, LoginID, JobTitle, VacationHours   
FROM HumanResources.Employee  
WHERE JobTitle = 'Marketing Assistant'  
AND VacationHours > 41 ;  
```  
  
### <a name="b-using-the-and-operator-in-an-if-statement"></a>B. 在 IF 语句中使用 AND 运算符  
 下面的示例显示如何在 IF 语句中使用 AND。 在第一个语句中，`1 = 1` 和 `2 = 2` 均为 True，因此结果是 True。 在第二个示例中，参数 `2 = 17` 为 False，因此结果为 False。  
  
```  
IF 1 = 1 AND 2 = 2  
BEGIN  
   PRINT 'First Example is TRUE'  
END  
ELSE PRINT 'First Example is FALSE';  
GO  
  
IF 1 = 1 AND 2 = 17  
BEGIN  
   PRINT 'Second Example is TRUE'  
END  
ELSE PRINT 'Second Example is FALSE' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

