---
title: EXP（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d98032d040c29e8c1455bbc0e037f920a8588e4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080955"
---
# <a name="exp-ssis-expression"></a>EXP（SSIS 表达式）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  返回数值表达式以 e 为基的指数。 EXP 函数是对 LN 函数操作的补充，有时称为反对数。  
  
## <a name="syntax"></a>语法  
  
```  
  
EXP(numeric_expression)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 有效的数值表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 计算指数前数值表达式被转换为 DT_R8 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 返回结果始终为正数。  
  
## <a name="expression-examples"></a>表达式示例  
 这些示例对正值、负值和零应用 EXP 函数。  
  
```  
EXP(74)  
```  
  
 返回 1.373382979540176E+32。  
  
```  
EXP(-27)  
```  
  
 返回 1.879528816539083E-12。  
  
```  
EXP(0)  
```  
  
 返回 1。  
  
## <a name="see-also"></a>另请参阅  
 [LOG（SSIS 表达式）](../../integration-services/expressions/log-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
