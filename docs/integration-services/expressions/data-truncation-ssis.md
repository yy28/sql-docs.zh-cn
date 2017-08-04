---
title: "数据截断 (SSIS) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- truncating data
- data truncation [Integration Services]
- expressions [Integration Services], data truncation
- truncate options [Integration Services]
ms.assetid: 02461e15-49ca-445b-abb3-5c369c283ec2
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5bed8ab4de8d1fe868cf12ca9e90e1040857d858
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="data-truncation-ssis"></a>数据截断 (SSIS)
  将值从一种数据类型转换成另一种数据类型可能导致值被截断。  
  
 在以下情况中，可能会发生截断：  
  
-   将字符串数据从 DT_WSTR 转换成相同长度的 DT_STR（若原始字符串包含双字节字符）。  
  
-   强制将整数从 DT_I4 转换成 DT_I2，可能会丢失有效位。  
  
-   强制将无符号整数转换成带符号整数，可能会丢失有效位。  
  
-   强制将实数从 DT_R8 转换成 DT_R4，可能会丢失无效位  
  
-   强制将整数从 DT_I4 转换成 DT_R4，可能会丢失无效位。  
  
 在分析表达式时，表达式计算器会标识可能导致截断的显式转换并发出警告。 例如，如果要将 30 个字符的字符串转换为 20 个字符的字符串，则表达式计算器会发出警告。  
  
 不过，系统不会在运行时检查截断。 在运行时，系统会在不发出警告的情况下截断数据。 大部分数据适配器和转换都支持可处理错误行处置的错误输出。  
  
 有关如何处理数据截断的详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)  
  
  
