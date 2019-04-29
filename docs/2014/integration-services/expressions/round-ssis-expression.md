---
title: ROUND（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- rounding expressions
- ROUND function [SSIS]
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bfb82476d42bf471853a66b3c93736952d876071
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62897327"
---
# <a name="round-ssis-expression"></a>ROUND（SSIS 表达式）
  返回舍入到指定长度或精度的数值表达式。 length 参数的取值必须为整数。  
  
## <a name="syntax"></a>语法  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 是有效的数值类型的表达式。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
 *长度*  
 是整数表达式。 它是 *numeric_expression* 的舍入精度。  
  
## <a name="result-types"></a>结果类型  
 与 *numeric*_*expression.* 相同的类型。  
  
## <a name="remarks"></a>备注  
 *length* 参数的取值必须为正整数或零。  
  
 如果该参数为空，则 ROUND 返回的结果为空。  
  
## <a name="expression-examples"></a>表达式示例  
 下面的示例对数值进行舍入操作，使其精确到小数点后 3 位。 第一个返回结果为 137.1570，第二个为 137.1580。  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## <a name="see-also"></a>请参阅  
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
