---
title: "TRIM（SSIS 表达式） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "前导空格"
  - "TRIM 函数"
  - "尾随空格"
ms.assetid: 7dd9081d-a3d4-483a-bf7e-bf2bd7692d39
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# TRIM（SSIS 表达式）
  返回删除了前导空格和尾随空格的字符表达式。  
  
> [!NOTE]  
>  TRIM 不删除空格字符，如制表符或换行符字符。 Unicode 针对许多不同类型的空格提供了码位，但是该函数仅识别 Unicode 码位 0x0020。 双字节字符集 (DBCS) 字符串转换为 Unicode 时，它们可能包含 0x0020 之外的空格字符，而该函数无法删除此类空格。 若要删除所有类型的空格，您可以在基于脚本组件运行的脚本中使用 Microsoft Visual Basic .NET Trim 方法。  
  
## 语法  
  
```  
  
TRIM(character_expression)  
```  
  
## 参数  
 *character_expression*  
 要从中删除空格的字符表达式。  
  
## 结果类型  
 DT_WSTR  
  
## 注释  
 如果该参数为空，则 TRIM 返回的结果为空。  
  
 TRIM 只可用于 DT_WSTR 数据类型。 如果 *character_expression* 参数是字符串文字或数据类型为 DT_STR 的数据列，则它在 TRIM 执行操作前隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)和[转换（SSIS 表达式）](../../integration-services/expressions/cast-ssis-expression.md)。  
  
## 表达式示例  
 此示例删除字符串文字中的前导空格和尾随空格。 返回结果为“New York”。  
  
```  
TRIM("   New York   ")  
```  
  
 此示例删除 **FirstName** 和 **LastName** 列的串联结果中的前导空格和尾随空格。 **FirstName** 和 **LastName** 之间的空字符串不会被删除。  
  
```  
TRIM(FirstName + " "+ LastName)  
```  
  
## 另请参阅  
 [LTRIM（SSIS 表达式）](../../integration-services/expressions/ltrim-ssis-expression.md)   
 [RTRIM（SSIS 表达式）](../../integration-services/expressions/rtrim-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  