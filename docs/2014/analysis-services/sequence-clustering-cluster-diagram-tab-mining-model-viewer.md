---
title: "\"序列聚类分析\" 分类关系图选项卡（挖掘模型查看器 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.diagrams.f1
ms.assetid: 4b705397-9af4-4678-9eda-149bc5d762fa
author: minewiskan
ms.author: owend
ms.openlocfilehash: a3e27ccc67858edd8e1f95bb910300a93a3e0db8
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940748"
---
# <a name="sequence-clustering-cluster-diagram-tab-mining-model-viewer"></a>顺序分析和聚类分析的“分类关系图”选项卡（挖掘模型查看器）
  **“Microsoft 顺序分析和聚类分析查看器”** 中的 **“分类关系图”** 选项卡提供顺序分析和聚类分析模型包含的所有分类的图形化视图。  
  
 可以使用此顺序分析和聚类分析模型视图，从每个分类深入到支持事例（如果已启用钻取）。 还可以为分类指定说明性名称并更改明暗度变量，以直观的形式评估值分布。  
  
 **有关详细信息，请参阅 ** [Microsoft 顺序分析和聚类分析算法](data-mining/microsoft-sequence-clustering-algorithm.md)和[使用 Microsoft 序列分类查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 选择一个包含在当前挖掘结构中的挖掘模型以进行查看。 挖掘模型将在其关联的查看器中打开。  
  
 **查看器**  
 选择用于浏览选定挖掘模型的查看器。 您可以使用自定义查看器或 **“Microsoft 一般内容树查看器”**。 还可以使用插件查看器（如果有）。  
  
 **放大**  
 放大关系图以获取更详细的分类视图。  
  
 **缩小**  
 缩小关系图以查看模型中的所有分类。  
  
 **复制图形视图**  
 将关系图的可见部分复制到剪贴板。  
  
 **复制整个图形**  
 将完整的关系图复制到剪贴板。  
  
 **缩放关系图以适应窗口**  
 缩小关系图，直到屏幕可容纳整个关系图。  
  
 **查找节点**  
 使用“查找节点”**** 对话框可筛选图形中的分类，并更轻松地查找特定分类。 有关详细信息，请参阅[“查找节点”对话框（挖掘模型查看器）](find-node-dialog-box-mining-model-viewer.md)。  
  
 请注意，在此上下文中，您只会搜索分类的名称，而不搜索分类中的属性；因此，如果您已为分类指定说明性名称，则此选项最为有用。 可以通过右键单击每个分类并选择“重命名”****，在查看器中为分类指定名称。  
  
 **改善布局**  
 对关系图中的分类进行重新排序以改善布局。  
  
 **Density**  
 密度栏图形的外观及其包含的值依赖于你在“明暗度变量”**** 中选择的属性。  
  
-   如果未将任何属性状态选定为明暗度变量，则默认情况下应用于每个分类的密度明暗度表示对相应分类的支持（与事例总体相比）。  
  
-   若在 **“明暗度变量”** 中选择一个属性，则必须同时在 **“状态”** 中选择一个值。 在执行此操作时，密度栏图形将更新以显示此状态的概率。 可以将鼠标指针悬停在任一分类的上方来查看该分类的选定状态的概率。  
  
 **“明暗度变量”**  
 从挖掘模型中选择一个用于设置分类关系图的明暗度的属性。  
  
 **状态**  
 选择与“明暗度变量”**** 对应的状态。 例如，如果需要查看包含特定产品的序列，你会选择 [Product] 列作为“明暗度变量”**** 的属性，并选择特定产品名作为“状态”**** 的值。  
  
 **链接**  
 关系图中的线指示各个序列分类之间的关联。 通过调整分类右侧的滑块，可以调整查看器显示的链接数。 降低滑块将只显示最强链接。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器 &#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
