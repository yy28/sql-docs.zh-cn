---
title: ~（位非）（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e67cb06d13ec7474a2a6fb23d3a6dbbd5efaecc0
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403159"
---
# <a name="-bitwise-not-ssis-expression"></a>~ （位非）（SSIS 表达式）
  对整数执行位求反运算。 此运算符可应用于有符号和无符号整数数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
~integer_expression  
  
```  
  
## <a name="arguments"></a>参数  
 *integer_expression*  
 整数数据类型的任何有效表达式。 integer_expression 是一个整数，该整数转换为二进制数以进行位运算。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 返回 integer_expression 数据类型。  
  
## <a name="remarks"></a>Remarks  
 InclusionThresholdSetting  
  
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
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
