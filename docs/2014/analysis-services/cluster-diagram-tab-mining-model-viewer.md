---
title: "\"分类关系图\" 选项卡（挖掘模型查看器） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.diagram.f1
ms.assetid: 180e6f48-5c4d-4160-b84d-608b98f7b840
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 127ff0c386a1f93c00178624b54499e33cf9042a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088009"
---
# <a name="cluster-diagram-tab-mining-model-viewer"></a>“分类关系图”选项卡（挖掘模型查看器）
  
  **“分类关系图”** 选项卡提供聚类分析模型中包含的所有分类的图形视图。  
  
 **有关详细信息：** [Microsoft 聚类分析算法](data-mining/microsoft-clustering-algorithm.md)、[使用 Microsoft 分类查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 从当前挖掘结构的挖掘模型中选择一个挖掘模型。 挖掘模型将在其关联的查看器中打开。  
  
 **查看器**  
 选择一个查看器以浏览选定挖掘模型。 可以使用一个自定义分类查看器或使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 挖掘内容查看器。 还可以使用插件查看器（如果有）。  
  
 **放大**  
 放大关系图以获取详细的分类视图。  
  
 **缩小**  
 缩小关系图以查看更多分类。  
  
 **复制图形视图**  
 将关系图的可见部分复制到剪贴板。  
  
 **复制整个图形**  
 将完整的关系图复制到剪贴板。  
  
 **缩放关系图以适应窗口**  
 缩小关系图，直到屏幕可容纳整个关系图。  
  
 **查找节点**  
 打开“查找节点”**** 对话框。 在难以找到所需属性的大型模型中，此功能很有用。 可以在该对话框中输入搜索条件，这将对分类视图进行筛选以仅显示包含搜索字符串的分类。  
  
 **改善布局**  
 对关系图中的分类进行重新排序以改善布局。  
  
 **密度**  
 使用此选项可更改分类关系图中显示的属性-值对。 使用 **“明暗度变量”** 选项选择一个属性，并使用 **“状态”** 选择一个值。 图形中的明暗度指示该属性-值对在分类中的密度。  
  
 如果选择 **“总体”** ，则关系图将显示每个分类的支持量，表示事例数目（自未选择属性开始）。  
  
 **“明暗度变量”**  
 选择一个属性以在分类图中显示。  
  
 **状态**  
 选择“明暗度变量”**** 的单个状态以在分类图中使用。  
  
 **链接**  
 通过上移或下移滑块来调整分类之间显示的链接数。 降低滑块将只保留分类之间的最强关联。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器 &#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
