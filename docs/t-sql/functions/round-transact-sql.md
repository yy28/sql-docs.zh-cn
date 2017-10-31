---
title: "ROUND (Transact SQL) |Microsoft 文档"
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
- ROUND_TSQL
- ROUND
dev_langs:
- TSQL
helpviewer_keywords:
- rounding expressions
- ROUND function [Transact-SQL]
ms.assetid: 23921ed6-dd6a-4c9e-8c32-91c0d44fe4b7
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: cba8b5a9b62a21fc810ff9bb5fcd3d0c6429f9f5
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="round-transact-sql"></a>ROUND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回一个数值，舍入到指定的长度或精度。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ROUND ( numeric_expression , length [ ,function ] )  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ROUND (numeric_expression , length )  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的精确数字或近似数字数据类型类别，除**位**数据类型。  
  
 *length*  
 是指精度*numeric_expression*要舍入。 *长度*必须是类型的表达式**tinyint**， **smallint**，或**int**。当*长度*的正数值*numeric_expression*舍入到由指定的小数位数*长度*。 当*长度*为负数， *numeric_expression*所指定的小数点左侧舍入*长度*。  
  
 *函数*  
 要执行的操作的类型。 *函数*必须**tinyint**， **smallint**，或**int**。当*函数*省略或者它的值为 0 （默认值）、 *numeric_expression*舍入。 如果以外的值指定了 0， *numeric_expression*将被截断。  
  
## <a name="return-types"></a>返回类型  
 返回以下数据类型。  
  
|表达式结果|返回类型|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**int**|**int**|  
|**ssNoversion**|**int**|  
|**bigint**|**bigint**|  
|**十进制**和**数值**类别 （p、 s）|**十进制 （p、 s）**|  
|**money**和**smallmoney**类别|**money**|  
|**float**和**实际**类别|**float**|  
  
## <a name="remarks"></a>注释  
 ROUND 始终返回一个值。 如果*长度*为负数，大于小数点前的数字个数，则 ROUND 返回 0。  
  
|示例|结果|  
|-------------|------------|  
|ROUND （748.58、-4）|0|  
  
 ROUND 返回的圆形*numeric_expression*，数据类型，而不考虑时*长度*为负数。  
  
|示例|结果|  
|--------------|------------|  
|ROUND （748.58，则为-1）|750.00|  
|ROUND （748.58，-2）|700.00|  
|ROUND(748.58, -3)|导致算术溢出，因为 748.58 默认为 decimal(5,2)，它无法返回 1000.00。|  
|若要向上舍入到 4 位，请更改输入的数据类型。 例如：<br /><br /> `SELECT ROUND(CAST (748.58 AS decimal (6,2)),-3);`|1000.00|  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-round-and-estimates"></a>A. 使用 ROUND 和估计值  
 以下示例显示了两个表达式，阐释使用了 `ROUND` 后，最后一位数将始终为估计值。  
  
```  
SELECT ROUND(123.9994, 3), ROUND(123.9995, 3);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -----------  
123.9990    124.0000      
```  
  
### <a name="b-using-round-and-rounding-approximations"></a>B. 使用 ROUND 和舍入近似值  
 以下示例显示舍入和近似值。  
  
```  
SELECT ROUND(123.4545, 2), ROUND(123.45, -2);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ----------
123.45    100.00
```
  
### <a name="c-using-round-to-truncate"></a>C. 使用 ROUND 截断  
 以下示例使用了两个 `SELECT` 语句，用于阐释舍入和截断之间的区别。 第一个语句舍入结果。 第二个语句截断结果。  
  
```  
SELECT ROUND(150.75, 0);  
GO  
SELECT ROUND(150.75, 0, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
151.00  
  
(1 row(s) affected)  
  
--------  
150.00  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-round-and-estimates"></a>D. 使用 ROUND 和估计值  
 以下示例显示了两个表达式，阐释使用了 `ROUND` 后，最后一位数将始终为估计值。  
  
```  
SELECT ROUND(123.994999, 3), ROUND(123.995444, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ---------
123.995000    123.995444
```
  
## <a name="see-also"></a>另请参阅  
 [上限 &#40;Transact SQL &#41;](../../t-sql/functions/ceiling-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FLOOR &#40;Transact SQL &#41;](../../t-sql/functions/floor-transact-sql.md)   
 [数学函数 &#40;Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


