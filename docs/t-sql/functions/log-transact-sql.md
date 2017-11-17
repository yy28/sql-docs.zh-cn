---
title: "日志 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOG
- LOG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- logarithm of expression
- LOG function
ms.assetid: f7c39511-cd84-4362-93ba-0d93655217ee
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 7918cb0d2832e88f3e4218b98c7f606f559f2e4e
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="log-transact-sql"></a>LOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回指定的自然对数**float**中的表达式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
  
LOG ( float_expression [, base ] )  
```  
  
```  
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
LOG ( float_expression )  
```  
  
## <a name="arguments"></a>参数  
 *float_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)类型的**float**或可以隐式转换为的类型**float**。  
  
 *基*  
 可选的整型参数，设置对数的底数。  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
## <a name="return-types"></a>返回类型  
 **float**  
  
## <a name="remarks"></a>注释  
 默认情况下， **log （)**返回自然对数。 从开始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，你可以通过使用可选改为其他值对数的底*基*参数。  
  
 自然对数是底数的对数**e**，其中**e**是一个无理常数约等于 2.718281828。  
  
 数字的指数的自然对数是数字本身： 日志 (EXP (  *n*  )) =  *n* 。 并且数字的自然对数的指数是该数字本身： EXP (日志 (  *n*  )) =  *n* 。  
  
## <a name="examples"></a>示例  
  
### <a name="a-calculating-the-logarithm-for-a-number"></a>A. 计算某数的对数。  
 下面的示例计算`LOG`指定**float**表达式。  
  
```  
DECLARE @var float = 10;  
SELECT 'The LOG of the variable is: ' + CONVERT(varchar, LOG(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------------------------  
The LOG of the variable is: 2.30259  
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-logarithm-of-the-exponent-of-a-number"></a>B. 计算某数指数的对数。  
 以下示例计算某数指数的 `LOG`。  
  
```  
SELECT LOG (EXP (10));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------  
10  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-logarithm-for-a-number"></a>C. 计算一个数字的对数  
 下面的示例计算`LOG`指定**float**表达式。  
  
```  
SELECT LOG(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ----------------`  
  
 2.30
 ```  
  
## <a name="see-also"></a>另请参阅  
 [数学函数 &#40;Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [EXP &#40;Transact SQL &#41;](../../t-sql/functions/exp-transact-sql.md)   
 [LOG10 &#40;Transact SQL &#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  


