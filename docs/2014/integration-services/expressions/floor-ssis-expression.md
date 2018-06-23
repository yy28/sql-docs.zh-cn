---
title: FLOOR（SSIS 表达式）| Microsoft Docs
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
- largest integer less than or equal to expression
- FLOOR function [SSIS]
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: cae43e01a262258fa2fce824797b3d20682c3829
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024859"
---
# <a name="floor-ssis-expression"></a>FLOOR（SSIS 表达式）
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
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>请参阅  
 [CEILING &#40;SSIS 表达式&#41;](ceiling-ssis-expression.md)   
 [函数&#40;SSIS 表达式&#41;](functions-ssis-expression.md)  
  
  