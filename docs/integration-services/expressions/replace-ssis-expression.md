---
title: "REPLACE（SSIS 表达式） | Microsoft Docs"
ms.custom: 
  - "ssisdev020617"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "替换字符串表达式"
  - "REPLACE 函数"
ms.assetid: a6837043-ea70-4c6a-9c7a-6868b02b2adc
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# REPLACE（SSIS 表达式）
  将表达式中的一个字符串替换为另一个字符串或空字符串后，返回一个字符表达式。  
  
> [!NOTE]  
>  REPLACE 函数经常使用长字符串。 可以适当处理截断的结果，否则会导致警告或错误。 有关详细信息，请参阅[语法 (SSIS)](../../integration-services/expressions/syntax-ssis.md)。  
  
## 语法  
  
```  
  
REPLACE(character_expression,searchstring,replacementstring)  
```  
  
## 参数  
 *character_expression*  
 是函数要搜索的有效字符表达式。  
  
 *searchstring*  
 是函数尝试定位的有效字符表达式。  
  
 *replacementstring*  
 是用作替换表达式的有效字符表达式。  
  
## 结果类型  
 DT_WSTR  
  
## 注释  
 *searchstring* 的长度一定不能为零。  
  
 *replacementstring* 的长度可以为零。  
  
 *searchstring* 和 *replacementstring* 参数可以使用变量和列。  
  
 REPLACE 只可用于 DT_WSTR 数据类型。 如果 *character_expression1、character_expression2* 和 *character_expression3* 参数是字符串文字或数据类型为 DT_STR 的数据列，则它们在 REPLACE 执行操作前隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。 有关详细信息，请参阅[转换（SSIS 表达式）](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果任何参数值为空，则 REPLACE 返回的结果为空。  
  
## 表达式示例  
 此示例使用一个字符串文字。 返回结果为“All Terrain Bike”。  
  
```  
REPLACE("Mountain Bike", "Mountain","All Terrain")  
```  
  
 此示例删除 **Product** 列中的字符串“Bike”。  
  
```  
REPLACE(Product, "Bike","")  
```  
  
 此示例替换 **DaysToManufacture** 列中的值。 该列具有整数数据类型，且表达式包含将 **DaysToManufacture** 转换为 DT_WSTR 数据类型的转换。  
  
```  
REPLACE((DT_WSTR,8)DaysToManufacture,"6","5")  
```  
  
## 另请参阅  
 [SUBSTRING（SSIS 表达式）](../../integration-services/expressions/substring-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  