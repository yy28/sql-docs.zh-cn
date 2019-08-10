---
title: 使用情况 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b961282ba6bc25caa260a3e156f843a413a5ef1a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893115"
---
# <a name="usage-dmx"></a>用法 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  使用数据挖掘扩展插件 (DMX) 在中[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]定义新的数据挖掘模型时, 必须指定生成模型的数据挖掘算法将如何使用每个列。 可以将列指定为下列类型之一：  
  
-   **Key**  
  
-   **键顺序**  
  
-   **关键时间**  
  
-   **Predict**  
  
-   **PredictOnly**  
  
 在 DMX 中未指定的列被视为输入列。  
  
 若要正确处理一个挖掘模型，该算法必须了解唯一地标识每行的键列、用于创建预测的目标列（如果要创建预测模型）以及创建用于预测目标列的关系时所用的输入列。  
  
 指定为**预测**类型的列用作输入列和输出列。 指定为**PredictOnly**的列仅用作输出列。 具体的算法可能会以不同的方式处理预测列。  
  
 有关[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]支持的列使用类型的详细信息, 请参阅[挖掘模型列](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法 &#40;Analysis Services-数据挖掘&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [数据挖掘扩展插件 (DMX) 参考](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展&#40;插件&#41;的 DMX 语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [数据挖掘扩展&#40;插件&#41; DMX 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展&#40;插件&#41; DMX 运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展&#40;插件&#41; DMX 语句参考](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展&#40;插件&#41;的 DMX 语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [一般预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [DMX 预测查询的结构和用法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
