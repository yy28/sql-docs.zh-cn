---
title: 浏览决策树模型（数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2e1472c2-3f3e-4dae-acb3-62fca374d397
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e7b77b445ff8cbef8be3acb72ef9cdb6fa3af159
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63224600"
---
# <a name="exploring-the-decision-tree-model-basic-data-mining-tutorial"></a>浏览决策树模型（数据挖掘基础教程）
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 决策树算法预测哪些列影响基于定型集中的其余列做出的自行车购买决策。  
  

  
##  <a name="decision-tree-tab"></a><a name="Decision_Tree_Tab"></a>决策树选项卡  
 在 "**决策树**" 选项卡上，可以查看数据集中每个可预测属性的决策树。  
  
 在这种情况下，模型只预测一列（自行车购买者），因此只有一个要查看的树。 如果有更多的树，可以使用**树**框选择另一个树。  
  
 在决策树查看`TM_Decision_Tree`器中查看模型时，可以在图表左侧看到最重要的属性。 "最重要" 意味着这些属性对结果的影响最大。 沿着该树越向下走的属性（图表右侧）的影响越小。  
  
 在此示例中，在预测自行车购买行为时，年龄是最重要的因素。 模型按年龄对客户进行分组，然后显示每个年龄组的下一个较重要的属性。 例如，在年龄为 34 到 40 的客户组中，拥有的汽车数是仅次于年龄的预测因子。  
  
#### <a name="to-explore-the-model-in-the-decision-tree-tab"></a>在“决策树”选项卡中浏览模型  
  
1.  在**数据挖掘设计器**中选择 "**挖掘模型查看器**" 选项卡。  
  
     默认情况下，设计器将打开添加到结构中的第一个模型， `TM_Decision_Tree`在本例中为。  
  
2.  使用放大镜按钮调整树的显示大小。  
  
     默认情况下，[!INCLUDE[msCoName](../includes/msconame-md.md)] 树查看器仅显示树的前三个级别。 如果树级别不到三个，则查看器仅显示现有级别。 您可以使用 "**显示级别**" 滑块或**默认扩展**列表查看更多级别。  
  
3.  向第四栏滑动**显示级别**。  
  
4.  将 "**背景**" 值`1`更改为。  
  
     通过更改 "**背景**" 设置，可以快速查看每个节点中的事例数，其目标值`1`为 [自行车购买者]。 请注意，在这种特定的情况下，每个事例均表示一个客户。 该值`1`表示客户以前购买了自行车;值**0**指示客户未购买自行车。 节点的底纹颜色越深，节点中具有目标值的事例所占的百分比越大。  
  
5.  将光标置于标记为 "**全部**" 的节点上。 将出现显示以下信息的工具提示：  
  
    -   事例总数  
  
    -   非自行车购买者事例的数量  
  
    -   自行车购买者事例的数量  
  
    -   缺少 [Bike Buyer] 值的事例的数量  
  
     或者，将光标放在树中的任何节点上，查看从上级节点到达该节点所需的条件。 您还可以在 "**挖掘图例**" 中查看相同的信息。  
  
6.  单击 " **Age >= 34" 节点，然后单击 "< 41**"。 直方图将显示为一个穿过该节点的窄水平条，并表示此年龄范围中以前买过自行车的客户（粉色）和没有买过自行车的客户（蓝色）的分布情况。 查看器显示：没有汽车或者有一辆汽车、年龄在 34 到 40 的客户有可能购买自行车。 再进一步考察发现，实际年龄在 38 到 40 的客户购买自行车的可能性会增加。  
  
 由于您在创建结构和模型时启用了钻取，因此，可以从模型事例和挖掘结构中检索详细的信息，其中包括挖掘模型中所不包含的列（例如，emailAddress 和 FirstName）。  
  
 有关详细信息，请参阅 [钻取查询（数据挖掘）](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
#### <a name="to-drill-through-to-case-data"></a>钻取到事例数据  
  
1.  右键单击某个节点，然后选择 "**钻取**"，然后选择 "**仅限模型列**"。  
  
     每个定型事例的详细信息将以电子表格方式显示。 这些详细信息来自您在生成挖掘结构时选作事例表的 vTargetMail 视图。  
  
2.  右键单击某个节点，然后选择 "**钻取**"，然后选择 "**模型和结构列**"。  
  
     将显示同一个电子表格，并在末尾处附加结构列。  
  
  
###  <a name="dependency-network-tab"></a><a name="Dependency_Network_Tab"></a>依赖关系网络选项卡  
 "**依赖关系网络**" 选项卡显示构成挖掘模型预测能力的属性之间的关系。 依赖关系网络查看器进一步证实了我们的发现：年龄和地区是预测自行车购买行为的重要因素。  
  
##### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>在“依赖关系网络”选项卡中浏览模型  
  
1.  单击`Bike Buyer`节点以标识其依赖项。  
  
     依赖关系网络`Bike Buyer`的中心节点表示挖掘模型中的可预测属性。 该图形突出显示了影响可预测的属性的任何已连接节点。  
  
2.  调整 "**所有链接**" 滑块以确定最具影响力的特性。  
  
     向下拖动滑块时，将从关系图中删除只对 [自行车买家] 列产生弱影响的属性。 通过调整滑块，可以发现“年龄”和“地区”是预测个人自行车购买行为的最主要因素。  
  
## <a name="related-tasks"></a>Related Tasks  
 请参阅以下主题，了解如何使用其他模型类型来探索数据。  
  
-   [浏览聚类分析模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [浏览 Naive Bayes 模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [浏览聚类分析模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型查看器任务和操作指南](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [挖掘模型查看器 &#40;的决策树选项卡&#41;](../../2014/analysis-services/decision-tree-tab-mining-model-viewer.md)   
 [挖掘模型查看器 &#40;的 "依赖关系网络" 选项卡&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)   
 [使用 Microsoft 树查看器浏览模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
  
