---
title: 序列聚类分析群集对比选项卡 （挖掘模型查看器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.discrimination.f1
ms.assetid: 7dd16479-2633-4f4b-83bf-cf55972a2241
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d4debc43286ffb3fe4f87115ed15e9b4c3f74b06
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187144"
---
# <a name="sequence-clustering-cluster-discrimination-tab-mining-model-viewer"></a>顺序分析和聚类分析的“分类对比”选项卡（挖掘模型查看器）
  **“Microsoft 顺序分析和聚类分析查看器”** 中的 **“分类对比”** 选项卡将比较顺序分析和聚类分析模型中的所选分类。  
  
 可以使用此顺序分析和聚类分析模型视图，比较两个分类并查看哪些状态和转换是不同的。  
  
 **有关详细信息，请参阅** [Microsoft 顺序分析和聚类分析算法](data-mining/microsoft-sequence-clustering-algorithm.md)和[使用 Microsoft 序列分类查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>“常规”  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 选择一个包含在当前挖掘结构中的挖掘模型以进行查看。 挖掘模型将在其关联的查看器中打开。  
  
 **查看器**  
 选择用于浏览选定挖掘模型的查看器。 您可以使用自定义查看器或 **“Microsoft 一般内容树查看器”**。 还可以使用插件查看器（如果有）。  
  
 **分类 1**  
 从模型的分类中选择一个分类。  
  
 **群集 2**  
 从挖掘模型的分类中选择第二个分类，与 **“分类 1”** 进行比较。  
  
 如果您不选择其他分类，则默认情况下，所选分类将会与其补数进行比较，这表示模型中不属于分类 1 的所有事例。  
  
 **对比分数\<聚类 1 > 和\<分类 2 >**  
 此图表提供所选分类的详细比较。 一般情况下，聚类分析模型很少以独占方式为单个分类分配状态或值。 因此，查看器仅指示特定属性或状态 *倾向于* 某个特定分类。  
  
 总体上而言，某个特定分类可能包含多个状态：例如，常见状态可能为依次购买 Water Bottle 和 Water Bottle Cage。 但是，相应的顺序可能存在于包含更重要的定义特征的其他分类中。 例如，另一个分类最主要的特点可能是事务时间非常短，并且分析表明，Water Bottle 和 Water Bottle Cage 项可能通常分组到此分类中，但并不总是这样。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**变量**|挖掘模型中的属性。|  
|**值**|**“变量”** 中列出的属性的状态。|  
|**倾向于\<聚类 1 >**|包含一个阴影条，指示 **“变量”** 和 **“值”** 中列出的属性和状态倾向于 **“分类 1”** 中的所选分类的程度。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法&#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器&#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
