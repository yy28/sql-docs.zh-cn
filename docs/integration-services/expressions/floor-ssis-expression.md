---
title: "FLOOR（SSIS 表达式） | Microsoft Docs"
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
  - "小于或等于表达式的最大整数"
  - "FLOOR 函数 [SSIS]"
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# FLOOR（SSIS 表达式）
  返回小于或等于数值表达式的最大整数。  
  
## 语法  
  
```  
  
FLOOR(numeric_expression)  
```  
  
## 参数  
 *numeric_expression*  
 有效的数值表达式。  
  
## 结果类型  
 参数表达式的数值数据类型。 结果是与 *numeric_expression* 数据类型相同的计算所得值的整数部分。  
  
## 注释  
 如果该参数为空，则 FLOOR 返回的结果为空。  
  
## 表达式示例  
 这些示例对正数、负数和零值应用 FLOOR 函数。  
  
```  
FLOOR(123.45)  
```  
  
 返回 123.00  
  
```  
FLOOR(-123.45)  
```  
  
 返回 -124.00  
  
```  
FLOOR(0.00)  
```  
  
 返回 0.00  
  
## 另请参阅  
 [CEILING（SSIS 表达式）](../../integration-services/expressions/ceiling-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  