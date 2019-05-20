---
title: CEILING（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- smallest integer great than or equal to expression
- CEILING function [SSIS]
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0b9c9c7ab5ed0067d86b3beaa69461ab6e90672
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725568"
---
# <a name="ceiling-ssis-expression"></a>CEILING（SSIS 表达式）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  返回大于或等于数值表达式的最小整数。  
  
## <a name="syntax"></a>语法  
  
```  
  
CEILING(numeric_expression)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 有效的数值表达式。  
  
## <a name="result-types"></a>结果类型  
 提交给函数的数值表达式的数据类型。  
  
## <a name="remarks"></a>Remarks  
 如果参数为空，则 CEILING 返回的结果为空。  
  
## <a name="expression-examples"></a>表达式示例  
 这些示例对正值、负值和零值应用 CEILING 函数。  
  
```  
CEILING(123.74)  
```  
  
 返回 124.00  
  
```  
CEILING(-124.27)  
```  
  
 返回 -124.00  
  
```  
CEILING(0.00)  
```  
  
 返回 0.00  
  
## <a name="see-also"></a>另请参阅  
 [FLOOR（SSIS 表达式）](../../integration-services/expressions/floor-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
