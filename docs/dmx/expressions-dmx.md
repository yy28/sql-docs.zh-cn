---
title: 表达式（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0e1bd5fa1ba4d4ff8b97436ac6e44b901f578187
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68074842"
---
# <a name="expressions-dmx"></a>表达式 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在数据挖掘扩展插件（DMX）中，表达式是标识符、值和运算符的组合，可以[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]计算该值以获得结果。  
  
 DMX 表达式可能很简单，也可能很复杂。 简单表达式可以是下列几种形式之一：  
  
 Constant  
 常量是表示单个特定值的符号。 常量可以是字符串、数值或日期值。 必须使用单引号 (') 来分隔字符串和日期常量。  
  
 标量函数  
 标量函数将返回单个值。  
  
 非标量函数  
 非标量函数将返回一个表。  
  
 对象标识符  
 在 DMX 中，对象标识符被视为简单表达式。  
  
 若要生成复杂表达式，可以使用运算符将这些表达式组合起来。 有关运算符的详细信息，请参阅[数据挖掘扩展插件 &#40;DMX&#41; Operator Reference](../dmx/data-mining-extensions-dmx-operator-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;DMX&#41; 的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 语法元素的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)   
 [DMX 预测查询的结构和用法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
