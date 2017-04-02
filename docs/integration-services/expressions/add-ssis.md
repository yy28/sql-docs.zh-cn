---
title: "+（加）(SSIS) | Microsoft Docs"
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
  - "+（加）"
  - "加法运算符 (+)"
  - "添加表达式"
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# +（加）(SSIS)
  将两个数值表达式相加。  
  
## 语法  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## 参数  
 *numeric_expression1、numeric_expression2*  
 是数值数据类型的任意有效表达式。  
  
## 结果类型  
 由两个参数的数据类型确定。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## 注释  
 如果任意一个操作数为 Null，则结果为 Null。  
  
## 表达式示例  
 此示例将数值相加。  
  
```  
5 + 6.09 + 7.0  
```  
  
 此示例将 **VacationHours** 和 **SickLeaveHours** 列中的值相加。  
  
```  
VacationHours + SickLeaveHours  
```  
  
 此示例将计算后的值添加到 **StandardCost** 列。 变量 **Profit%** 必须用方括号括起来，因为该名称包含 % 字符。 有关详细信息，请参阅[标识符 (SSIS)](../../integration-services/expressions/identifiers-ssis.md)。  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## 另请参阅  
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)  
  
  