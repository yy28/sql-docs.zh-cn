---
title: "UPPER（SSIS 表达式）| Microsoft Docs"
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
- UPPER function
- converting lowercase to uppercase
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: d33985f7-1048-4023-83e4-274090acda78
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 737d3ee312d1b9cea65be4807f375923d60ca9d9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="upper-ssis-expression"></a>UPPER（SSIS 表达式）
  返回将小写字符转换为大写字符后得到的字符表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
UPPER(character_expression)  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 要转换为大写字符的字符表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>注释  
 UPPER 只能用于 DT_WSTR 数据类型。 如果 *character_expression* 参数是字符串文字或数据类型为 DT_STR 的数据列，则它在 UPPER 执行操作前隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)和[转换（SSIS 表达式）](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果参数为空，UPPER 将返回空结果。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例将字符串文字转换为大写字符。 返回结果为“HELLO”。  
  
```  
UPPER("hello")  
```  
  
 以下示例将 **FirstName** 列中的第一个字符转换为大写字符。 如果 **FirstName** 为 anna，则返回结果为“A”。 有关详细信息，请参阅 [SUBSTRING（SSIS 表达式）](../../integration-services/expressions/substring-ssis-expression.md)。  
  
```  
UPPER(SUBSTRING(FirstName, 1, 1))  
```  
  
 以下示例将 **PostalCode** 变量中的值转换为大写字符。 如果 **PostalCode** 为 k4b1s2，则返回结果为“K4B1S2”。  
  
```  
UPPER(@PostalCode)  
```  
  
## <a name="see-also"></a>另请参阅  
 [LOWER（SSIS 表达式）](../../integration-services/expressions/lower-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
