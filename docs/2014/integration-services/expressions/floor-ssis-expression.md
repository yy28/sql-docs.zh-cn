---
title: FLOOR（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- largest integer less than or equal to expression
- FLOOR function [SSIS]
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5857fb4552800c6cc072d7b68fe51793fa542e80
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52764039"
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
  
## <a name="see-also"></a>请参阅  
 [CEILING（SSIS 表达式）](ceiling-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
