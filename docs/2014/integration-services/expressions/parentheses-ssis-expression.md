---
title: ()（括号）（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
manager: jhubbard
ms.openlocfilehash: b6daec07c75ccc9b6c2a04c7604c18261f979eb2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124120"
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
 *expression*的数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="expression-examples"></a>表达式示例  
 该示例显示如何使用括号修改运算符优先顺序。 第一个表达式取值为 100，而第二个则取值为 31。  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>请参阅  
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符&#40;SSIS 表达式&#41;](operators-ssis-expression.md)  
  
  