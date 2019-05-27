---
title: 模型选项卡 （挖掘模型查看器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.timeseries.decisiontree.f1
ms.assetid: 50570bb4-fcac-411e-b530-0398437efda7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05c0a25ceded07264e4dbe10467e9dc6f093f6c0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077623"
---
# <a name="model-tab-mining-model-viewers"></a>“模型”选项卡（挖掘模型查看器）
  Microsoft 时序查看器中的 **“模型”** 选项卡会将时序的表示形式显示为图形中的节点，这与决策树模型中采用的方式类似。  
  
 使用此时序模型视图可提取有关时序分析的有用信息，包括图形的公式、ARIMA 术语和系数。  
  
 **有关详细信息：**[Microsoft 时序算法](data-mining/microsoft-time-series-algorithm.md)，[使用 Microsoft 时序查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)， [Microsoft 时序算法](data-mining/microsoft-time-series-algorithm.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 选择要查看的挖掘模型。 挖掘模型将在其关联的查看器中打开。  
  
 **Viewer**  
 选择用于浏览所选挖掘模型的查看器。 可以对此模型类型使用自定义查看器，也可以使用 **“Microsoft 一般内容树查看器”** 。 还可以使用插件查看器（如果有）。  
  
 **放大**  
 放大关系图。  
  
 **缩小**  
 缩小关系图。  
  
 **复制图形视图**  
 将关系图的可见部分复制到剪贴板。  
  
 **复制整个图形**  
 将完整的关系图复制到剪贴板。  
  
 **缩放关系图以适应窗口**  
 缩小关系图，直到屏幕可容纳整个关系图。  
  
 **树**  
 从下拉列表中选择一个树以在查看器中显示  
  
 如果时序模型包含多个系列，每个系列将表示为一个单独的树。 例如，如果您在一段时间内为 [Quantity] 和 [Sales Amount] 创建预测，则将为每个可预测属性创建一个单独的系列。  
  
 列表中突出显示的颜色的长度指示树中的级别数。 也就是说，可由单个节点表示的时序模型将包含一个用于描述走向的公式，并且彩色条会很短。 （当然，如果该模型是一个 MIXED 模型，则节点将同时包含 ARIMA 和 ARTXP 公式。）  
  
 如果下拉列表中显示的树包含一个较长的彩色条，则意味着该模型在树中有多个分支。 分支意味着回归会更加复杂且必须将模型分为多个段，每个节点中均有一个不同的公式（或公式对）。  
  
 **背景**  
 使用此控件可选择每个节点中背景色所表示的状态。  
  
 **默认扩展**  
 调整模型中所有树的默认显示级别数。  
  
 **显示级别**  
 更改树中显示的级别数。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法 &#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器（数据挖掘模型设计器）](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
