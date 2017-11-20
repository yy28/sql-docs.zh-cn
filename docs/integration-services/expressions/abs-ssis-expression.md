---
title: "ABS （SSIS 表达式） |Microsoft 文档"
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
- ABS function
- absolute positive value
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cf829866d0e55798b612af57a8d8c6cef6d3fcd4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

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
  
## <a name="remarks"></a>注释  
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
 [函数 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

