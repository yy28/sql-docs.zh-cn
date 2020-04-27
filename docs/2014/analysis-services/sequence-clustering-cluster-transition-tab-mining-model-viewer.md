---
title: 顺序分析群集 "分类转换" 选项卡（挖掘模型查看器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.transition.f1
ms.assetid: 40aef457-d69f-4905-a2d3-924c37bd3d97
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a236805ac047b351aa49c2486b8acac84818017
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66069082"
---
# <a name="sequence-clustering-cluster-transition-tab-mining-model-viewer"></a>顺序分析和聚类分析的“分类转换”选项卡（挖掘模型查看器）
  可以使用“Microsoft 顺序分析和聚类分析查看器”**** 中的“状态转换”**** 选项卡，更仔细地查看选定分类中的各个属性-值对或状态之间的转换。  
  
 使用此顺序分析和聚类分析模型视图可查看模式。 在关系图中，链接表示转换的概率，节点则表示序列状态。  
  
 **有关详细信息，请参阅 ** [Microsoft 顺序分析和聚类分析算法](data-mining/microsoft-sequence-clustering-algorithm.md)和[使用 Microsoft 序列分类查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 选择一个包含在当前挖掘结构中的挖掘模型以进行查看。 挖掘模型将在其关联的查看器中打开。  
  
 **查看器**  
 选择用于浏览选定挖掘模型的查看器。 您可以使用自定义查看器或 **“Microsoft 一般内容树查看器”**。 还可以使用插件查看器（如果有）。  
  
 **放大**  
 放大关系图以更好地查看状态。  
  
 **缩小**  
 缩小关系图以获取分类中的状态的整体视图。  
  
 **复制图形视图**  
 将关系图的可见部分复制到剪贴板。  
  
 **复制整个图形**  
 将完整的关系图复制到剪贴板。  
  
 **聚集**  
 选择要在查看器中显示的分类。 默认情况下，“总体(全部)”**** 处于选中状态，这意味着整个模型中的状态和转换都包含在图形中。 在选择某个特定分类时，仅显示该分类中的状态和转换。  
  
 **提示：** 可以使用 "**分类关系图**" 选项卡重命名群集。只需选择一个分类，右键单击，然后选择 "**重命名**"。 通过使用更具说明性的标签来对分类进行重命名，可使得在 **“状态转换”** 选项卡中比较分类变得更容易。  
  
 **显示边缘标签**  
 选择此选项可在图形的每个边缘上显示一些数字来指示转换概率。  
  
 **链接**  
 使用滑块可控制图表中显示的状态数和转换数。 降低滑块将只显示具有最高概率的状态和转换。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器 &#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
