---
title: "SUBSTRING（SSIS 表达式）| Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SUBSTRING function
- part of expression returned [Integration Services]
ms.assetid: 3a46748a-f5f8-4a6c-9108-673666754068
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8de4f380006eb9d584cdeff8e71e8df82ed3d700
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="substring-ssis-expression"></a>SUBSTRING（SSIS 表达式）
  返回字符表达式的一部分，该部分从指定位置开始并具有指定长度。 *position* 参数和 *length* 参数的取值必须为整数。  
  
## <a name="syntax"></a>语法  
  
```  
  
SUBSTRING(character_expression, position, length)  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 是从中提取字符的字符表达式。  
  
 *position*  
 是一个指定子字符串开始位置的整数。  
  
 *length*  
 是一个用字符个数指定子字符串长度的整数。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 SUBSTRING 使用从 1 开始的索引。 如果 *position* 为 1，则子字符串从 *character_expression*的第一个字符开始。  
  
 SUBSTRING 只能处理 DT_WSTR 数据类型。 如果 *character_expression* 参数是字符串文字或数据类型为 DT_STR 的数据列，则它在 SUBSTRING 执行操作前隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)和[转换（SSIS 表达式）](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果此参数为空，则 SUBSTRING 返回的结果为空。  
  
 表达式中的所有参数都可以使用变量和列。  
  
 *length* 参数可以超过字符串长度。 在这种情况下，函数将返回字符串的剩余部分。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例从字符串文字的第 4 个字符开始返回两个字符。 返回结果为“ph”。  
  
```  
SUBSTRING("elephant",4,2)  
```  
  
 此示例从第四个字符开始返回字符串文字的剩余部分。 返回结果为“phant”。 *length* 参数超过字符串长度不是错误。  
  
```  
SUBSTRING ("elephant",4,50)  
```  
  
 此示例返回 **MiddleName** 列的第一个字母。  
  
```  
SUBSTRING(MiddleName,1,1)  
```  
  
 此示例使用参数 *position* 和 *length* 中的变量。 如果 **Start** 为 1 而 **Length** 为 5，则函数返回 **Name** 列的头五个字符。  
  
```  
SUBSTRING(Name,@Start,@Length)  
```  
  
 此示例从 **PostalCode** 变量的第六个字符开始返回最后四个字符。  
  
```  
SUBSTRING (@PostalCode,6,4)  
```  
  
 此示例从字符串文字中返回一个零长度的字符串。  
  
```  
SUBSTRING ("Redmond",4,0)  
```  
  
## <a name="see-also"></a>另请参阅  
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
