---
title: "运算符优先级和结合性 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- associativity [Integration Services]
- precedence [Integration Services]
ms.assetid: 5094164f-dabc-45b5-b611-384feb2b3fe3
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1b6f1c3252fb8a2f68fae20a67cc6174ea41924a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="operator-precedence-and-associativity"></a>运算符优先级和结合性
  表达式计算器支持的运算符集中的每个运算符在优先级层次结构中具有指定的优先级，并包含计算方向。 运算符的计算方向就是运算符结合性。 具有高优先级的运算符先于低优先级的运算符进行计算。 如果复杂的表达式有多个运算符，则运算符优先级将确定执行操作的顺序。 执行顺序可能对结果值有明显的影响。 某些运算符具有相等的优先级。 如果表达式包含多个具有相等的优先级的运算符，则按照从左到右或从右到左的方向进行运算。  
  
 下表按从高到低的顺序列出了运算符的优先级。 同一层上的运算符具有相等的优先级。  
  
|运算符|运算类型|结合性|  
|---------------------|-----------------------|-------------------|  
|( )|表达式|从左到右|  
|–, !, ~|一元|从右到左|  
|casts|一元|从右到左|  
|*, / ,%|乘法性的|从左到右|  
|+, –|累加性|从左到右|  
|\<, >, \<=, >=|关系|从左到右|  
|==, !=|等式|从左到右|  
|&|位与|从左到右|  
|^|位异或|从左到右|  
|||位或|从左到右|  
|&&|逻辑与|从左到右|  
|&#124;&#124;|逻辑或|从左到右|  
|? 设置用户帐户 ：|条件表达式|从右到左|  
  
## <a name="see-also"></a>另请参阅  
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

