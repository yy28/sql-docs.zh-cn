---
title: "- （负号）(Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
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
- negative
dev_langs:
- TSQL
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
- negative values
ms.assetid: d6c14d14-d379-403b-82db-c197ad58c896
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47a9eb729127e53dc3ee72fe5353ad536c56d922
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="unary-operators---negative"></a>一元运算符的负
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回数值表达式的值的负值（一元运算符）。 一元运算符只对一个表达式执行操作，该表达式可以是 numeric 数据类型类别中的任何一种数据类型。   
  
|运算符|含义|  
|--------------|-------------|  
|[+（正）](../../t-sql/language-elements/unary-operators-positive.md)|数值为正。|  
|[-（负）](../../t-sql/language-elements/unary-operators-negative.md)|数值为负。|  
|[~ （位非）](../../t-sql/language-elements/bitwise-not-transact-sql.md)|返回数字的非。|  
  
 +（正）和 -（负）运算符可以用于 numeric 数据类型类别中任一数据类型的任意表达式。 ~ （位非）运算符只能用于整数数据类型类别中任一数据类型的表达式。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
- numeric_expression  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何一种数据类型的数值数据类型类别，除日期和时间类别。  
  
## <a name="result-types"></a>结果类型  
 返回的数据类型*numeric_expression*，只不过 unsigned **tinyint**表达式将提升为一个有符号**smallint**结果。  
  
## <a name="examples"></a>示例  
  
### <a name="a-setting-a-variable-to-a-negative-value"></a>A. 将一个变量设置为负值  
 以下示例将一个变量设置为负值。  
  
```  
USE tempdb;  
GO  
DECLARE @MyNumber decimal(10,2);  
SET @MyNumber = -123.45;  
SELECT @MyNumber AS NegativeValue;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
NegativeValue  
---------------------------------------  
-123.45  
  
(1 row(s) affected)  
  
```  
  
### <a name="b-changing-a-variable-to-a-negative-value"></a>B. 将一个变量更改为负值  
 以下示例将一个变量更改为负值。  
  
```  
USE tempdb;  
GO  
DECLARE @Num1 int;  
SET @Num1 = 5;  
SELECT @Num1 AS VariableValue, -@Num1 AS NegativeValue;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
VariableValue NegativeValue  
------------- -------------  
5             -5  
  
(1 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-the-negative-of-a-positive-constant"></a>C. 返回的负数正的常量  
 下面的示例返回正数的常量的负值。  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) - 17 FROM DimEmployee;  
```  
  
 返回  
  
```  
-17  
```  
  
### <a name="d-returning-the-positive-of-a-negative-constant"></a>D. 返回负常量的正  
 下面的示例返回负常量的正。  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) – ( - 17) FROM DimEmployee;  
```  
  
 返回  
  
```  
17  
```  
  
### <a name="e-returning-the-negative-of-a-column"></a>E. 返回列的负值  
 下面的示例返回的负数`BaseRate`值为每个雇员`dimEmployee`表。  
  
```  
USE ssawPDW;  
  
SELECT - BaseRate FROM DimEmployee;  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  


