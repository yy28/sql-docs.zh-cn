---
title: 挖掘模型列 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- columns [data mining], mining model columns
- columns [data mining]
- REGRESSOR column
- columns [data mining], modeling flags
- modeling flags [data mining]
- MODEL_EXISTENCE_ONLY column
- usage property [data mining]
ms.assetid: fab47643-5bfd-424e-a0f7-69e665db6bab
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a982333d62398da617c7eae40c48a05181494c0c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027334"
---
# <a name="mining-model-columns"></a>挖掘模型列
  数据挖掘模型为挖掘结构表示的数据应用挖掘模型算法。 如挖掘结构一样，挖掘模型也包含列。 挖掘模型包含在挖掘结构之内，继承由挖掘结构定义的所有属性值。 该模型可以使用挖掘结构包含的所有列，或使用其中一部分列。  
  
 您还可以为挖掘模型列定义另外两条信息：用法和建模标志。  
  
-   **用法** 是一个属性，它定义模型如何使用列。 列可用作输入列、键列或可预测列。  
  
-   **建模标志** 为算法提供有关事例表中定义的数据的附加信息，以便算法可以生成更精确的模型。 可以使用数据挖掘扩展插件 (DMX) 语言以编程的方式定义建模标志，也可以在 **的** 数据挖掘设计器 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中定义建模标志。  
  
 下面介绍了可以为挖掘模型列定义的建模标志。  
  
 `MODEL_EXISTENCE_ONLY`  
 指示属性的存在比属性列中的值更为重要。 例如，假定一个事例表包含与特定用户相关联的一系列订单项。 表数据包括产品类型、ID 和每项的费用。 对于建模来说，客户购买了某特定订单项这个事实可能比订单项本身的费用更重要。 在这种情况下，费用列应标记为 `MODEL_EXISTENCE_ONLY`。  
  
 `REGRESSOR`  
 指示该算法可以在回归算法的回归公式中使用指定列。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法支持该标志。  
  
 有关使用 DMX 以编程方式设置用法属性和定义建模标志的详细信息，请参阅 [CREATE MINING MODEL (DMX)](/sql/dmx/create-mining-model-dmx)。 有关在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中设置用法属性和定义建模标志的详细信息，请参阅[移动数据挖掘对象](moving-data-mining-objects.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法&#40;Analysis Services-数据挖掘&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘结构&#40;Analysis Services-数据挖掘&#41;](mining-structures-analysis-services-data-mining.md)   
 [更改挖掘模型的属性](change-the-properties-of-a-mining-model.md)   
 [从挖掘模型中排除列](exclude-a-column-from-a-mining-model.md)   
 [挖掘结构列](mining-structure-columns.md)  
  
  
