---
title: "ABS（SSIS 表达式） | Microsoft Docs"
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
  - "ABS 函数"
  - "绝对正值"
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# ABS（SSIS 表达式）
  返回数值表达式的绝对值。  
  
## 语法  
  
```  
  
ABS(numeric_expression)  
```  
  
## 参数  
 *numeric_expression*  
 是有符号或无符号的数值表达式。  
  
## 结果类型  
 提交给函数的数值表达式的数据类型。  
  
## 注释  
 如果该参数为空，则 ABS 返回的结果为空。  
  
## 表达式示例  
 这些示例对一个正数和一个负数应用 ABS 函数。 两者都返回 1.23。  
  
```  
ABS(-1.23)  
ABS(1.23)  
```  
  
 此示例对将变量 **HighTemperature** 和 **LowTempature**的值相减的表达式应用 ABS 函数。  
  
```  
ABS(@HighTemperature - @LowTemperature)  
```  
  
## 另请参阅  
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  