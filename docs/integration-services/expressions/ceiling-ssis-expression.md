---
title: "CEILING（SSIS 表达式） | Microsoft Docs"
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
  - "大于或等于表达式的值的最小整数"
  - "CEILING 函数 [SSIS]"
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# CEILING（SSIS 表达式）
  返回大于或等于数值表达式的最小整数。  
  
## 语法  
  
```  
  
CEILING(numeric_expression)  
```  
  
## 参数  
 *numeric_expression*  
 有效的数值表达式。  
  
## 结果类型  
 提交给函数的数值表达式的数据类型。  
  
## 注释  
 如果参数为空，则 CEILING 返回的结果为空。  
  
## 表达式示例  
 这些示例对正值、负值和零值应用 CEILING 函数。  
  
```  
CEILING(123.74)  
```  
  
 返回 124.00  
  
```  
CEILING(-124.27)  
```  
  
 返回 -124.00  
  
```  
CEILING(0.00)  
```  
  
 返回 0.00  
  
## 另请参阅  
 [FLOOR（SSIS 表达式）](../../integration-services/expressions/floor-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  