---
title: "使用 Microsoft 树查看器浏览模型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "树查看器 [Analysis Services]"
  - "预测 [Analysis Services], 离散属性"
  - "挖掘模型内容, 查看"
  - "预测 [Analysis Services], 连续属性"
  - "挖掘图例 [Analysis Services]"
  - "离散属性 [Analysis Services]"
  - "Microsoft 决策树算法 [Analysis Services]"
  - "决策树算法 [Analysis Services]"
  - "Microsoft 树查看器"
  - "决策树 [Analysis Services]"
  - "依赖关系 [Analysis Services]"
  - "连续属性"
ms.assetid: 0c96d518-ed20-40b7-8d62-b26ad6244287
caps.latest.revision: 46
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 46
---
# 使用 Microsoft 树查看器浏览模型
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 树查看器显示借助于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法生成的决策树。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法是一种既支持分类又支持回归的混合决策树算法。 因此，你可以使用该查看器来查看基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法的模型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法用于为离散属性和连续属性进行预测性建模。 有关此算法的详细信息，请参阅 [Microsoft Decision Trees Algorithm](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)。  
  
> [!NOTE]  
>  若要查看有关模型中使用的公式以及所发现的模式的详细信息，请使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般内容树查看器。 有关详细信息，请参阅[使用 Microsoft 一般内容树查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般内容树查看器（数据挖掘）](../Topic/Microsoft%20Generic%20Content%20Tree%20Viewer%20\(Data%20Mining\).md)。  
  
##  <a name="BKMK_TabsPanes"></a> 查看器的选项卡  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中浏览挖掘模型时，该模型会显示在其相应查看器的数据挖掘设计器的 **“挖掘模型查看器”** 选项卡上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 树查看器包括以下选项卡和窗格：  
  
-   [决策树](#BKMK_DecisionTree)  
  
-   [依赖关系网络](#BKMK_DependencyNetwork)  
  
-   [挖掘图例](#BKMK_MiningLegend)  
  
###  <a name="BKMK_DecisionTree"></a> 决策树  
 生成决策树模型时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将为每个可预测属性生成一个单独的树。 从查看器的 **“决策树”** 选项卡上的 **“树”** 列表中选择单个树，可查看该树。  
  
 决策树由一系列拆分组成，最重要的拆分由算法确定，该拆分位于 **“全部”** 节点中查看器的左侧。 其他拆分出现在右侧。 “全部”节点中的拆分最为重要，由于该节点包含了数据集内引起拆分的最充分的条件，因而产生了第一个拆分。  
  
 您可以展开或折叠决策树中的各个节点，以显示或隐藏各节点后出现的拆分。 您还可以使用 **“决策树”** 选项卡上的选项来设置树的显示方式。 使用 **“显示级别”** 滑块，可以调整树中显示的级别数。 使用 **“默认扩展”** 可以设置模型中所有树的默认显示级别数。  
  
#### 预测离散属性  
 如果树是使用离散可预测属性生成的，则查看器将在树的每个节点上显示以下信息：  
  
-   导致拆分的条件。  
  
-   表示可预测属性的状态分布情况的直方图，其中各个状态按使用频率高低进行排列。  
  
 可以使用 **“直方图”** 选项来更改在树的直方图中显示的状态数。 如果可预测属性有很多状态，这一功能将非常有用。 各种状态按使用频率高低自左到右显示在直方图中；如果选择显示的状态数少于属性的状态总数，则使用频率最低的状态将集中以灰色显示。 若要查看某个节点的各种状态的确切数目，可以将指针停留在该节点上来查看 InfoTip（信息提示），也可以选择该节点以便在 **“挖掘图例”**中查看其详细信息。  
  
 如果使用 **“后台”** 选项选择了特定属性状态，则各个节点的背景色将表示处于所选状态的事例的密集程度。 可以使用此选项来突出显示包含所关注的特定目标的节点。  
  
#### 预测连续属性  
 如果树是使用连续可预测属性生成的，则查看器为树中的每个节点显示一个菱形图，而不是直方图。 菱形图有一个表示属性范围的线条。 菱形位于节点的中间，其宽度表示该节点处属性的方差。 菱形越窄，说明该节点生成的预测更为精确。 查看器还显示用于确定节点中的拆分的回归公式。  
  
#### 其他决策树显示选项  
 为决策树模型启用钻取后，即可访问支持某个节点的定型事例，方法是：右键单击树中的该节点，然后选择“钻取”。 可以在数据挖掘向导内启用钻取，也可以在 **“挖掘模型”** 选项卡中通过调整挖掘模型的钻取属性来启用钻取。  
  
 可以使用 **“决策树”** 选项卡上的缩放选项来放大或缩小某个树，也可以使用 **“调整为合适大小”** 将整个模型放入查看器的屏幕中。 如果某个树太大而无法将其调整为适合屏幕的大小，则可使用“导航” 选项在树中导航。 单击 **“导航”** 将打开一个单独的导航窗口，可通过它来选择要显示的模型部分。  
  
 您还可以将树视图图像复制到剪贴板上，以便可将其粘贴到文档或图像处理软件中。 可以使用 **“复制图形视图”** 仅复制查看器中树的可见部分，也可以使用 **“复制整个图形”** 来复制树中所有扩展节点。  
  
 [返回页首](#BKMK_TabsPanes)  
  
###  <a name="BKMK_DependencyNetwork"></a> 依赖关系网络  
 **“依赖关系网络”** 显示了模型中的输入属性和可预测属性之间的依赖关系。 查看器左侧的滑块可起到与依赖关系强度相联系的筛选器的作用。 如果向下拉动滑块，则查看器中只会显示最强链接。  
  
 选择一个节点后，查看器将突出显示该节点特定的依赖项。 例如，如果选择一个可预测节点，查看器也将突出显示有助于预测该可预测节点的各个节点。  
  
 如果查看器包含大量的节点，则可使用 **“查找节点”** 按钮来搜索特定的节点。 单击 **“查找节点”** 将打开 **“查找节点”** 对话框，可以在该对话框中使用筛选器来搜索和选择特定的节点。  
  
 查看器底部的图例说明了图表中不同颜色代码所代表的依赖关系类型。 例如，如果选择一个可预测节点，该节点将呈青绿色，而预测所选节点的节点呈橙色。  
  
 [返回页首](#BKMK_TabsPanes)  
  
###  <a name="BKMK_MiningLegend"></a> 挖掘图例  
 在选中决策树模型中的某个节点时， **“挖掘图例”** 显示下列信息：  
  
-   节点中按可预测属性的状态划分的事例的数目。  
  
-   节点的可预测属性的各种事例的概率。  
  
-   一个直方图，其中包含可预测属性的各种状态的数目。  
  
-   访问某个特定节点所需的条件，也称为“节点路径 ”。  
  
-   回归公式（对于线性回归模型）  
  
 停靠和使用 **“挖掘图例”** 的方式与解决方案资源管理器的使用方式类似。  
  
 [返回页首](#BKMK_TabsPanes)  
  
## 另请参阅  
 [Microsoft 决策树算法](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)   
 [挖掘模型查看器（数据挖掘模型设计器）](../Topic/Mining%20Model%20Viewers%20\(Data%20Mining%20Model%20Designer\).md)   
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [数据挖掘工具](../../analysis-services/data-mining/data-mining-tools.md)   
 [数据挖掘模型查看器](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  