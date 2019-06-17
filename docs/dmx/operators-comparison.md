---
title: 比较运算符 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8049f2bad6e78ff301b460b1375a0a73807ccd8d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62501949"
---
# <a name="operators---comparison"></a>运算符 - 比较
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  可以对任何数据挖掘扩展插件 (DMX) 表达式中的标量数据使用比较运算符[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。 比较运算符计算结果为布尔数据类型，这些运算符可根据测试条件的结果返回 TRUE 或 FALSE。  
  
 下表标识了 DMX 支持的比较运算符。  
  
|运算符|Description|  
|--------------|-----------------|  
|[&#60;&#40;小于&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|对于计算结果为非 Null 值的参数，如果左侧的参数值小于右侧的参数值，则返回 TRUE；否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#62;&#40;大于&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|对于计算结果为非 null 值的参数，返回 TRUE 左侧参数的值是否大于右侧; 参数的值否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[=&#40;等于&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|对于计算结果为非 null 值的参数，返回 TRUE 左侧参数的值是否等于右侧; 参数的值否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#60;&#62;&#40;不等于&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|对于计算结果为非 null 值的参数，返回 TRUE 左侧参数的值是否不等于右侧; 参数的值否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#60;=&#40;小于或等于&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|对于计算结果为非 Null 值的参数，如果左侧的参数值小于或等于右侧的参数值，则返回 TRUE；否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#62;=&#40;大于或等于&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|对于计算结果为非 null 值的参数，返回 TRUE，在左侧参数的值是否大于或等于自变量的值在右侧;否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
  
 还可以在 DMX 语句和函数中使用比较运算符来搜索条件。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件 (DMX) 参考](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [表达式&#40;DMX&#41;](../dmx/expressions-dmx.md)   
 [通用预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [DMX 预测查询的结构和用法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
