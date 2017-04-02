---
title: "YEAR（SSIS 表达式） | Microsoft Docs"
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
  - "日期 [Integration Services], YEAR"
  - "YEAR 函数"
ms.assetid: 9d88dead-ace8-44b9-b8e2-916c1842e155
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# YEAR（SSIS 表达式）
  返回一个表示日期中的“年份”日期部分的整数。  
  
## 语法  
  
```  
  
YEAR(date)  
```  
  
## 参数  
 *date*  
 是任意日期格式的日期。  
  
## 结果类型  
 DT_I4  
  
## 注释  
 如果参数为空，则 YEAR 返回的结果为空。  
  
 日期文字必须显式转换为日期数据类型之一。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
> [!NOTE]  
>  在日期文本显式转换为以下日期数据类型之一时，表达式验证失败：DT_DBTIMESTAMPOFFSET 和 DT_DBTIMESTAMP2。  
  
 使用 YEAR 函数更为简要，但其等价于使用 DATEPART("Year", date) 函数。  
  
## 表达式示例  
 此示例返回日期文字中表示年份的数字。 如果日期格式为 mm/dd/yyyy，则此示例返回“2002”。  
  
```  
YEAR((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 此示例返回 **ModifiedDate** 列中表示年份的整数。  
  
```  
YEAR(ModifiedDate)  
```  
  
 此示例返回当前日期中表示年的整数。  
  
```  
YEAR(GETDATE())  
```  
  
## 另请参阅  
 [DATEADD（SSIS 表达式）](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF（SSIS 表达式）](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART（SSIS 表达式）](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY（SSIS 表达式）](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH（SSIS 表达式）](../../integration-services/expressions/month-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  