---
title: "\"决策树\" 选项卡（挖掘模型查看器） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.decisiontree.f1
ms.assetid: dc88606f-ba7c-4f8d-af65-bfa17ec16e2b
author: minewiskan
ms.author: owend
ms.openlocfilehash: b13eb819edc2a33117d45954423466343f5de18a
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528871"
---
# <a name="decision-tree-tab-mining-model-viewer"></a>“决策树”选项卡（挖掘模型查看器）
  “决策树”**** 窗格直观地显示在决策树模型中创建的决策规则。 决策规则描述通向某个特定结果的路径。  
  
 **有关详细信息：** [Microsoft 决策树算法](data-mining/microsoft-decision-trees-algorithm.md)、[使用 Microsoft 树查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 从当前挖掘结构的挖掘模型中选择一个挖掘模型。 挖掘模型将在其关联的查看器中打开。  
  
 **查看器**  
 选择用于浏览所选挖掘模型的查看器。 可以使用自定义查看器或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 挖掘内容查看器。 还可以使用插件查看器（如果有）。  
  
 **放大**  
 放大以获取决策树中节点和分支的更详细视图。 在复杂模型中，决策树可具有多个分支级别。  
  
 **缩小**  
 缩小以获取树结构的总体视图。  
  
 **复制图形视图**  
 将关系图的可见部分复制到剪贴板。  
  
 **复制整个图形**  
 将完整的关系图复制到剪贴板。  
  
 **缩放关系图以适应窗口**  
 缩小关系图，直到屏幕可容纳整个树结构。  
  
 **直方图**  
 选择可在每个节点的直方图中显示的状态数。 如果模型中的状态数小于所选的值，则将不显示附加条形。  
  
 **视图**  
 选择要在查看器中显示的树。 如果创建一个包含多个可预测属性的模型，则算法将为每个可预测属性创建一个单独的树。  
  
 **背景**  
 选择用于表示每个节点的背景色的可预测属性值。 例如，在示例 AdventureWorks 模型中，如果将“背景”**** 设置为 1 ([Bike Buyer] = Yes)，则自行车购买者数的比例较大的时候，节点会具有较深的阴影。 此选项提供有关树中分支和节点的含义的其他可视化提示。  
  
 **默认扩展**  
 从列表中选择一个值可设置树图形中显示的级别数的默认值。  
  
 **显示级别**  
 向右或向左移动滑动条可调整树图形中显示的级别数。 若要查看模型中的所有节点，请将滑动条一直向右移动。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器 &#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
