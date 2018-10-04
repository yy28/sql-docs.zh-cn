---
title: 数字数据格式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- integer data types [Integration Services]
- numeric data formats for fast parse
- locale-sensitive parsing [Integration Services]
- fast parse [Integration Services]
ms.assetid: fa3975ce-9d21-408a-857d-f85e30af27b0
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 92dc9782a00a55a9409bd5e87dd00a423002d200
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105437"
---
# <a name="numeric-data-formats"></a>数字数据格式
  快速分析提供了一组简单、快捷、不受区域设置影响的数据分析例程。 快速分析仅支持有限的一组整数数据类型格式。  
  
## <a name="integer-data-types"></a>整数数据类型  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 所提供的整数数据类型有：DT_I1、DT_UI1、DT_I2、DT_UI2、DT_I4、DT_UI4、DT_I8 和 DT_UI8。 有关详细信息，请参阅 [Integration Services 数据类型](data-flow/integration-services-data-types.md)。  
  
 快速分析支持下列整数数据类型的格式：  
  
-   零个或多个前导及尾随空格或制表位。 例如，“  123  ”是有效值。 全部是空格的值计算结果为零。  
  
-   前导加号、减号或无加减号。 例如，+123、-123 和 123 都是有效值。  
  
-   一位或多位阿拉伯数字 (0-9)。 例如，345 是有效值。 不支持其他语言的数字。  
  
 不支持下列数据格式：  
  
-   特殊字符。 例如，不支持货币字符“$”，因而无法分析值“$20”。  
  
-   空白字符，如换行符、回车符和不间断空格符。 例如，无法分析值“ 123”。  
  
-   以十六进制形式表示的整数。 例如，无法分析值 2EE。  
  
-   以科学记数法形式表示的整数。 例如，无法分析值 1E+10。  
  
 下列格式为整数的输出数据格式：  
  
-   负数用减号，正数不用符号。  
  
-   没有空白。  
  
-   一位或多位阿拉伯数字 (0-9)。  
  
  
