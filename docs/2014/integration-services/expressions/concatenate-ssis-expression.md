---
title: + （连接）（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- concatenation [Integration Services]
- + (concatenate operator)
- concatenate operator (+)
ms.assetid: 0fed6334-7a4f-42dc-a611-191fcaa0e443
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 124071d10424e9b8ee33d1d8966bc6f543533efb
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967435"
---
# <a name="-concatenate-ssis-expression"></a>+（连接）（SSIS 表达式）
  将两个表达式连接为一个表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
character_expression1 + character_expression2  
  
```  
  
## <a name="arguments"></a>参数  
 *expression1、expression2*  
 是任何有效的 DT_STR、DT_WSTR、DT_TEXT、DT_NTEXT 或 DT_IMAGE 数据类型表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>备注  
 表达式可以使用 DT_STR 和 DT_WSTR 数据类型中的任一种或两者都使用。  
  
 DT_STR 和 DT_WSTR 数据类型的连接将返回 DT_WSTR 类型的结果。 字符串的长度是两个原始字符串长度的和（以字符计）。  
  
 只有字符串数据类型 DT_STR 和 DT_WSTR 的数据或二进制大型对象块 (BLOB) 数据类型 DT_TEXT、DT_NTEXT 和 DT_IMAGE 类型的数据可以连接。 其他数据类型必须显式转换为这些数据类型之一，然后才能进行连接。 有关数据类型之间的合法转换的详细信息，请参阅[转换（SSIS 表达式）](cast-ssis-expression.md)。  
  
 两个表达式必须具有相同的数据类型，或者其中一个表达式必须能够隐式转换为另一表达式的数据类型。 例如，如果字符串“Order date is”和 **OrderDate** 列进行连接， **OrderDate** 中的值将隐式转换为字符串数据类型。 若要连接两个数值，这两个数值都必须显式转换为某种字符串数据类型。  
  
 连接只能使用一种 BLOB 数据类型：DT_TEXT、DT_NTEXT 或 DT_IMAGE。  
  
 如果任一元素为空，则结果为空。  
  
 字符串文字必须用引号引起来。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例连接了 **FirstName** 和 **LastName** 列中的值，并在两个值之间插入一个空格。  
  
```  
FirstName + ' ' + LastName  
```  
  
 此示例连接了变量 **ZIPCode** 和 **ZIPCode+4**。 两个变量都具有字符串数据类型。 **ZIPCode+4** 必须用方括号括起来，因为该变量名包含 + 字符。  
  
```  
@ZIPCcode + "-" + @[ZipCode+4]  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](operators-ssis-expression.md)  
  
  
