---
title: 浏览聚类分析模型 （数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e56d1dc66e8e6ac73a3ae8b1888cbdee16c63df
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146737"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>浏览聚类分析模型（数据挖掘基础教程）
  [!INCLUDE[msCoName](../includes/msconame-md.md)]聚类分析算法事例分组为包含类似特征的分类。 在浏览数据、标识数据中的异常及创建预测时，这些分组十分有用。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 分类查看器提供了以下选项卡，用于浏览聚类分析挖掘模型：  
  

  
##  <a name="ClusterDiagramTab"></a> 群集关系图选项卡  
 “分类关系图”选项卡显示挖掘模型中的所有分类。 分类之间的线条表示“接近程度”，其明暗度取决于分类之间的相似程度。 每个分类的实际颜色表示分类中变量和状态的出现频率。  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>在“分类关系图”选项卡中浏览模型  
  
1.  使用**挖掘模型**顶部的列表**挖掘模型查看器**选项卡以切换到`TM_Clustering`模型。  
  
2.  在中**查看器**列表中，选择**Microsoft 分类查看器**。  
  
3.  在中**明暗度变量**框中，选择**Bike Buyer**。  
  
     默认变量是**填充**，但你可以更改为在模型中，若要发现哪些群集包含成员具有所需的属性的任何属性。  
  
4.  选择**1**中**状态**框可以浏览那些购买自行车的事例。  
  
     **密度**图例描述了在明暗度变量和状态中选择的属性状态对的密度。 在此示例中它告诉我们 clusterwith 最暗的自行车购买者百分比最高。  
  
5.  将鼠标悬停在明暗度最深的分类上。  
  
     工具提示将显示具有 `Bike Buyer = 1` 属性的事例所占的百分比。  
  
6.  选择密度最高，右键单击该分类中，选择的群集**重命名分类**并键入**Bike Buyers High**以用作日后标识。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  查找明暗度最浅（也就是密度最低）的分类。 右键单击该分类中，选择**重命名分类**并键入**Bike Buyers Low**。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  单击**Bike Buyers High**群集并将其拖到，使其与其他分类的连接的清晰视图窗格中某个区域。  
  
     选择某个分类时，将此分类连接到其他分类的线条将突出显示，以便您方便地查看此分类的所有关系。 如果该分类处于未选定状态，则可以通过线条的暗度来确定关系图中所有分类之间关系的紧密程度。 如果明暗度较浅或无明暗度，则表示分类的相似程度较低。  
  
9. 使用网络左侧的滑块，可筛选掉强度较低的链接，找出关系最接近的分类。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 市场部可能希望将相似的分类组合在一起，以便确定提供目标邮件的最佳方法。  
  

  
##  <a name="ClusterProfilesTab"></a> 群集配置文件选项卡  
 **分类剖面图**选项卡提供的总体视图`TM_Clustering`模型。 **分类剖面图**选项卡包含模型中的每个分类的列。 第一列列出至少与一个分类关联的属性。 查看器的其余部分包含每个分类的某个属性的状态分布。 离散变量的分布显示为最大数目的条形图中显示一个彩色条**直方图条数**列表。 连续属性以菱形图显示，表示每个分类中的平均偏差和标准偏差。  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>在“分类剖面图”选项卡中浏览模型  
  
1.  设置**直方图**到条**5**。  
  
     在我们的模型中，任意一个变量的最大状态数均为 5。  
  
2.  如果**挖掘图例**阻止显示**属性配置文件**，将其移开。  
  
3.  选择**Bike Buyers High**列并将其拖到右侧**填充**列。  
  
4.  选择**Bike Buyers Low**列并将其拖到右侧**Bike Buyers High**列。  
  
5.  单击**Bike Buyers High**列。  
  
     **变量**列排序顺序对该群集的重要性。 滚动浏览该列，查看 Bike Buyer High 分类的特征。 例如，他们上下班路程较短的可能性较大。  
  
6.  双击**年龄**中的单元格**Bike Buyers High**列。  
  
     **挖掘图例**显示更详细视图，您可以看到这些客户，以及平均年龄的年龄范围。  
  
7.  右键单击**Bike Buyers Low**列并选择**隐藏列**。  
  

  
##  <a name="ClusterCharacteristicsTab"></a> 群集特征选项卡  
 与**分类特征**选项卡上，您可以更加详细地检查组成分类的特征。 您可以一次浏览一个分类，而不是比较所有分类的特征（就像在“分类剖面图”选项卡中那样）。 例如，如果您选择**Bike Buyers High**从**群集**列表中，您可以看到此分类中的客户的特征。 尽管显示方式与分类剖面图查看器不同，但查找结果却是相同的。  
  
> [!NOTE]  
>  除非设置为初始值，否则**holdoutseed**，每次处理模型时，结果会有所不同。 有关详细信息，请参阅[HoldoutSeed 元素](https://docs.microsoft.com/bi-reference/assl/properties/holdoutseed-element)  
  

  
##  <a name="ClusterDiscriminationTab"></a> 群集对比选项卡  
 与**分类对比**选项卡上，你可以浏览区分分类的特征。 选择两个群集，一个来自后**分类 1**列表中，一个来自**分类 2**列表中，在查看器计算群集之间的差异，并显示属性的列表，各分类最。  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>在“分类对比”选项卡中浏览模型  
  
1.  在中**分类 1**框中，选择**Bike Buyers High**。  
  
2.  在中**分类 2**框中，选择**Bike Buyers Low**。  
  
3.  单击**变量**以字母顺序排序。  
  
     一些中的客户之间更显著的差异**Bike Buyers Low**并**Bike Buyers High**群集包括年龄、 汽车拥有情况、 子女数和区域。  
  
## <a name="related-tasks"></a>Related Tasks  
 请参阅以下主题以了解其他挖掘模型。  
  
-   [浏览决策树模型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [浏览 Naive Bayes 模型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [浏览 Naive Bayes 模型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [浏览决策树模型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用 Microsoft 分类查看器浏览模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [群集对比选项卡&#40;挖掘模型查看器&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [群集配置文件选项卡&#40;挖掘模型查看器&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [群集特征选项卡&#40;挖掘模型查看器&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [群集关系图选项卡&#40;挖掘模型查看器&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
