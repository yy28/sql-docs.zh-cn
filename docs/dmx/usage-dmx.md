---
title: "使用情况 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- column usage [DMX]
- Data Mining Extensions [Analysis Services], column usage types
- DMX [Analysis Services], column usage types
ms.assetid: 6d7ae72a-f5b5-4744-a3a2-46ccd6432c1a
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2acfde9b8d7c9d13fc626b006116e9b3760fd432
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="usage-dmx"></a>用法 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  当你使用数据挖掘扩展插件 (DMX) 来定义新的数据挖掘模型中[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，你必须指定如何生成模型的数据挖掘算法将使用每个列。 可以将列指定为下列类型之一：  
  
-   **Key**  
  
-   **键序列**  
  
-   **Key Time**  
  
-   **预测**  
  
-   **PredictOnly**  
  
 在 DMX 中未指定的列被视为输入列。  
  
 若要正确处理一个挖掘模型，该算法必须了解唯一地标识每行的键列、用于创建预测的目标列（如果要创建预测模型）以及创建用于预测目标列的关系时所用的输入列。  
  
 指定为列**预测**类型用作输入和输出列。 指定为列**PredictOnly**仅用作输出列。 具体的算法可能会以不同的方式处理预测列。  
  
 有关详细信息的列使用情况类型[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]支持，请参阅[挖掘模型列](../analysis-services/data-mining/mining-model-columns.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services-数据挖掘 &#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [结构和使用情况的 DMX 预测查询](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  

