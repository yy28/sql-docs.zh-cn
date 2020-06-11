---
title: 比较运算符（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05bb9bc1ad4dfeed1cf2747a8d5bb854fec8d9af
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669698"
---
# <a name="operators---comparison"></a>运算符 - 比较
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  可以在中的任何数据挖掘扩展插件（DMX）表达式中将比较运算符与标量数据一起使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。 比较运算符计算结果为布尔数据类型，这些运算符可根据测试条件的结果返回 TRUE 或 FALSE。  
  
 下表标识了 DMX 支持的比较运算符。  
  
|运算符|说明|  
|--------------|-----------------|  
|[&#60; &#40;低于&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|对于计算结果为非 Null 值的参数，如果左侧的参数值小于右侧的参数值，则返回 TRUE；否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#62; &#40;大于&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|对于计算结果为非 null 值的参数，如果左侧的参数值大于右侧的参数值，则返回 TRUE;否则，返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[= &#40;等于&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|对于计算结果为非 null 值的参数，如果左侧的参数值等于右侧的参数值，则返回 TRUE;否则，返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#60;&#62; &#40;不等于&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|对于计算结果为非 null 值的参数，如果左侧的参数的值不等于右侧的参数值，则返回 TRUE;否则，返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#60;= &#40;小于或等于&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|对于计算结果为非 Null 值的参数，如果左侧的参数值小于或等于右侧的参数值，则返回 TRUE；否则返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
|[&#62;= &#40;大于或等于&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|对于计算结果为非 null 值的参数，如果左侧的参数值大于或等于右侧的参数值，则返回 TRUE;否则，返回 FALSE。 如果其中一个参数的计算结果为 Null 值或这两个参数的计算结果均为 Null 值，则该运算符返回 Null 值。|  
  
 还可以在 DMX 语句和函数中使用比较运算符来搜索条件。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;DMX&#41; 的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 语法元素的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [&#40;DMX&#41;的表达式](../dmx/expressions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)   
 [运算符 &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [DMX 预测查询的结构和用法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
