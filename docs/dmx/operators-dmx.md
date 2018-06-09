---
title: 运算符 (DMX) |Microsoft 文档
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 072d0a36a4803f4de1d50ba066e4e86e5d171c5c
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842880"
---
# <a name="operators-dmx"></a>运算符 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  你可以使用数据挖掘扩展插件 (DMX) 运算符中的查询中执行算术、 比较、 串联运算符和逻辑运算[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用运算符执行下列运算：  
  
-   搜索满足特定条件的值或对象。  
  
-   在值或表达式之间进行判断。  
  
 DMX 使用多种类别的运算符，这些运算符将在以后各节中加以说明。 有关各个运算符的其他信息，请参阅[数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)。  
  
|运算符类别|类型的操作|  
|-----------------------|-----------------------|  
|[算术运算符&#40;DMX&#41;](../dmx/operators-arithmetic.md)|执行加、减、乘或除运算。|  
|[比较运算符&#40;DMX&#41;](../dmx/operators-comparison.md)|将一个值与另一个值或表达式比较。|  
|[逻辑运算符&#40;DMX&#41;](../dmx/operators-logical.md)|测试条件的真实性，如 AND、OR 或 NOT。|  
|[一元运算符&#40;DMX&#41;](../dmx/operators-unary.md)|对单个操作数执行运算。|  
  
 可以使用运算符将 DMX 中较小的表达式组合为较复杂的表达式。 在复杂的表达式中，系统将根据 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 定义的运算符优先顺序，按顺序进行运算。 具有较高优先顺序的运算符先于低优先顺序的运算符进行计算。 有关表达式的详细信息，请参阅[表达式&#40;DMX&#41;](../dmx/expressions-dmx.md)。  
  
 将简单表达式组合为复杂的表达式时，生成的表达式的数据类型取决于运算符规则与数据类型优先顺序规则的组合。 如果结果是一个字符或 Unicode 值，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 通过组合运算符规则和排序规则优先顺序来确定结果的排序规则。 另外还有一些规则，根据简单表达式的精度、小数位数和长度来确定结果的精度、小数位数和长度。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;函数引用](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [常规预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [结构和使用情况的 DMX 预测查询](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
