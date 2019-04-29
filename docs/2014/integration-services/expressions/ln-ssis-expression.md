---
title: LN（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LN function
- natural logarithm of expression [Integration Services]
ms.assetid: 55d7b657-b5fd-4753-9c81-54ed7575e720
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 521ed3f1c817f687bfbddc497f638ee4eed4a834
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62897544"
---
# <a name="ln-ssis-expression"></a>LN（SSIS 表达式）
  返回数值表达式的自然对数。  
  
## <a name="syntax"></a>语法  
  
```  
  
LN(numeric_expression)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 是有效的非零和非负数值表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_R8  
  
## <a name="remarks"></a>备注  
 计算对数前，数值表达式被转换为 DT_R8 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
 如果 *numeric_expression* 的计算结果为 0 或负值，则返回结果为 Null。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例使用了一个数值。 该函数将返回值 3.737766961828337。  
  
```  
LN(42)  
```  
  
 此示例使用列 **Length**。 如果列值为 53.99，则该函数返回 3.9887988442302。  
  
```  
LN(Length)   
```  
  
 此示例使用变量 **Length**。 变量必须为数值数据类型，否则表达式必须包含到数值数据类型的显式转换。 如果 **Length** 为 234.567，则函数将返回 5.45774126708797。  
  
```  
LN(@Length)   
```  
  
## <a name="see-also"></a>请参阅  
 [LOG（SSIS 表达式）](log-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
