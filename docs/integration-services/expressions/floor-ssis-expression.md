---
title: FLOOR（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- largest integer less than or equal to expression
- FLOOR function [SSIS]
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3a79328a87c3b28f814c70c394b8a3e92aeaa6c7
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35411389"
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
  
## <a name="see-also"></a>另请参阅  
 [CEILING（SSIS 表达式）](../../integration-services/expressions/ceiling-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
