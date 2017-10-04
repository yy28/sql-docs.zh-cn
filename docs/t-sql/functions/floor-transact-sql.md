---
title: "FLOOR (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FLOOR_TSQL
- FLOOR
dev_langs:
- TSQL
helpviewer_keywords:
- integers [SQL Server]
- largest integers
- FLOOR function [Transact-SQL]
ms.assetid: 4f26c784-9240-491f-b854-754be3fccae4
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 765cdfb78d13dfa2054571812a051250b19d9d8e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="floor-transact-sql"></a>FLOOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  返回小于或等于指定数值表达式的最大整数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
FLOOR ( numeric_expression )  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 除是精确数字或近似数值数据类型类别的表达式**位**数据类型。  
  
## <a name="return-types"></a>返回类型  
 返回与 numeric_expression 相同的类型。  
  
## <a name="examples"></a>示例  
 以下示例显示正数、负数和货币值在 `FLOOR` 函数中的运用。  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR($123.45);  
```  
  
 结果是与相同的数据类型中的计算值的整数部分*numeric_expression*。  
  
```  
---------      ---------     -----------  
123            -124          123.0000     
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例显示正的数字，负数值，并使用值`FLOOR`函数。  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR($123.45);  
```  
  
 结果是与相同的数据类型中的计算值的整数部分*numeric_expression*。  
  
 `-----   ---------    -----------`  
  
 `123     -124         123`  
  
## <a name="see-also"></a>另请参阅  
 [数学函数 &#40;Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


