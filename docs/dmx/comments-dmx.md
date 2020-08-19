---
description: （注释）(DMX)
title: DMX)  (注释 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8069241656de868ae2165fa7348b549c8e3308e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431119"
---
# <a name="comments-dmx"></a>（注释）(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  数据挖掘扩展插件中 (DMX) 的注释是不执行的程序代码中的文本字符串 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。 注释又称为备注。 您可以使用注释对代码进行说明，或在诊断代码时临时禁用部分 DMX 语句或脚本。  
  
 使用注释对程序代码加以说明，可使您以后更为方便的维护代码。 可以使用注释记录一些详细信息，如程序名称、编写代码的开发人员姓名以及代码进行重要更改的日期等。 也可以使用注释说明复杂的计算过程或编程方法。  
  
 以下是编写注释的基本指南：  
  
-   您可以在注释中使用任何字母数字字符或符号。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将忽略注释中的所有字符。  
  
-   语句或脚本中的注释没有最大长度限制。 一条注释可由一行或多行组成。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持下列类型的注释字符：  
  
-   **)  (双正斜杠。** 使用这些注释字符，您既可以在要执行的代码的行上编写注释，也可以在单独的行上编写注释。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会将从双正斜杠到行尾之间的所有内容均作为注释部分进行处理。 若要创建多行注释，请在每行注释的开头使用双正斜杠。 有关此注释字符的详细信息，请参阅 [&#41; &#40;DMX&#41;&#40;注释的双斜杠 ](../dmx/double-slash-comment-dmx.md)。  
  
-   **-- (双连字符) 。** 使用这些注释字符，您既可以在要执行的代码的行上编写注释，也可以在单独的行上编写注释。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会将从双连字符到行尾之间的所有内容均作为注释部分进行处理。 若要创建多行注释，请在每行注释的开头使用双连字符。 有关此注释字符的详细信息，请参阅 " [&#40;注释"&#41; &#40;DMX&#41; 摘要](../dmx/comment-dmx-summary.md)"。  
  
-   **/\* ... \*/ (正斜杠-星号字符对) 。** 使用这些注释字符，您既可以在要执行的代码的行上编写注释，也可以在单独的行上编写注释，甚至还可以在可执行代码中编写注释。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将打开的注释对中的所有内容都 (/* ) 为注释中 (/) 的结束注释对 \* 。 若要创建多行注释，请使用开放注释字符对（ (/) ）开始注释， \* 并以结束注释字符对 (\* /) 结束注释。 该类注释的任何行中都不应包含其他注释字符。 有关此注释字符的详细信息，请参阅 [斜线&#41;&#41; &#40;斜线 &#40;注释 ](../dmx/slash-star-comment-dmx.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;DMX&#41; 的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 语法元素的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [&#40;DMX&#41;的常规预测函数 ](../dmx/general-prediction-functions-dmx.md)   
 [DMX 预测查询的结构和用法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
