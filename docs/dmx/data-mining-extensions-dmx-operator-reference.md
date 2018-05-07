---
title: 数据挖掘扩展插件 (DMX) 运算符参考 |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- operators [DMX]
- DMX [Analysis Services], operators
- Data Mining Extensions [Analysis Services], operators
ms.assetid: a6d747c0-9ff0-475f-86cd-34bebd79c21a
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 1f9a7d4921ce1f5fd82eb832f9ed66550931a218
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-extensions-dmx-operator-reference"></a>数据挖掘扩展插件 (DMX) 运算符参考
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  中的数据挖掘扩展插件 (DMX) 语言[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]支持算术运算符、 分配、 比较、 逻辑和一元运算符。 下表列出了 DMX 支持的运算符。  
  
|运算符|Description|  
|--------------|-----------------|  
|[+&#40;添加&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|将两个数相加的算术运算符。|  
|[-&#40;减去&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|从一个数中减去另一个数的算术运算符。|  
|[&#42;&#40;乘&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|将一个数与另一个数相乘的算术运算符。|  
|[&#40;将划分&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|将一个数除以另一个数的算术运算符。|  
|[&#60;&#40;小于&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|一个比较运算符。 计算结果为非 null 值的自变量，则返回 TRUE 左侧参数的值是否小于右侧; 自变量的值否则，返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#62;&#40;大于&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|一个比较运算符。 对于计算结果为非 Null 值的参数，如果左侧的参数值大于右侧的参数值，则返回 TRUE；否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[=&#40;等于&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|一个比较运算符。 对于计算结果为非 Null 值的参数，如果左侧的参数值等于右侧的参数值，则返回 TRUE；否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#60;&#62;&#40;不等于&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|一个比较运算符。 对于计算结果为非 Null 值的参数，如果左侧的参数值不等于右侧的参数值，则返回 TRUE；否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#60;=&#40;小于或等于&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|一个比较运算符。 如果左侧参数的值小于或等于右侧; 自变量的值，则计算结果为非 null 值的自变量，返回 TRUE否则，返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#62;=&#40;大于或等于&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|一个比较运算符。 对于计算结果为非 Null 值的参数，如果左侧的参数值大于或等于右侧的参数值，则返回 TRUE；否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[和&AMP;#40;DMX&AMP;#41;](../dmx/and-dmx.md)|对两个数值表达式执行“与”运算的逻辑运算符。|  
|[不&AMP;#40;DMX&AMP;#41;](../dmx/not-dmx.md)|对一个数值表达式执行“求反”运算的逻辑运算符。|  
|[或者&AMP;#40;DMX&AMP;#41;](../dmx/or-dmx.md)|对两个数值表达式执行“或”运算的逻辑运算符。|  
|[+&#40;正&#41; &#40;DMX&#41;](../dmx/positive-dmx.md)|一元运算符，返回数值表达式的正值。|  
|[-&#40;负&#41; &#40;DMX&#41;](../dmx/negative-dmx.md)|一元运算符，返回数值表达式的负值。|  
|[双斜线&#40;注释&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)|指示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不应执行的文本字符串。 您可以在 DMX 语句中嵌入注释，将其加在代码行末尾，或者单独插入一行。|  
|[-&#40;注释&#41; &#40;DMX&#41;摘要](../dmx/comment-dmx-summary.md)|指示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不应执行的文本字符串。 您可以在 DMX 语句中嵌入注释，将其加在代码行末尾，或者单独插入一行。|  
|[正斜杠星型&#40;注释&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)|指示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不应执行的文本字符串。 您可以在 DMX 语句中嵌入注释，将其加在代码行末尾，或者单独插入一行。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;函数引用](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 & #40; DMX & #41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 & #40; DMX & #41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [运算符&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
