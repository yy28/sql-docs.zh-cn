---
title: ~（位非）（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d7434dd2b5d6ecaa1f72474e7fc3d450de18b8d2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967467"
---
# <a name="-bitwise-not-ssis-expression"></a>~ （位非）（SSIS 表达式）
  对整数执行位求反运算。 此运算符可应用于有符号和无符号整数数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
~integer_expression  
  
```  
  
## <a name="arguments"></a>参数  
 *integer_expression*  
 整数数据类型的任何有效表达式。 integer  _expression  是一个整数，该整数转换为二进制数以进行位运算。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 返回 integer_expression  数据类型。  
  
## <a name="remarks"></a>备注  
 无  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例对数值 170 (0000 0000 1010 1010) 执行位 ~（非）运算。 该数值是一个有符号整数。  
  
```  
  
~ 170  
```  
  
 表达式的计算结果为 -170 (1111111101010101)。  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](operators-ssis-expression.md)  
  
  
