---
title: ABS（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ABS function
- absolute positive value
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 79e0c524c2b74b76921f8eafe6f8e4cc47a9f6b5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966697"
---
# <a name="abs-ssis-expression"></a>ABS（SSIS 表达式）
  返回数值表达式的绝对值。  
  
## <a name="syntax"></a>语法  
  
```  
  
ABS(numeric_expression)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 是有符号或无符号的数值表达式。  
  
## <a name="result-types"></a>结果类型  
 提交给函数的数值表达式的数据类型。  
  
## <a name="remarks"></a>备注  
 如果该参数为空，则 ABS 返回的结果为空。  
  
## <a name="expression-examples"></a>表达式示例  
 这些示例对一个正数和一个负数应用 ABS 函数。 两者都返回 1.23。  
  
```  
ABS(-1.23)  
ABS(1.23)  
```  
  
 此示例对将变量 **HighTemperature** 和 **LowTempature**的值相减的表达式应用 ABS 函数。  
  
```  
ABS(@HighTemperature - @LowTemperature)  
```  
  
## <a name="see-also"></a>另请参阅  
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
