---
title: 字符串填充 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4ffdfe7b79dad5d8fa9ee4d68d13ffcb57f9e038
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125643"
---
# <a name="string-padding-ssis"></a>字符串填充 (SSIS)
  表达式计算器不检查字符串是否包含前导空格和尾随空格，并且比较前不填充字符串来使其具有相同长度。 如果表达式需要字符串填充，可使用 + 运算符连接列值和空字符串。 有关详细信息，请参阅 [+（连接）（SSIS 表达式）](concatenate-ssis-expression.md)。  
  
 另一方面，如果要删除空格，表达式计算器提供了 LTRIM、RTRIM 和 TRIM 函数，用于删除前导空格和/或尾随空格。 有关详细信息，请参阅 [LTRIM（SSIS 表达式）](trim-ssis-expression.md)、[RTRIM（SSIS 表达式）](rtrim-ssis-expression.md)和 [TRIM（SSIS 表达式）](trim-ssis-expression.md)。  
  
> [!NOTE]  
>  LEN 函数将前导空格和尾随空格包含在其计数中。  
  
## <a name="related-content"></a>相关内容  
 pragmaticworks.com 上的技术文章 [SSIS 表达式小抄表](http://go.microsoft.com/fwlink/?LinkId=217683)。  
  
  