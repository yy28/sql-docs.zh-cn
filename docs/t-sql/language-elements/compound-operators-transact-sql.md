---
title: "复合运算符 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators
- compound operators, described
ms.assetid: 5072fe91-02d3-42a7-831f-756eff714a17
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2e5fde8cd4265359722f33400d834b0a301718ef
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="compound-operators-transact-sql"></a>复合运算符 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  复合运算符执行一些运算并将原始值设置为运算的结果。 例如，如果变量@x等于 35，则@x+ = 2 采用的原始值@x，将 2 和集添加@x为该新值 (37)。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 提供了以下复合运算符：  
  
|运算符|详细信息链接|操作|  
|--------------|------------------------------|------------|  
|+=|[+ = &#40;添加等于 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/add-equals-transact-sql.md)|将原始值加上一定的量，并将原始值设置为结果。|  
|-=|[-= &#40;减去等于 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md)|将原始值减去一定的量，并将原始值设置为结果。|  
|*=|[&#42; = &#40;乘等于 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/multiply-equals-transact-sql.md)|将原始值乘上一定的量，并将原始值设置为结果。|  
|/=|[&#40; 划分等于 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)|将原始值除以一定的量，并将原始值设置为结果。|  
|%=|[取模等于 &#40;Transact SQL &#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md)|将原始值除以一定的量，并将原始值设置为余数。|  
|&=|[& = &#40;按位与等于 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)|对原始值执行位与运算，并将原始值设置为结果。|  
|^=|[^ = &#40;按位异或等于 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)|对原始值执行位异或运算，并将原始值设置为结果。|  
|&#124;=|[&#124; = &#40;按位或等于 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)|对原始值执行位或运算，并将原始值设置为结果。|  
  
## <a name="syntax"></a>语法  
  
```  
  
expression operator expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何数据类型之一数值类别中。  
  
## <a name="result-types"></a>结果类型  
 返回优先级较高的参数的数据类型。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>注释  
 有关详细信息，请参阅与每个运算符相关的主题。  
  
## <a name="examples"></a>示例  
 下面的示例演示复合运算。  
  
```  
DECLARE @x1 int = 27;  
SET @x1 += 2 ;  
SELECT @x1 AS Added_2;  
  
DECLARE @x2 int = 27;  
SET @x2 -= 2 ;  
SELECT @x2 AS Subtracted_2;  
  
DECLARE @x3 int = 27;  
SET @x3 *= 2 ;  
SELECT @x3 AS Multiplied_by_2;  
  
DECLARE @x4 int = 27;  
SET @x4 /= 2 ;  
SELECT @x4 AS Divided_by_2;  
  
DECLARE @x5 int = 27;  
SET @x5 %= 2 ;  
SELECT @x5 AS Modulo_of_27_divided_by_2;  
  
DECLARE @x6 int = 9;  
SET @x6 &= 13 ;  
SELECT @x6 AS Bitwise_AND;  
  
DECLARE @x7 int = 27;  
SET @x7 ^= 2 ;  
SELECT @x7 AS Bitwise_Exclusive_OR;  
  
DECLARE @x8 int = 27;  
SET @x8 |= 2 ;  
SELECT @x8 AS Bitwise_OR;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [按位运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  
