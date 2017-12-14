---
title: "LEN（SSIS 表达式）| Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- LEN function
- number of characters
ms.assetid: d961398b-e4d0-4936-be17-8f4c5882a640
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dba697545c46a5060de3e10bec146a1b1c845753
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="len-ssis-expression"></a>LEN（SSIS 表达式）
  返回字符表达式中的字符数。 如果字符串中包含前导空格和尾随空格，则函数会将它们包含在计数内。 LEN 对相同的单字节和双字节字符串返回相同的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
LEN(character_expression)  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 要处理的表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_I4  
  
## <a name="remarks"></a>注释  
 *character_expression* 参数可以是 DT_WSTR、DT_TEXT、DT_NTEXT 或 DT_IMAGE 数据类型。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 如果 *character_expression* 是字符串文字或包含 DT_STR 数据类型的数据列，则在执行 LEN 操作前，该参数将隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。 有关详细信息，请参阅[转换（SSIS 表达式）](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果传递给 LEN 函数的参数包含二进制大型对象块 (BLOB) 数据类型，如 DT_TEXT、DT_NTEXT 或 DT_IMAGE，则该函数将返回字节计数。  
  
 如果参数为 Null，LEN 将返回 Null 结果。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例将返回字符串文字的长度。 返回结果为 12。  
  
```  
LEN("Ball Bearing")  
```  
  
 以下示例将返回 **FirstName** 和 **LastName** 列中的值之间的长度差。  
  
```  
LEN(FirstName) - LEN(LastName)  
```  
  
 返回使用系统变量 **MachineName**的计算机名称的长度。  
  
```  
LEN(@MachineName)  
```  
  
## <a name="see-also"></a>另请参阅  
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
