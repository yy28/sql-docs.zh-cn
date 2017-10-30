---
title: "电源 (Transact SQL) |Microsoft 文档"
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
- POWER_TSQL
- POWER
dev_langs:
- TSQL
helpviewer_keywords:
- POWER function
ms.assetid: 0fd34494-90b9-4559-8011-a8c1b9f40239
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cb1f3ca862c070888a8e8cb5265f582dcf47d4aa
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="power-transact-sql"></a>POWER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回指定表达式的指定幂的值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
POWER ( float_expression , y )  
```  
  
## <a name="arguments"></a>参数  
 *float_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)类型的**float**或可以隐式转换为的类型**float**。  
  
 *y*  
 是要提升到幂*float_expression*。 *y*可以是除精确数字或近似数值数据类型类别的表达式**位**数据类型。  
  
## <a name="return-types"></a>返回类型  
 返回相同的类型，如在中提交*float_expression*。 例如，如果**十进制**(2,0) 作为提交*float_expression*，返回的结果是**十进制**(2,0)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-power-to-return-the-cube-of-a-number"></a>A. 使用 POWER 返回一个数字的立方  
 下列示例演示一个数字的 3 次幂（数的立方）的运算。  
  
```  
DECLARE @input1 float;  
DECLARE @input2 float;  
SET @input1= 2;  
SET @input2 = 2.5;  
SELECT POWER(@input1, 3) AS Result1, POWER(@input2, 3) AS Result2;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result1                Result2  
---------------------- ----------------------  
8                      15.625  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-power-to-show-results-of-data-type-conversion"></a>B. 使用 POWER 显示数据类型转换的结果  
 下面的示例演示如何*float_expression*保留的数据类型可返回意外的结果。  
  
```  
SELECT   
POWER(CAST(2.0 AS float), -100.0) AS FloatResult,  
POWER(2, -100.0) AS IntegerResult,  
POWER(CAST(2.0 AS int), -100.0) AS IntegerResult,  
POWER(2.0, -100.0) AS Decimal1Result,  
POWER(2.00, -100.0) AS Decimal2Result,  
POWER(CAST(2.0 AS decimal(5,2)), -100.0) AS Decimal2Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
FloatResult            IntegerResult IntegerResult Decimal1Result Decimal2Result Decimal2Result  
---------------------- ------------- ------------- -------------- -------------- --------------  
7.88860905221012E-31   0             0             0.0            0.00           0.00  
```  
  
### <a name="c-using-power"></a>C. 使用 POWER  
 以下示例返回 `POWER` 的 `2` 结果。  
  
```  
DECLARE @value int, @counter int;  
SET @value = 2;  
SET @counter = 1;  
  
WHILE @counter < 5  
   BEGIN  
      SELECT POWER(@value, @counter)  
      SET NOCOUNT ON  
      SET @counter = @counter + 1  
      SET NOCOUNT OFF  
   END;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
2             
  
(1 row(s) affected)  
  
-----------   
4             
  
(1 row(s) affected)  
  
-----------   
8             
  
(1 row(s) affected)  
  
-----------   
16            
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-power-to-return-the-cube-of-a-number"></a>D： 使用 POWER 返回大量的多维数据集  
 下面的示例演示返回`POWER`结果`2.0`的第三次幂。  
  
```  
SELECT POWER(2.0, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
------------ 
8.0
```  
  
## <a name="see-also"></a>另请参阅  
 [小数和数值 &#40;Transact SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [float 和 real &#40;Transact SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)   
 [int、 bigint、 smallint 和 tinyint &#40;Transact SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)   
 [数学函数 &#40;Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [money 和 smallmoney &#40;Transact SQL &#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
  
  


