---
title: "分发 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- column distributions [DMX]
- distributions [DMX]
- DMX [Analysis Services], distributions
- Data Mining Extensions [Analysis Services], distributions
ms.assetid: cfbb9f38-ae71-401e-867f-15c6a2b6fb97
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4bc79c9a1c641f625a6a0dae11c17aba4188b5e8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
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
  
 有关详细信息[!INCLUDE[msCoName](../includes/msconame-md.md)]数据挖掘算法，请参阅[数据挖掘算法 &#40;Analysis Services-数据挖掘 &#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md). 第三方算法提供程序可能支持其他分布类型。 要确定哪些分发类型的一种算法支持，请使用**SUPPORTED_DISTRIBUTION_FLAGS**架构行集。  
  
 有关分发类型的详细信息，请参阅[列分布 &#40; 数据挖掘 &#41;](../analysis-services/data-mining/column-distributions-data-mining.md)。  
  
## <a name="see-also"></a>另请参阅  
 [内容类型 &#40; 数据挖掘 &#41;](../analysis-services/data-mining/content-types-data-mining.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [结构和使用情况的 DMX 预测查询](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
