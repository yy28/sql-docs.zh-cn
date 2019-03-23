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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9addd13deb4dcf3c81a4975e0ed33783799ae2a7
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375905"
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
  
  
