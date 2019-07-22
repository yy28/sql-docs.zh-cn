---
title: UPPER（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- UPPER function
- converting lowercase to uppercase
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: d33985f7-1048-4023-83e4-274090acda78
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ea5012b367aedd86be7b0180b975964c61c50905
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967575"
---
# <a name="upper-ssis-expression"></a>UPPER（SSIS 表达式）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="remarks"></a>Remarks  
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
  
  
