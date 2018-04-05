---
title: 注释 (DMX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- comments [DMX]
- Data Mining Extensions [Analysis Services], comments
- double forward slashes
- commenting characters
- text strings [SQL Server]
- remarks [DMX]
- forward slash-asterisk character pairs
- DMX [Analysis Services], comments
- /*...*/ (comment)
- double hyphens
- // (comment)
- -- (comment character)
ms.assetid: 64d10eb5-4fe8-42c6-b387-eff336315e56
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 86fd2ea716fd0366149937af749c240fe01e486d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="comments-dmx"></a>（注释）(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  注释在数据挖掘扩展插件 (DMX) 是在程序中的文本字符串代码[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]不会执行。 注释又称为备注。 您可以使用注释对代码进行说明，或在诊断代码时临时禁用部分 DMX 语句或脚本。  
  
 使用注释对程序代码加以说明，可使您以后更为方便的维护代码。 可以使用注释记录一些详细信息，如程序名称、编写代码的开发人员姓名以及代码进行重要更改的日期等。 也可以使用注释说明复杂的计算过程或编程方法。  
  
 以下是编写注释的基本指南：  
  
-   您可以在注释中使用任何字母数字字符或符号。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将忽略注释中的所有字符。  
  
-   语句或脚本中的注释没有最大长度限制。 一条注释可由一行或多行组成。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持下列类型的注释字符：  
  
-   **（双正斜杠）。** 使用这些注释字符，您既可以在要执行的代码的行上编写注释，也可以在单独的行上编写注释。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会将从双正斜杠到行尾之间的所有内容均作为注释部分进行处理。 若要创建多行注释，请在每行注释的开头使用双正斜杠。 有关此注释字符的详细信息，请参阅[双正斜杠 &#40;注释 &#41;&#40; DMX &#41;](../dmx/double-slash-comment-dmx.md).  
  
-   **-（双连字符）。** 使用这些注释字符，您既可以在要执行的代码的行上编写注释，也可以在单独的行上编写注释。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会将从双连字符到行尾之间的所有内容均作为注释部分进行处理。 若要创建多行注释，请在每行注释的开头使用双连字符。 有关此注释字符的详细信息，请参阅[-&#40;注释 &#41;&#40; DMX &#41;摘要](../dmx/comment-dmx-summary.md)。  
  
-   **/\*...\*/ （正斜杠星号字符对）。** 使用这些注释字符，您既可以在要执行的代码的行上编写注释，也可以在单独的行上编写注释，甚至还可以在可执行代码中编写注释。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]计算开始注释对中的所有内容 (/ *) 到结束注释对 (\*/) 作为注释的一部分。 若要创建多行注释，以打开注释字符对开头的注释 (/\*)，日期和结束的结束注释字符对，对注释 (\*/)。 该类注释的任何行中都不应包含其他注释字符。 有关此注释字符的详细信息，请参阅[正斜杠星型 &#40;注释 &#41;&#40; DMX &#41;](../dmx/slash-star-comment-dmx.md).  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [结构和使用情况的 DMX 预测查询](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
