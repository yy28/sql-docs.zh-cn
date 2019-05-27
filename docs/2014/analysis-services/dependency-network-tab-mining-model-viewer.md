---
title: 依赖关系网络选项卡 （挖掘模型查看器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.dependencynetwork.f1
ms.assetid: e58ce1b7-20d6-42cb-ade5-916da8471e09
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 819a69ad9c1b1415726d816e2cbc1faa92bd6cd1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081943"
---
# <a name="dependency-network-tab-mining-model-viewer"></a>“依赖关系网络”选项卡（挖掘模型查看器）
  **“依赖关系网络”** 选项卡提供挖掘模型所包含的所有属性的图形视图，并显示这些属性之间的关系。  
  
 **“依赖关系网络”**  选项卡用于多种类型的挖掘模型，包括 Naïve Bayes 模型、决策树模型和关联模型。 有关如何在这些模型的上下文中解释 **“依赖关系网络”**  选项卡的内容的详细信息，请参阅以下链接：  
  
 [使用 Microsoft 树查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
 [使用 Microsoft Naive Bayes 查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
 [使用 Microsoft 关联规则查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 从当前挖掘结构的挖掘模型中选择一个挖掘模型以进行查看。 挖掘模型将在自定义查看器中打开。 用于每个模型的自定义查看器的类型由您用来创建该模型的算法决定。  
  
 **Viewer**  
 选择用于浏览所选挖掘模型的查看器。 对于每个挖掘模型，可以使用为其提供的自定义查看器，也可以使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 挖掘内容查看器。 还可以使用插件查看器（如果有）。 Microsoft 内容树查看器可用于所有模型，并表示 HTML 表中的模型内容。  
  
 **放大**  
 放大关系图，以便能更详细地查看属性。  
  
 **缩小**  
 缩小关系图，以便能查看更多属性以及这些属性之间的链接。  
  
 **复制图形视图**  
 将关系图的可见部分复制到剪贴板。  
  
 **复制整个图形**  
 将完整的关系图复制到剪贴板。  
  
 **Links**  
 通过调整属性右侧的滑块，可以调整查看器显示的链接（边缘）数和节点数。 向下拖动滑动条将增大阈值，以便只显示最强链接。 对于每种模型类型，均使用一个略为不同的值来表示图形中的链接：  
  
-   在 **决策树** 模型中，边缘表示连接的预测强度（部分地由拆分分数决定）。  
  
-   在 **Naïve Bayes** 模型中，两个节点之间的链接可以在任一方向上进行：也就是说，节点 A 可预测节点 B，节点 B 也可预测节点 A。 与边缘关联的分数表示连接的预测强度。  
  
-   在 **关联模型**中，节点之间的边缘表示包含连接两个项集的规则的重要性分数。  
  
 所有模型类型的一般规则是：链接越强，两个属性之间的预测关系就越强。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法 &#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器（数据挖掘模型设计器）](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
