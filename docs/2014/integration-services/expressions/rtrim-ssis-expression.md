---
title: RTRIM（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RTRIM function
- trailing blanks
ms.assetid: 529bd43e-3f8a-4682-a33e-569176aa7fc4
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e5ef553ad49cc2bc78248d2b244eefd827ce80df
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280053"
---
# <a name="rtrim-ssis-expression"></a>RTRIM（SSIS 表达式）
  返回删除了尾随空格的字符表达式。  
  
> [!NOTE]  
>  RTRIM 不删除空格字符，如制表符或换行符字符。 Unicode 针对许多不同类型的空格提供了码位，但是该函数仅识别 Unicode 码位 0x0020。 双字节字符集 (DBCS) 字符串转换为 Unicode 时，它们可能包含 0x0020 之外的空格字符，而该函数无法删除此类空格。 若要删除所有类型的空格，您可以在基于脚本组件运行的脚本中使用 Microsoft Visual Basic .NET RTrim 方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
RTRIM(character expression)  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 要从中删除空格的字符表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 RTRIM 只用于 DT_WSTR 数据类型。 如果 *character_expression* 参数是字符串文字或数据类型为 DT_STR 的数据列，则它在 RTRIM 执行操作前隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)和[转换（SSIS 表达式）](cast-ssis-expression.md)。  
  
 如果该参数为空，则 RTRIM 返回的结果为空。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例删除字符串文字中的尾随空格。 返回结果为“Hello”。  
  
```  
RTRIM("Hello   ")  
```  
  
 此示例删除 **FirstName** 和 **LastName** 列的串联中的尾随空格。  
  
```  
RTRIM(FirstName + " " + LastName)  
```  
  
 此示例删除 **FirstName** 变量中的尾随空格。  
  
```  
RTRIM(@FirstName)  
```  
  
## <a name="see-also"></a>请参阅  
 [LTRIM &#40;SSIS 表达式&#41;](trim-ssis-expression.md)   
 [TRIM（SSIS 表达式）](trim-ssis-expression.md)   
 [函数&#40;SSIS 表达式&#41;](functions-ssis-expression.md)  
  
  
