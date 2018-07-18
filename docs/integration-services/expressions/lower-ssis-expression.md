---
title: LOWER（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 68d2cc83b98161269859fe1cb42af3e5417f2186
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35406439"
---
# <a name="lower-ssis-expression"></a>LOWER（SSIS 表达式）
  返回将大写字符转换为小写字符后得到的字符表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
LOWER(character_expression)  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 是要转换为小写字符的字符表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 LOWER 只可用于 DT_WSTR 数据类型。 如果 *character_expression* 参数是字符串文字或数据类型为 DT_STR 的数据列，则它在 LOWER 执行操作前隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)和[转换（SSIS 表达式）](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果该参数为空，则 LOWER 返回的结果为空。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例将字符串文字转换为小写字符。 返回结果为“new york”。  
  
```  
LOWER("New York")  
```  
  
 此示例将 **Color** 输入列中除第一个字符外的所有字符转换为小写字符。 如果 Color 为 YELLOW，则返回结果为“Yellow”。 有关详细信息，请参阅 [SUBSTRING（SSIS 表达式）](../../integration-services/expressions/substring-ssis-expression.md)。  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 此示例将 **CityName** 变量中的值转换为小写字符。  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>另请参阅  
 [UPPER（SSIS 表达式）](../../integration-services/expressions/upper-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
