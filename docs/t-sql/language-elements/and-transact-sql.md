---
title: AND (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 340905e1f4ed4917fa4485278e43c6dc754f6164
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="and-transact-sql"></a>AND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  合并两个布尔表达式；在两个表达式均为 TRUE 时返回 TRUE。 当语句中使用多个逻辑运算符时，将首先计算 AND 运算符。 可以通过使用括号改变求值顺序。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
boolean_expression AND boolean_expression  
```  
  
## <a name="arguments"></a>参数  
 *boolean_expression*  
 返回以下布尔值的任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)：TRUE、FALSE 或 UNKNOWN。  
  
## <a name="result-types"></a>结果类型  
 **Boolean**  
  
## <a name="result-value"></a>结果值  
 当两个表达式均为 TRUE 时返回 TRUE。  
  
## <a name="remarks"></a>Remarks  
 下表显示了使用 AND 运算符比较 TRUE 值和 FALSE 值时的结果。  
  
||TRUE|FALSE|UNKNOWN|  
|------|----------|-----------|-------------|  
|**TRUE**|TRUE|FALSE|UNKNOWN|  
|**FALSE**|FALSE|FALSE|FALSE|  
|UNKNOWN|UNKNOWN|FALSE|UNKNOWN|  
  
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
 [运算符 (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [WHERE (Transact-SQL)](../../t-sql/queries/where-transact-sql.md)  
  
  
