---
title: 浏览市场篮模型 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: da1c9cb7-6c32-4b9b-96ec-ecea772aeb77
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8a7b2f97cbda0594698c6cbaa68019a6493f1e74
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224610"
---
# <a name="exploring-the-market-basket-models-intermediate-data-mining-tutorial"></a>浏览市场篮模型（数据挖掘中级教程）
  现在，您构建`Association`模型中，您可以浏览该模型使用[!INCLUDE[msCoName](../includes/msconame-md.md)]中的关联查看器**挖掘模型查看器**数据挖掘设计器选项卡。 本教程指导您使用查看器来浏览各项之间的关系。 查看器可以帮助您快速查看哪些产品通常会一起出现，并且大致了解出现的模式。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]关联查看器包含三个选项卡：**规则**，**项集**，和**依赖关系网络**。 由于每个选项卡显示的数据视图略有差异，因此在浏览某个模型时，您通常会在不同窗格之间多次来回切换，以便深入了解数据。  
  
-   [依赖关系网络选项卡](#bkmk_DepNet)  
  
-   [项集选项卡](#bkmk_Itemsets)  
  
-   [规则选项卡](#bkmk_Rules)  
  
-   [泛型的内容视图](#bkmk_ContentViewer)  
  
 对于本教程，您将开始在**依赖关系网络**选项卡，然后使用**规则**选项卡并**项集**选项卡以加深您的理解的关系在查看器中显示。 你还将使用**Microsoft 一般内容树查看器**来检索各个规则或项集的详细统计信息。  
  
##  <a name="bkmk_DepNet"></a> 依赖关系网络选项卡  
 与**依赖关系网络**选项卡上，你可以调查的模型中不同的项交互。 查看器中的每个节点代表一个项，而节点之间的线条则代表规则。 通过选择节点，可以查看哪些其他节点预测选定项，还可以查看当前项预测哪些项。 在某些情况下，项之间存在双向关联，这意味着它们可以出现在同一事务中。 您可以参考选项卡底部的颜色图例来确定关联的方向。  
  
 连接两个项的线条意味着这些项很可能共同出现在同一事务中。 也就是说，客户很可能一起购买这些物品。 滑块与规则的概率关联。 上下移动滑块可以筛选出弱关联，弱关联意味着这些规则的概率很低。  
  
 依赖关系网络图显示了成对规则，可以从逻辑上表示，为 A-> B，这意味着如果购买产品 A，则可能是产品 B。 此图不能显示类型 AB 的规则，-> c。 如果您移动滑块来显示所有规则，但仍未在图中看到任何线条，则意味着没有成对规则满足算法参数的条件。  
  
 还可以通过键入属性名称的前几个字母，按名称查找节点。 有关详细信息，请参阅[“查找节点”对话框（挖掘模型查看器）](../../2014/analysis-services/find-node-dialog-box-mining-model-viewer.md)。  
  
#### <a name="to-open-the-association-mode-in-the-microsoft-assocaition-rules-viewer"></a>在 Microsoft 关联规则查看器中打开关联模式  
  
1.  在中**解决方案资源管理器**，双击关联结构。  
  
2.  在数据挖掘设计器中，单击 **“挖掘模型查看器”** 选项卡。  
  
3.  从列表中的挖掘模型中选择关联**挖掘模型**下拉列表中。  
  
#### <a name="to-navigate-the-dependency-graph-and-locate-specific-nodes"></a>导航依赖关系图和查找特定节点  
  
1.  在中**挖掘模型查看器**选项卡上，单击**依赖关系网络**选项卡。  
  
2.  单击**放大**几次，直至你可以轻松地查看每个节点的标签。  
  
     默认情况下，该图会以所有节点都可见这种形式显示。 复杂模型中可能有很多节点，使得每个节点都显得很小。  
  
3.  单击**+** 登录查看器的右下角并按下鼠标按钮，在关系图上平移。  
  
4.  在查看器的左侧，拖动下，将其从移动滑块**的所有链接**（默认值） 到滑块控件的底部。  
  
5.  查看器更新该图，只显示最强的关联，也就是 Touring Tire 和 Touring Tire Tube 项之间的关联。  
  
6.  单击标记为节点**Touring Tire Tube = Existing**。  
  
     该图进行更新，只突出显示与此项紧密相关的项。 请注意两个项之间箭头的方向。  
  
7.  在查看器的左侧，重新向上拖动滑块，将其从底部移至大约中间位置。  
  
     请注意连接两个项的箭头的变化。  
  
8.  选择**仅显示属性名称**从下拉列表顶部的依赖关系网络窗格。  
  
     图中的文本标签会更新为仅显示模型名称。  
  
 [返回页首](#bkmk_DepNet)  
  
##  <a name="bkmk_Itemsets"></a> 项集选项卡  
 接下来，您将更加详细地了解 Touring Tire 和 Touring Tire Tube 产品的模型所生成的规则和项集。 **项集**选项卡显示三个重要的信息片段的项集相关的[!INCLUDE[msCoName](../includes/msconame-md.md)]关联算法发现：  
  
-   **支持：** 在其中出现项集的事务数。  
  
-   **大小：** 集中的项的项的数目。  
  
-   **项：** 每个项集中包含的项的列表。  
  
 根据算法参数的设置方式，算法可能生成多个项集。 查看器中返回的每个项集都代表销售该项的事务。 在顶部使用的控件**项集**选项卡上，您可以筛选查看器显示包含指定的最小支持度和项集大小的项集。  
  
 如果您使用不同的挖掘模型，并且没有列出项集，则原因在于没有项集满足算法参数的条件。 在这种情况下，可以更改算法参数，以允许具有较低支持的项集。  
  
#### <a name="to-filter-the-itemsets-that-are-shown-in-the-viewer-by-name"></a>按名称筛选在查看器中显示的项集  
  
1.  单击**项集**查看器的选项卡。  
  
2.  在中**筛选项集**框中，键入`Touring Tire`，然后在框外部单击。  
  
     筛选器返回所有包含此字符串的项。  
  
3.  在中**显示**列表中，选择**仅显示属性名称**。  
  
4.  选择**显示长名称**复选框。  
  
     项集列表会更新为仅显示包含字符串“Touring Tire”的项集。 项集的长名称包括了表的名称，表名称包含每个项的属性和值。  
  
5.  清除**显示长名称**复选框。  
  
     项集的列表会更新为仅显示短名称。  
  
 中的值**支持**列指示每个项集的事务数。 项集的事务表示该购买包括项集中的所有项。  
  
 默认情况下，查看器按支持的降序列出项集。 可以单击列标题，按不同列（例如项集大小或名称）进行排序。 如果您有兴趣了解关于包括在项集中的各个事务的更多信息，可以从项集钻取到各个事例。 钻取结果中的结构列是客户的收入水平和客户 ID，这些信息未在模型中使用。  
  
#### <a name="to-view-details-for-an-itemset"></a>查看项集的详细信息  
  
1.  在项集列表中，单击**项集**列标题按名称进行排序。  
  
2.  找到的项， `Touring Tire` （与没有第二项）。  
  
3.  右键单击该项， `Touring Tire`，选择**钻取**，然后选择**模型和结构列**。  
  
     **钻取**对话框显示用作此项集支持的各个事务。  
  
4.  展开嵌套表 vAssocSeqLineItems 可以查看事务中的实际购买列表。  
  
#### <a name="to-filter-itemsets-by-support-or-size"></a>按支持或大小筛选项集  
  
1.  清除可能在任何文本**筛选项集**框。 不能将文本筛选器和数值筛选器一起使用。  
  
2.  在中**最低支持**框中，键入 100，，然后单击查看器的背景。  
  
     项集的列表会更新为仅显示支持最低达到 100 的项集。  
  
 [返回页首](#bkmk_DepNet)  
  
##  <a name="bkmk_Rules"></a> 规则选项卡  
 **规则**选项卡显示与算法发现的规则相关的以下信息。  
  
-   **概率：***可能性*的规则，定义为给定左侧项的右侧项的概率。  
  
-   **重要性：** 规则的有用性的度量值。 值越大则意味着规则越有用。  
  
     重要性用于度量规则的有用性，因为只使用概率可能会发生误导。 例如，如果每个事务都包含一个水壶（也许水壶是作为促销活动的一部分自动添加到每位客户的购物车中），该模型会创建一条规则，预测水壶的概率为 1。 仅依据概率来看，此规则非常准确，但它并未提供有用的信息。  
  
-   **规则：** 规则的定义。 对于市场篮模型，规则描述特定的项组合。  
  
 每条规则都可以根据事务中其他项的发生情况来预测某个项的发生情况。 类似**项集**选项卡上，您可以筛选规则，以便显示最关心的规则。 如果您使用的挖掘模型没有任何规则，您可能希望更改算法参数，以降低规则的概率阈值。  
  
#### <a name="to-see-only-rules-that-include-the-mountain-200-bicycle"></a>仅查看包括 Mountain-200 自行车的规则  
  
1.  在中**挖掘模型查看器**选项卡上，单击**规则**选项卡。  
  
2.  在中**筛选器规则**框中，输入`Mountain-200`。  
  
     清除**显示长名称**复选框。  
  
3.  从**显示**列表中，选择**仅显示属性名称**。  
  
     在查看器然后显示规则包含单词"`Mountain-200`"。 规则的概率告诉您如何可能它是，当有人购买了`Mountain-200`自行车，此人也会购买其他所列的产品。  
  
 这些规则按照概率降序排序，但您可以单击栏标题来更改排序顺序。 如果您有兴趣查找关于某个特定规则的更多详细信息，可以使用钻取功能来查看支持事例。  
  
#### <a name="to-view-cases-that-support-a-particular-rule"></a>查看支持特定规则的事例  
  
1.  在中**规则**选项卡上，右键单击你想要查看的规则。  
  
2.  选择**钻取**，然后选择**仅限模型列**，或**模型和结构列**。  
  
     **钻取**对话框中提供了在窗格的顶部和用作支持数据的规则的所有事例的列表的规则的摘要。  
  
 [返回页首](#bkmk_DepNet)  
  
##  <a name="bkmk_ContentViewer"></a> 一般内容树查看器  
 此查看器可用于所有模型，无论算法和模型类型为何均为如此。 **Microsoft 一般内容树查看器**可从**查看器**下拉列表。  
  
 内容树是挖掘模型的表示形式，由一系列节点组成，其中每个节点都表示与数据的某一子集相关的已发现的知识。 节点可以包含一种模式、一组规则、一个群集或共享某些特性的日期范围的定义。 根据算法和可预测属性的类型的不同，节点的具体内容也会不同，但内容的通用表示形式是相同的。 您可以展开每个节点以查看详细信息的递增级别，并可以将任何节点的内容复制到剪贴板。  
  
#### <a name="to-view-details-about-the-rule-by-using-the-content-viewer"></a>使用内容查看器查看关于规则的详细信息  
  
1.  在中**挖掘模型查看器**选项卡上，选择**Microsoft 一般内容树查看器**从**查看器**列表。  
  
2.  在“节点标题”窗格中，滚动到列表的底部，然后单击最后一个节点。  
  
     查看器首先显示项集，接下来显示规则，但不对它们进行分组。 查找特定节点的最简单方法是创建内容查询。 有关详细信息，请参阅 [关联模型查询示例](../../2014/analysis-services/data-mining/association-model-query-examples.md)  
  
3.  在“节点详细信息”窗格中，查看 NODE_TYPE 和 NODE_DESCRIPTION 的值。  
  
     节点类型 8 是规则，节点类型 7 是项集。 对于规则来说，NODE_DESCRIPTION 的值指示了构成规则的条件。 对于项集来说，NODE_DESCRIPTION 的值指示了包括在项集中的项。  
  
 您还可以创建内容查询，以获取关于规则的详细统计信息。 有关挖掘模型内容以及如何解释它的详细信息，请参阅[关联模型的挖掘模型内容&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)。  
  
 [返回页首](#bkmk_DepNet)  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [筛选挖掘模型中的嵌套的表&#40;数据挖掘中级教程&#41;](../../2014/tutorials/filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [第 3 课：生成市场篮方案&#40;数据挖掘中级教程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)   
 [第 4 课：生成顺序聚类分析方案&#40;数据挖掘中级教程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)   
 [Microsoft 关联算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Microsoft 关联算法技术参考](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)  
  
  
