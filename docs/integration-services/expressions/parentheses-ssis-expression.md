---
title: ()（括号）（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16412dc829f4a574a505928d6c4ff380dd8273d4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="-parentheses-ssis-expression"></a>()（括号）（SSIS 表达式）
  标识表达式的计算顺序。 包括在括号内的表达式具有最高的计算优先级。 包括在括号内的嵌套表达式按照从内到外的顺序计算。  
  
 括号还可用来使复杂的表达式变得更易理解。  
  
## <a name="syntax"></a>语法  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 为任意有效的表达式。  
  
## <a name="result-types"></a>结果类型  
 *expression*的数据类型。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="expression-examples"></a>表达式示例  
 该示例显示如何使用括号修改运算符优先顺序。 第一个表达式取值为 100，而第二个则取值为 31。  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
