---
title: "LN（SSIS 表达式） | Microsoft Docs"
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
  - "LN 函数"
  - "表达式的自然对数 [Integration Services]"
ms.assetid: 55d7b657-b5fd-4753-9c81-54ed7575e720
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# LN（SSIS 表达式）
  返回数值表达式的自然对数。  
  
## 语法  
  
```  
  
LN(numeric_expression)  
```  
  
## 参数  
 *numeric_expression*  
 是有效的非零和非负数值表达式。  
  
## 结果类型  
 DT_R8  
  
## 注释  
 计算对数前，数值表达式被转换为 DT_R8 数据类型。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 如果 *numeric_expression* 的计算结果为 0 或负值，则返回结果为 Null。  
  
## 表达式示例  
 以下示例使用了一个数值。 该函数将返回值 3.737766961828337。  
  
```  
LN(42)  
```  
  
 此示例使用列 **Length**。 如果列值为 53.99，则该函数返回 3.9887988442302。  
  
```  
LN(Length)   
```  
  
 此示例使用变量 **Length**。 变量必须为数值数据类型，否则表达式必须包含到数值数据类型的显式转换。 如果 **Length** 为 234.567，则函数将返回 5.45774126708797。  
  
```  
LN(@Length)   
```  
  
## 另请参阅  
 [LOG（SSIS 表达式）](../../integration-services/expressions/log-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  