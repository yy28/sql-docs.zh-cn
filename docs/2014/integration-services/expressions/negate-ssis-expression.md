---
title: '- （负号）（SSIS 表达式）| Microsoft Docs'
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
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6bbdbea2ccc69cbbcf6c35fe14254d2b9e0a4b2d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138894"
---
# <a name="--negate-ssis-expression"></a>-（负号）（SSIS 表达式）
  对一个数值表达式求反。  
  
## <a name="syntax"></a>语法  
  
```  
  
-numeric_expression  
  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 任何数值数据类型的有效表达式。 仅支持有符号数值数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 返回 *numeric_expression*的数据类型。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例对 **Counter** 变量的值求反，并加上数值 50。  
  
```  
-@Counter + 50  
```  
  
## <a name="see-also"></a>请参阅  
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符&#40;SSIS 表达式&#41;](operators-ssis-expression.md)  
  
  