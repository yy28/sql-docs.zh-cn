---
title: 数据截断 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data truncation [Integration Services]
- expressions [Integration Services], data truncation
- truncate options [Integration Services]
ms.assetid: 02461e15-49ca-445b-abb3-5c369c283ec2
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5f80a51df610040e18dbdae7b1552c56d81cb084
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37328087"
---
# <a name="data-truncation-ssis"></a>数据截断 (SSIS)
  表达式可能因疏忽而致使数据截断。 在下列情况下会发生截断：  
  
-   字符串。 例如，将 DT_WSTR 数据类型的字符串数据转换为相同长度（以字符计）的 DT_STR 数据类型字符串时，如果原始字符串包含有双字节字符将导致数据丢失。  
  
-   有效数字。 例如，将整数从 DT_I4 数据类型转换为 DT_I2 数据类型，或将无符号整数转换为有符号整数。  
  
-   无效数字。 例如，将实数从 DT_R8 转换为 DT_R4 或将整数从 DT_I4 数据类型转换为 DT_R4 数据类型。  
  
 在分析表达式时，表达式计算器会标识可能导致截断的显式转换并发出警告。 例如，如果要将 30 个字符的字符串转换为 20 个字符的字符串，则表达式计算器会发出警告。  
  
> [!NOTE]  
>  运行时不检查截断；数据被截断而不发出警告。 但是，大部分数据适配器和转换支持可处理错误行处置的错误输出。 有关处理数据截断的详细信息，请参阅[数据中的错误处理](../data-flow/error-handling-in-data.md)。  
  
  
