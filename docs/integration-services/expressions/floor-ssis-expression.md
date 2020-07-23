---
title: FLOOR（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- largest integer less than or equal to expression
- FLOOR function [SSIS]
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4f0161fe842ad8271d04a69b9cb2726db3403314
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917004"
---
# <a name="floor-ssis-expression"></a>FLOOR（SSIS 表达式）

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  返回小于或等于数值表达式的最大整数。  
  
## <a name="syntax"></a>语法  
  
```  
  
FLOOR(numeric_expression)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 有效的数值表达式。  
  
## <a name="result-types"></a>结果类型  
 参数表达式的数值数据类型。 结果是与 *numeric_expression*数据类型相同的计算所得值的整数部分。  
  
## <a name="remarks"></a>备注  
 如果该参数为空，则 FLOOR 返回的结果为空。  
  
## <a name="expression-examples"></a>表达式示例  
 这些示例对正数、负数和零值应用 FLOOR 函数。  
  
```  
FLOOR(123.45)  
```  
  
 返回 123.00  
  
```  
FLOOR(-123.45)  
```  
  
 返回 -124.00  
  
```  
FLOOR(0.00)  
```  
  
 返回 0.00  
  
## <a name="see-also"></a>另请参阅  
 [CEILING（SSIS 表达式）](../../integration-services/expressions/ceiling-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
