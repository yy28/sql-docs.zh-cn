---
title: LN（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
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
ms.openlocfilehash: ac9490abd45c37005fc77ed7733768fa6d7c35a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725255"
---
# <a name="ln-ssis-expression"></a>LN（SSIS 表达式）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="remarks"></a>Remarks  
 计算对数前，数值表达式被转换为 DT_R8 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [LOG（SSIS 表达式）](../../integration-services/expressions/log-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
