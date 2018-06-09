---
title: 分发 (DMX) |Microsoft 文档
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e4ffd21a2b507e03af6534296715528d83aac0f6
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841240"
---
# <a name="distributions-dmx"></a>分布 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，你可以在挖掘结构，以影响在创建挖掘模型时算法如何处理这些列中的数据中定义的列的内容。 对于某些算法，如果已知列中包含常用的值分布，则在处理模型之前定义任意连续列的分布将非常有用。 如果不定义分布，则由于算法据以解释数据的信息较少，生成的挖掘模型产生的预测可能不如定义了分布时产生的预测精确。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 数据挖掘算法支持下列分布类型：  
  
 **正常**  
 连续列的值构成一个正态高斯分布直方图。  
  
 **Log Normal**  
 连续列的值构成一个直方图，其中值的对数呈正态分布。  
  
 **统一**  
 连续列的值构成平坦曲线，曲线上的所有值都具有相同概率。  
  
 有关详细信息[!INCLUDE[msCoName](../includes/msconame-md.md)]数据挖掘算法，请参阅[数据挖掘算法&#40;Analysis Services-数据挖掘&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。 第三方算法提供程序可能支持其他分布类型。 要确定哪些分发类型的一种算法支持，请使用**SUPPORTED_DISTRIBUTION_FLAGS**架构行集。  
  
 有关分发类型的详细信息，请参阅[列分布&#40;数据挖掘&#41;](../analysis-services/data-mining/column-distributions-data-mining.md)。  
  
## <a name="see-also"></a>请参阅  
 [内容类型&#40;数据挖掘&#41;](../analysis-services/data-mining/content-types-data-mining.md)   
 [数据挖掘扩展插件&#40;DMX&#41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [数据挖掘扩展插件&#40;DMX&#41;函数引用](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [常规预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [结构和使用情况的 DMX 预测查询](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
