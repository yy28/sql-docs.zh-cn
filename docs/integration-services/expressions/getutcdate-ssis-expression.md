---
title: "GETUTCDATE（SSIS 表达式） | Microsoft Docs"
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
  - "日期 [Integration Services], GETUTCDATE"
  - "当前日期"
  - "UTC 时间"
  - "GETUTCDATE 函数"
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# GETUTCDATE（SSIS 表达式）
  使用 DT_DBTIMESTAMP 格式返回以 UTC 时间（协调世界时或格林尼治标准时间）表示的系统当前日期。 GETUTCDATE 函数不带参数。  
  
## 语法  
  
```  
  
GETUTCDATE()  
```  
  
## 参数  
 InclusionThresholdSetting  
  
## 结果类型  
 DT_DBTIMESTAMP  
  
## 表达式示例  
 此示例返回以 UTC 时间表示的当前日期的年份。  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 此示例返回 **ModifiedDate** 列中的日期和当前 UTC 日期之间的天数。  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 此示例将三个月加到当前 UTC 日期。  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## 另请参阅  
 [GETDATE（SSIS 表达式）](../../integration-services/expressions/getdate-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  