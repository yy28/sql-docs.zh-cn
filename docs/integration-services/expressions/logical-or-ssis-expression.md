---
title: "||（逻辑或）（SSIS 表达式） | Microsoft Docs"
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
  - "OR 运算符"
  - "逻辑或 (||)"
  - "||（逻辑或）"
ms.assetid: a3c07c09-f121-4187-9617-b01adcf843c4
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# ||（逻辑或）（SSIS 表达式）
  执行“逻辑或”运算。 如果条件之一或两个条件都为 TRUE，则表达式计算结果为 TRUE。  
  
## 语法  
  
```  
  
boolean_expression1 || boolean_expression2  
```  
  
## 参数  
 *boolean_expression1、boolean_expression2*  
 计算结果为 TRUE、FALSE 或 NULL 的任意有效表达式。  
  
## 结果类型  
 DT_BOOL  
  
## 注释  
 下表显示了 || 运算符的结果。  
  
|结果|表达式|表达式|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|TRUE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|TRUE|NULL|TRUE|  
|NULL|NULL|FALSE|  
  
## SSIS 表达式示例  
 该示例使用 **StandardCost** 和 **ListPrice** 列。 如果 **StandardCost** 列的值小于 300 或者 **ListPrice** 列的值大于 500，则该示例计算结果为 TRUE。  
  
```  
StandardCost < 300 || ListPrice > 500  
```  
  
 该示例使用变量 **SPrice** 和 **LPrice** ，而不是数值。  
  
```  
StandardCost < @SPrice || ListPrice > @LPrice  
```  
  
## 另请参阅  
 [|（位异或）（SSIS 表达式）](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [^（位异或）（SSIS 表达式）](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)  
  
  