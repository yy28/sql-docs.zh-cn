---
description: ()（括号）（SSIS 表达式）
title: ()（括号）（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 970ac5479d0d09276aae8eb095199abbbee910c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477517"
---
# <a name="-parentheses-ssis-expression"></a>()（括号）（SSIS 表达式）

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  标识表达式的计算顺序。 包括在括号内的表达式具有最高的计算优先级。 包括在括号内的嵌套表达式按照从内到外的顺序计算。  
  
 括号还可用来使复杂的表达式变得更易理解。  
  
## <a name="syntax"></a>语法  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 为任何有效的表达式。  
  
## <a name="result-types"></a>结果类型  
 *expression*的数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="expression-examples"></a>表达式示例  
 该示例显示如何使用括号修改运算符优先顺序。 第一个表达式取值为 100，而第二个则取值为 31。  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
