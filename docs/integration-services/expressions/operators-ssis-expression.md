---
title: "运算符 （SSIS 表达式） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ab52310bc72b0288369ed10bccfbf0b58e6c6ee4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="operators-ssis-expression"></a>运算符（SSIS 表达式）
  本部分介绍了表达式语言提供的运算符和表达式计算器使用的运算符优先级及结合性。  
  
 下表列出了本部分中有关运算符的主题。  
  
|运算符|Description|  
|--------------|-----------------|  
|[强制转换 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/cast-ssis-expression.md)|将表达式从一种数据类型转换为另外一种数据类型。|  
|[&#40; &#41;&#40;括号 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/parentheses-ssis-expression.md)|标识表达式的计算顺序。|  
|[+ &#40;添加 &#41;&#40;SSIS &#41;](../../integration-services/expressions/add-ssis.md)|将两个数值表达式相加。|  
|[+ &#40;串联 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/concatenate-ssis-expression.md)|连接两个表达式。|  
|[-&#40;减去 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/subtract-ssis-expression.md)|从第一个数值表达式的值中减去第二个数值表达式的值。|  
|[-&#40;要求反 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/negate-ssis-expression.md)|对一个数值表达式求反。|  
|[&#42;&#40;乘 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/multiply-ssis-expression.md)|将两个数值表达式相乘。|  
|[除 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/divide-ssis-expression.md)|用第一个数值表达式除以第二个数值表达式。|  
|[&#40;取模 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/modulo-ssis-expression.md)|将第一个数据表达式的值除以第二个数据表达式的值后，提供整数余数。|  
|[&#124;&#124; &#40;逻辑或&#41; &#40;SSIS 表达式&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)|执行“逻辑或”运算。|  
|[& & &#40;逻辑与 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/logical-and-ssis-expression.md)|执行“逻辑与”运算。|  
|[!&#40;逻辑非 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/logical-not-ssis-expression.md)|对布尔操作数求反。|  
|[&#124;&#40;按位与或 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)|对两个整数值执行“位或”运算。|  
|[^ &#40;按位异或&#41; &#40;SSIS 表达式&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)|对两个整数值执行“位异或”运算。|  
|[& &#40;按位 AND &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)|对两个整数值执行“位与”运算。|  
|[~ &#40;位非 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/bitwise-not-ssis-expression.md)|对整数执行位求反运算。|  
|[= = &#40;等 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/equal-ssis-expression.md)|执行比较来确定两个表达式是否相等。|  
|[！ = &#40;不相等 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/unequal-ssis-expression.md)|通过比较来确定两个表达式是否不相等。|  
|[&#62;&#40;大于 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/greater-than-ssis-expression.md)|通过比较来确定第一个表达式是否大于第二个表达式。|  
|[&#60;&#40;小于 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/less-than-ssis-expression.md)|通过比较确定第一个表达式是否小于第二个表达式。|  
|[&#62; = &#40;大于或等于 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)|执行比较来确定第一个表达式是否大于或等于第二个表达式。|  
|[&#60; = &#40;小于或等于 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)|通过比较确定第一个表达式是否小于或等于第二个表达式。|  
|[?: &#40;条件 &#41;&#40;SSIS 表达式 &#41;](../../integration-services/expressions/conditional-ssis-expression.md)|根据布尔表达式的计算结果，返回两个表达式之一。|  
  
 有关优先级层次结构中各个运算符的位置的信息，请参阅 [Operator Precedence and Associativity](../../integration-services/expressions/operator-precedence-and-associativity.md)。  
  
## <a name="see-also"></a>另请参阅  
 [函数 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/functions-ssis-expression.md)   
 [高级的 Integration Services 表达式的示例](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)   
 [Integration Services &#40;SSIS &#41;表达式](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
