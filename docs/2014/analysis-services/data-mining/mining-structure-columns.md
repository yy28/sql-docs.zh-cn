---
title: 挖掘结构列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], structure
- mining structures [Analysis Services], columns
- data sources [Analysis Services], mining structure columns
- columns [data mining], mining structure columns
ms.assetid: 20cbf433-70d1-4b61-a462-41a8435b27b4
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 29a8577ee503668dd3bae72441155abc5977073a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37284203"
---
# <a name="mining-structure-columns"></a>挖掘结构列
  创建挖掘结构时，通过选择外部数据的列，然后指定如何将数据用于建模来定义挖掘结构中的列。 因此，挖掘结构列不仅仅是数据源的数据副本：它们定义挖掘模型要如何使用数据源的数据。 您可以分配确定数据如何离散化的属性以及说明数据值如何分布的属性。  
  
 挖掘结构列设计得很灵活且可扩展，这是因为用于生成挖掘模型的每种算法可以使用该结构中的不同列来解释数据。 不需要为每个模型提供一个数据集，您可以使用单个挖掘结构并使用其中的列来自定义每个模型的数据。  
  
## <a name="defining-mining-structure-columns"></a>定义挖掘结构列  
 定义结构列的基本数据类型和内容类型是从用于创建该结构的数据源中派生的。 可以更改挖掘结构中的这些设置，还可以设置建模标志以及为连续列设置分发。  
  
 挖掘结构列的定义必须包含以下信息：  
  
-   **ID**：列的唯一名称，通常与名称相同。 在创建挖掘结构后将不能更改它，但是可以更改名称。  
  
-   **名称**：列的名称或别名。  
  
-   **内容**：一个说明数据是离散的还是连续的枚举。  
  
-   **类型**：一个指示一般数据类型的枚举。  
  
-   **分布**：一个说明值的预期分布的枚举。 如果该列为连续列，则包含分发。  
  
-   **建模标志**：一个指示如何处理缺失值等等的枚举。 还可以对挖掘模型定义建模标志，但是模型标志不同于对结构列使用的标志。  
  
-   **绑定**：指定源数据的属性。  
  
 第三方算法还可以包含可以为挖掘结构列定义的自定义属性。  
  
 有关数据挖掘结构和数据挖掘模型的详细信息，请参阅[挖掘结构&#40;Analysis Services-数据挖掘&#41;](mining-structures-analysis-services-data-mining.md)。  
  
## <a name="related-content"></a>相关内容  
 有关如何定义和使用挖掘结构列的详细信息，请参阅下列主题：  
  
|主题|链接|  
|-----------|-----------|  
|介绍可用于定义挖掘结构列的数据类型。|[数据类型&#40;数据挖掘&#41;](data-types-data-mining.md)|  
|说明挖掘结构列中包含的每个数据类型可用的内容类型。 内容类型依赖于数据类型。 内容类型在模型级别上分配，确定模型如何使用列数据。|[内容类型&#40;数据挖掘&#41;](content-types-data-mining.md)|  
|介绍嵌套表的概念，并说明如何将嵌套表作为挖掘结构列添加到数据源。|[已分类列&#40;数据挖掘&#41;](classified-columns-data-mining.md)|  
|列出和说明可以对挖掘结构列设置的分布属性，以指定列中值的预期分布。|[列分布&#40;数据挖掘&#41;](column-distributions-data-mining.md)|  
|说明离散化的概念（有时称为“装箱”），并说明 Analysis Services 提供的将连续数值数据离散化的方法。|[离散化方法&#40;数据挖掘&#41;](discretization-methods-data-mining.md)|  
|说明可对挖掘结构列设置的建模标志。|[建模标志&#40;数据挖掘&#41;](modeling-flags-data-mining.md)|  
|说明已分类列，可以使用这种特殊列类型将一个挖掘结构列与另一个挖掘结构列关联。|[已分类列&#40;数据挖掘&#41;](classified-columns-data-mining.md)|  
|了解如何添加和修改挖掘结构列。|[挖掘结构任务和操作指南](mining-structure-tasks-and-how-tos.md)|  
  
## <a name="see-also"></a>请参阅  
 [挖掘结构&#40;Analysis Services-数据挖掘&#41;](mining-structures-analysis-services-data-mining.md)   
 [挖掘模型列](mining-model-columns.md)  
  
  
