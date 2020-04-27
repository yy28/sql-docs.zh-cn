---
title: 数据类型（数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data types [data mining]
- columns [data mining], data types
- data mining [Analysis Services], data types
ms.assetid: 4af5b7db-790b-459c-b2b4-00f0cf6b5ce4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc810f56d552fa17cb027598a25bde114a696375
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084803"
---
# <a name="data-types-data-mining"></a>数据类型（数据挖掘）
  在中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]创建挖掘模型或挖掘结构时，必须为挖掘结构中的每个列定义数据类型。 数据类型告知数据挖掘引擎数据源中的数据是数值还是文本以及应如何处理数据。 例如，如果数据源中包含数值数据，则可以指定是将数字作为整数处理还是使用小数位数来处理。  
  
 每种数据类型支持一种或多种内容类型。 通过设置内容类型，您可以自定义在挖掘模型中如何处理或计算列中的数据。  
  
 例如，如果列中有数值数据，您可以选择将其作为数值数据类型或文本数据类型来处理。 如果选择数值数据类型，则可以设置几种不同的内容类型：可以使数字离散化或者将数字作为连续值处理。 有关所有内容类型列表的信息，请参阅 [内容类型（数据挖掘）](content-types-data-mining.md)。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持挖掘结构列的以下数据类型：  
  
|数据类型|支持的内容类型|  
|---------------|-----------------------------|  
|`Text`|Cyclical、Discrete、Discretized、Key Sequence、Ordered 和 Sequence|  
|`Long`|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered、Sequence 和 Time<br /><br /> Classified|  
|`Boolean`|Cyclical、Discrete 和 Ordered|  
|`Double`|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered、Sequence 和 Time<br /><br /> Classified|  
|`Date`|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time 和 Ordered|  
  
> [!NOTE]  
>  只有第三方算法支持 Time 和 Sequence 内容类型。 支持 Cyclical 和 Ordered 内容类型，但大多数算法将它们视为离散值，不会进行特殊处理。  
  
## <a name="specifying-a-data-type"></a>指定数据类型  
 如果直接使用数据挖掘扩展插件 (DMX) 创建挖掘模型，则可以在定义该模型时定义每一列的数据类型，同时 Analysis Services 将创建对应的包含指定数据类型的挖掘结构。 如果通过使用向导创建挖掘模型或挖掘结构，Analysis Services 将建议一种数据类型，或者您可以从列表中选择一种数据类型。  
  
## <a name="changing-a-data-type"></a>更改数据类型  
 如果更改某一列的数据类型，则必须始终重新处理挖掘结构以及基于该结构的所有挖掘模型。 有时候，如果更改数据类型，则可能无法再在特定的模型中使用该列。 在这种情况下，Analysis Services 将在您重新处理该模型时引发一个错误，或者将处理该模型但忽略该特定列。  
  
## <a name="see-also"></a>另请参阅  
 [内容类型 &#40;数据挖掘&#41;](content-types-data-mining.md)   
 [内容类型 &#40;DMX&#41;](/sql/dmx/content-types-dmx)   
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘结构 &#40;Analysis Services 数据挖掘&#41;](mining-structures-analysis-services-data-mining.md)   
 [DMX&#41;的数据类型 &#40;](/sql/dmx/data-types-dmx)   
 [挖掘模型列](mining-model-columns.md)   
 [挖掘结构列](mining-structure-columns.md)  
  
  
