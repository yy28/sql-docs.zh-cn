---
title: "弧度 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RADIANS
- RADIANS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RADIANS function
ms.assetid: e9f69951-ecda-45d9-8909-dcb716b1b1c0
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 64c662ed806f5173c506756433318d589a42d4ea
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="radians-transact-sql"></a>RADIANS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  对于在数值表达式中输入的度数值返回弧度值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
RADIANS ( numeric_expression )  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的精确数字或近似数字数据类型类别，除**位**数据类型。  
  
## <a name="return-types"></a>返回类型  
 返回与 numeric_expression 相同的类型。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-radians-to-show-00"></a>A. 使用 RADIANS 显示 0.0  
 以下示例返回结果 `0.0`，因为用于转换为弧度的数值表达式对于 `RADIANS` 函数太小。  
  
```  
SELECT RADIANS(1e-307)  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------   
0.0                        
(1 row(s) affected)  
```  
  
### <a name="b-using-radians-to-return-the-equivalent-angle-of-a-float-expression"></a>B. 使用 RADIANS 返回浮点表达式的等价角度。  
 以下示例执行 `float` 表达式并返回指定角度的 `RADIANS`。  
  
```  
-- First value is -45.01.  
DECLARE @angle float  
SET @angle = -45.01  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is -181.01.  
DECLARE @angle float  
SET @angle = -181.01  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is 0.00.  
DECLARE @angle float  
SET @angle = 0.00  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is 0.1472738.  
DECLARE @angle float  
SET @angle = 0.1472738  
SELECT 'The RADIANS of the angle is: ' +  
    CONVERT(varchar, RADIANS(@angle))  
GO  
-- Last value is 197.1099392.  
DECLARE @angle float  
SET @angle = 197.1099392  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------------------------------   
The RADIANS of the angle is: -0.785573                        
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: -3.15922                         
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 0                                
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 0.00257041                       
 (1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 3.44022                          
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [强制转换和转换 &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [小数和数值 &#40;Transact SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [float 和 real &#40;Transact SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)   
 [int、 bigint、 smallint 和 tinyint &#40;Transact SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)   
 [数学函数 &#40;Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [money 和 smallmoney &#40;Transact SQL &#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
  
  


