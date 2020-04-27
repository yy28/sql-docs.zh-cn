---
title: 浏览聚类分析模型（数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9bb2c6457122a5ea49824ca178b6950d88f75563
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63280424"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>浏览聚类分析模型（数据挖掘基础教程）
  聚[!INCLUDE[msCoName](../includes/msconame-md.md)]类分析算法将事例分组为包含类似特征的分类。 在浏览数据、标识数据中的异常及创建预测时，这些分组十分有用。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 分类查看器提供了以下选项卡，用于浏览聚类分析挖掘模型：  
  

  
##  <a name="cluster-diagram-tab"></a><a name="ClusterDiagramTab"></a>分类关系图选项卡  
 “分类关系图”选项卡显示挖掘模型中的所有分类。 分类之间的线条表示“接近程度”，其明暗度取决于分类之间的相似程度。 每个分类的实际颜色表示分类中变量和状态的出现频率。  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>在“分类关系图”选项卡中浏览模型  
  
1.  可以使用 "**挖掘模型查看器**" 选项卡顶部的 "**挖掘模型**" 列表切换`TM_Clustering`到模型。  
  
2.  在**查看器**列表中，选择 " **Microsoft 分类查看器**"。  
  
3.  在 "**明暗度变量**" 框中，选择 "**自行车购买**者"。  
  
     默认变量是**填充**，但您可以将其更改为模型中的任何属性，以发现哪些分类包含具有所需属性的成员。  
  
4.  在 "**状态**" 框中选择**1**以浏览购买了自行车的情况。  
  
     **密度**图例描述了 "明暗度变量" 和 "状态" 中选定的属性状态对的密度。 在此示例中，它告诉我们，最暗的 clusterwith 是自行车购买者的最高百分比。  
  
5.  将鼠标悬停在明暗度最深的分类上。  
  
     工具提示将显示具有 `Bike Buyer = 1` 属性的事例所占的百分比。  
  
6.  选择密度最高的分类，右键单击该群集，选择 "**重命名群集**"，然后键入 "**自行车买家 High** "，以供以后标识。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  查找明暗度最浅（也就是密度最低）的分类。 右键单击该群集，选择 "**重命名群集**"，然后键入 "**自行车买家 Low**"。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  单击**自行车购买者高级**群集并将其拖到窗格中的某个区域，这会使你清楚地了解其与其他分类的连接。  
  
     选择某个分类时，将此分类连接到其他分类的线条将突出显示，以便您方便地查看此分类的所有关系。 如果该分类处于未选定状态，则可以通过线条的暗度来确定关系图中所有分类之间关系的紧密程度。 如果明暗度较浅或无明暗度，则表示分类的相似程度较低。  
  
9. 使用网络左侧的滑块，可筛选掉强度较低的链接，找出关系最接近的分类。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 市场部可能希望将相似的分类组合在一起，以便确定提供目标邮件的最佳方法。  
  

  
##  <a name="cluster-profiles-tab"></a><a name="ClusterProfilesTab"></a>群集配置文件选项卡  
 "**分类配置文件**" 选项卡提供了`TM_Clustering`模型的总体视图。 "**分类配置文件**" 选项卡包含模型中每个分类的列。 第一列列出至少与一个分类关联的属性。 查看器的其余部分包含每个分类的某个属性的状态分布。 离散变量的分布以彩色条显示，并显示在 "**直方图条**" 列表中显示的最大栏数。 连续属性以菱形图显示，表示每个分类中的平均偏差和标准偏差。  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>在“分类剖面图”选项卡中浏览模型  
  
1.  将**直方图**条设置为**5**。  
  
     在我们的模型中，任意一个变量的最大状态数均为 5。  
  
2.  如果 "**挖掘图例**" 阻止显示**属性配置文件**，请将其移开。  
  
3.  选择 "**自行车购买**者" 列并将其拖动到**填充**列的右侧。  
  
4.  选择 "**自行车买家 Low** " 列并将其拖动到 "**自行车购买**者" 列的右侧。  
  
5.  单击 "**自行车购买**者" 列。  
  
     **Variables**列按该分类的重要性顺序进行排序。 滚动浏览该列，查看 Bike Buyer High 分类的特征。 例如，他们上下班路程较短的可能性较大。  
  
6.  双击 "**自行车购买**者" 列中的**Age**单元格。  
  
     "**挖掘图例**" 显示更详细的视图，可以查看这些客户的年龄范围以及平均年龄。  
  
7.  右键单击 "**自行车买家 Low** " 列并选择 "**隐藏列**"。  
  

  
##  <a name="cluster-characteristics-tab"></a><a name="ClusterCharacteristicsTab"></a>分类特征选项卡  
 使用 "**分类特征**" 选项卡，可以更详细地查看组成群集的特征。 您可以一次浏览一个分类，而不是比较所有分类的特征（就像在“分类剖面图”选项卡中那样）。 例如，如果从**群集**列表中选择 "高" "**自行车购买**者"，则可以看到此群集中的客户的特征。 尽管显示方式与分类剖面图查看器不同，但查找结果却是相同的。  
  
> [!NOTE]  
>  除非为**holdoutseed**设置初始值，否则每次处理该模型时，结果将有所不同。 有关详细信息，请参阅[HoldoutSeed 元素](https://docs.microsoft.com/bi-reference/assl/properties/holdoutseed-element)  
  

  
##  <a name="cluster-discrimination-tab"></a><a name="ClusterDiscriminationTab"></a>分类对比选项卡  
 利用 "**分类对比**" 选项卡，可以浏览区分不同分类的特征。 从 "**分类 1** " 列表中选择两个群集，然后从 "**分类 2** " 列表中选择两个群集后，查看器将计算这些分类之间的差异，并显示最大程度地区分分类的属性列表。  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>在“分类对比”选项卡中浏览模型  
  
1.  在 "**分类 1** " 框中，选择 "**自行车买家 High**"。  
  
2.  在 "**分类 2** " 框中，选择 "**自行车买家 Low**"。  
  
3.  单击 "**变量**" 以按字母顺序排序。  
  
     **自行车买家低端**和**自行车购买者高**群集的客户之间的一些显著差异包括年龄、汽车所有权、子女数量和地区。  
  
## <a name="related-tasks"></a>Related Tasks  
 请参阅以下主题以了解其他挖掘模型。  
  
-   [浏览决策树模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [浏览 Naive Bayes 模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [浏览 Naive Bayes 模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [浏览决策树模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用 Microsoft 分类查看器浏览模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [&#40;挖掘模型查看器的 "分类对比" 选项卡&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [挖掘模型查看器 &#40;的 "分类配置文件" 选项卡&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [&#40;挖掘模型查看器的 "分类特征" 选项卡&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [&#40;挖掘模型查看器的 "分类关系图" 选项卡&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
