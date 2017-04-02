---
title: "字符串填充 (SSIS) | Microsoft Docs"
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
  - "填充字符串 [Integration Services]"
  - "表达式 [Integration Services], 字符串填充"
  - "字符串填充"
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# 字符串填充 (SSIS)
  表达式计算器不检查字符串是否包含前导空格和尾随空格，并且比较前不填充字符串来使其具有相同长度。 如果表达式需要字符串填充，可使用 + 运算符连接列值和空字符串。 有关详细信息，请参阅 [+（连接）（SSIS 表达式）](../../integration-services/expressions/concatenate-ssis-expression.md)。  
  
 另一方面，如果要删除空格，表达式计算器提供了 LTRIM、RTRIM 和 TRIM 函数，用于删除前导空格和/或尾随空格。 有关详细信息，请参阅 [LTRIM（SSIS 表达式）](../../integration-services/expressions/ltrim-ssis-expression.md)、[RTRIM（SSIS 表达式）](../../integration-services/expressions/rtrim-ssis-expression.md)和 [TRIM（SSIS 表达式）](../../integration-services/expressions/trim-ssis-expression.md)。  
  
> [!NOTE]  
>  LEN 函数将前导空格和尾随空格包含在其计数中。  
  
## 相关内容  
 pragmaticworks.com 上的技术文章 [SSIS 表达式小抄表](http://go.microsoft.com/fwlink/?LinkId=746575)。  
  
  