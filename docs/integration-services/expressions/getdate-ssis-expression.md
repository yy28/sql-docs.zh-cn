---
title: "GETDATE（SSIS 表达式） | Microsoft Docs"
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
  - "当前日期"
  - "GETDATE 函数"
  - "日期 [Integration Services], GETDATE"
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# GETDATE（SSIS 表达式）
  以 DT_DBTIMESTAMP 格式返回系统的当前日期。 GETDATE 函数不使用参数。  
  
> [!NOTE]  
>  GETDATE 函数的返回结果的长度为 29 个字符。  
  
## 语法  
  
```  
  
GETDATE()  
```  
  
## 参数  
 InclusionThresholdSetting  
  
## 结果类型  
 DT_DBTIMESTAMP  
  
## 表达式示例  
 此示例返回当前日期的年份。  
  
```  
DATEPART("year",GETDATE())  
```  
  
 此示例返回 **ModifiedDate** 列中的日期和当前日期之间的天数。  
  
```  
DATEDIFF("dd",ModifiedDate,GETDATE())  
```  
  
 此示例将三个月加到当前日期。  
  
```  
DATEADD("Month",3,GETDATE())  
```  
  
## 另请参阅  
 [GETUTCDATE（SSIS 表达式）](../../integration-services/expressions/getutcdate-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  