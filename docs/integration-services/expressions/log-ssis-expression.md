---
title: LOG（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- base-10 logarithms
- LOG function
ms.assetid: f7fccace-c178-4e13-bde9-7dc4ef1d98fa
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 77e50116aee1dfc144e5175de7cc56077d205e86
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725242"
---
# <a name="log-ssis-expression"></a>LOG（SSIS 表达式）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  返回数值表达式以 10 为底的对数。  
  
## <a name="syntax"></a>语法  
  
```  
  
LOG(numeric_expression)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 非零或非负数值的有效表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 计算对数前， *数值表达式* 被转换为 DT_R8 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 如果 *numeric_expression* 的计算结果为 0 或负值，则返回结果为 Null。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例使用了一个数值。 该函数将返回值 1.988291341907488。  
  
```  
LOG(97.34)  
```  
  
 此示例使用列 **Length**。 如果列为 101.24，则函数返回 2.005352136486217。  
  
```  
LOG(Length)   
```  
  
 此示例使用变量 **Length**。 变量必须为数值数据类型，或者表达式必须包含到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 数值数据类型的显式转换。 如果 **Length** 为 234.567，则函数将返回 2.370266913465859。  
  
```  
LOG(@Length)   
```  
  
## <a name="see-also"></a>另请参阅  
 [EXP（SSIS 表达式）](../../integration-services/expressions/exp-ssis-expression.md)   
 [LN（SSIS 表达式）](../../integration-services/expressions/ln-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
