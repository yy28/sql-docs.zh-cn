---
title: "REVERSE（SSIS 表达式） | Microsoft Docs"
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
  - "REVERSE 函数"
  - "反向字符表达式"
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# REVERSE（SSIS 表达式）
  按相反顺序返回字符表达式。  
  
## 语法  
  
```  
  
REVERSE(character_expression)  
```  
  
## 参数  
 *character_expression*  
 是要反转的字符表达式。  
  
## 结果类型  
 DT_WSTR  
  
## 注释  
 character_expression 参数必须具有 DT_WSTR 数据类型。  
  
 如果 character_expression 为 Null，则 REVERSE 将返回 Null 结果。  
  
## 表达式示例  
 此示例使用一个字符串文字。 返回结果为“ekiB niatnuoM”。  
  
```  
REVERSE("Mountain Bike")  
```  
  
 此示例使用一个变量。 如果 **Name** 包含 Touring Bike，则返回的结果为“ekiB gniruoT”。  
  
```  
REVERSE(@Name)  
```  
  
## 另请参阅  
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  