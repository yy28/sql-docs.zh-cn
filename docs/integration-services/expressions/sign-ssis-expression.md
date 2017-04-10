---
title: "SIGN（SSIS 表达式） | Microsoft Docs"
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
  - "正值 [Integration Services]"
  - "SIGN 函数"
  - "负值"
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# SIGN（SSIS 表达式）
  返回数值表达式的符号：正号 (+1)、负号 (-1) 或零 (0)。  
  
## 语法  
  
```  
  
SIGN(numeric_expression)  
```  
  
## 参数  
 *numeric_expression*  
 是一个有效的有符号数值表达式。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## 结果类型  
 DT_I4  
  
## 注释  
 如果该参数为空，SIGN 返回的结果为空。  
  
## 表达式示例  
 此示例返回数值的符号。 返回结果为 -1。  
  
```  
SIGN(-123.45)  
```  
  
 此示例返回从 **DealerPrice** 列减去 **StandardCost** 列的结果的符号。  
  
```  
SIGN(DealerPrice - StandardCost)  
```  
  
## 另请参阅  
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  