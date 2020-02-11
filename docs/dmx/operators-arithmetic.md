---
title: 算术运算符（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e78241252733e8298c0bc727f9c45dd6df2768ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008213"
---
# <a name="operators---arithmetic"></a>运算符 - 算术
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  可以在数据挖掘扩展插件（DMX）中使用算术运算符来实现中[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的算术计算，包括加、减、乘和除。  
  
 下表标识了 DMX 支持的算术运算符。  
  
|操作员|说明|  
|--------------|-----------------|  
|[+ &#40;添加&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|将两个数相加。|  
|[-&#40;减去&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|从一个数中减去另一个数。|  
|[&#42; &#40;乘&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|将一个数与另一个数相乘。|  
|[&#40;除以&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|将一个数除以另一个数。|  
  
 下列规则确定了各种运算符在 DMX 表达式中的优先顺序：  
  
-   如果表达式中有多个算术运算符，则先计算乘除，后计算加减。  
  
-   如果表达式中的所有算术运算符具有相同的优先顺序，则运算顺序为从左到右。  
  
-   括号中的表达式运算优先于其他所有运算。  
  
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
  
  
