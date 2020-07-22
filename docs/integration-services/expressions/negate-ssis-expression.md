---
title: '- （负号）（SSIS 表达式）| Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9322d5a25b8b65432e83ddeac03f486722a50b7c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86911746"
---
# <a name="--negate-ssis-expression"></a>-（负号）（SSIS 表达式）

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  对一个数值表达式求反。  
  
## <a name="syntax"></a>语法  
  
```  
  
-numeric_expression  
  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 任何数值数据类型的有效表达式。 仅支持有符号数值数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 返回 *numeric_expression*的数据类型。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例对 **Counter** 变量的值求反，并加上数值 50。  
  
```  
-@Counter + 50  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
