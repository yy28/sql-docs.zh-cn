---
title: 建模标志（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7e05d629f46f1c94bbe9305510daf37c09a39c9b
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969018"
---
# <a name="modeling-flags-dmx"></a>建模标志 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  可以在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中使用建模标志，为数据挖掘算法提供有关事例表中定义的数据的附加信息。 该算法可以使用该附加信息生成更精确的数据挖掘模型。 可以同时在挖掘结构列和挖掘模型列中定义建模标志。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持下列建模标志：  
  
 **NOT NULL**  
 属性列的值不应包含 Null 值。 如果 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在模型定型过程中发现该属性列的值为 Null 值，则将出现错误。 该标志是在挖掘结构列中定义的。  
  
 **回归量**  
 指示该算法可以在回归算法的回归公式中使用指定列。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 线性回归算法和 [!INCLUDE[msCoName](../includes/msconame-md.md)] 决策树算法支持该标志，并在挖掘模型列中定义该标志。  
  
 **MODEL_EXISTENCE_ONLY**  
 是否存在特性比特性列值更重要。 该标志是在挖掘模型列中定义的。  
  
 第三方算法可能支持其他建模标志。 若要确定算法支持的建模标志，请使用**SUPPORTED_MODELING_FLAGS**架构行集。 您还可以查询服务器上的挖掘服务，以确定特定算法支持哪些建模标志。 例如，下面的查询返回当前服务器上 Microsoft 线性回归算法支持的建模标志：  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 预期的结果：  
  
 NOT NULL,REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>在挖掘模型中指定建模标志  
 有关 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持对挖掘结构列指定标志的语法的示例，请参阅[CREATE 挖掘 STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md)。  
  
 有关在挖掘模型列上指定建模标志的语法的示例，请参阅[ALTER 挖掘 STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md)。  
  
 有关使用挖掘模型列的详细信息，请参阅[挖掘模型列](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [&#40;DMX&#41; 的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-reference.md)   
 [&#40;DMX&#41; 语法元素的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)   
 [DMX 预测查询的结构和用法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
