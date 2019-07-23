---
title: 字符串填充 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 29b7f35f41ede90c0b5cc54e336fb1d3e331ef81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967747"
---
# <a name="string-padding-ssis"></a>字符串填充 (SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  表达式计算器不检查字符串是否包含前导空格和尾随空格，并且比较前不填充字符串来使其具有相同长度。 如果表达式需要字符串填充，可使用 + 运算符连接列值和空字符串。 有关详细信息，请参阅 [+（连接）（SSIS 表达式）](../../integration-services/expressions/concatenate-ssis-expression.md)。  
  
 另一方面，如果要删除空格，表达式计算器提供了 LTRIM、RTRIM 和 TRIM 函数，用于删除前导空格和/或尾随空格。 有关详细信息，请参阅 [LTRIM（SSIS 表达式）](../../integration-services/expressions/ltrim-ssis-expression.md)、[RTRIM（SSIS 表达式）](../../integration-services/expressions/rtrim-ssis-expression.md)和 [TRIM（SSIS 表达式）](../../integration-services/expressions/trim-ssis-expression.md)。  
  
> [!NOTE]  
>  LEN 函数将前导空格和尾随空格包含在其计数中。  
  
## <a name="related-content"></a>相关内容  
 pragmaticworks.com 上的技术文章 [SSIS 表达式小抄表](https://go.microsoft.com/fwlink/?LinkId=746575)。  
  
  
