---
title: LEFT（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e6deba09d2804903e8353d4648a2775d18c8c392
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62897685"
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
  
 *数字*  
 指示要返回的字符数的整数表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>备注  
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
  
## <a name="see-also"></a>另请参阅  
 [RIGHT（SSIS 表达式）](right-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
