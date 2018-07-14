---
title: LEFT（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: da89c1a1740d8acd0f284d9cf1475d34ca651792
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252589"
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
  
## <a name="remarks"></a>Remarks  
 如果 *number* 大于 *character_expression*的长度，则该函数将返回 *character_expression*。  
  
 如果 *number* 为 0，则该函数返回零长度的字符串。  
  
 如果 *number* 为负数，则该函数返回一个错误。  
  
 *number* 参数可使用变量和列。  
  
 LEFT 只可用于 DT_WSTR 数据类型。 如果 *character_expression* 参数是字符串文字或数据类型为 DT_STR 的数据列，则在 LEFT 执行操作前将隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)和[转换（SSIS 表达式）](cast-ssis-expression.md)。  
  
 如果任一参数为 Null ，则 LEFT 返回的结果为 Null。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例使用字符串文字。 返回结果为 `"Mountain"`。  
  
```  
LEFT("Mountain Bike", 8)  
```  
  
## <a name="see-also"></a>请参阅  
 [右&#40;SSIS 表达式&#41;](right-ssis-expression.md)   
 [函数&#40;SSIS 表达式&#41;](functions-ssis-expression.md)  
  
  
