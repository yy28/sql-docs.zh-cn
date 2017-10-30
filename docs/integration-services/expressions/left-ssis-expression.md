---
title: "LEFT （SSIS 表达式） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aad5c2de4903b5ad79fd5087be7801a8195e943f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="left-ssis-expression"></a>LEFT（SSIS 表达式）
  返回从给定字符表达式最左侧开始的指定数量的字符。  
  
## <a name="syntax"></a>语法  
  
```  
  
LEFT(character_expression,number)  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 是从中提取字符的字符表达式。  
  
 *number*  
 指示要返回的字符数的整数表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>注释  
 如果 *number* 大于 *character_expression*的长度，则该函数将返回 *character_expression*。  
  
 如果 *number* 为 0，则该函数返回零长度的字符串。  
  
 如果 *number* 为负数，则该函数返回一个错误。  
  
 *number* 参数可使用变量和列。  
  
 LEFT 只可用于 DT_WSTR 数据类型。 如果 *character_expression* 参数是字符串文字或数据类型为 DT_STR 的数据列，则在 LEFT 执行操作前将隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)和[转换（SSIS 表达式）](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果任一参数为 Null ，则 LEFT 返回的结果为 Null。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例使用字符串文字。 返回结果为 `"Mountain"`。  
  
```  
LEFT("Mountain Bike", 8)  
```  
  
## <a name="see-also"></a>另请参阅  
 [右 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/right-ssis-expression.md)   
 [函数 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

