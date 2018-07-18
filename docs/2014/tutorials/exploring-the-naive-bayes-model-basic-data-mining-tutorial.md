---
title: 浏览 Naive Bayes 模型 （数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b06708d5-4477-4a51-bf8d-0b1e3c1f9ebb
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 172c4eb4cd0ad134298ffce813113036b79baefd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200707"
---
# <a name="exploring-the-naive-bayes-model-basic-data-mining-tutorial"></a>浏览 Naive Bayes 模型（数据挖掘基础教程）
  [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 算法提供了多种方法来显示自行车的购买和输入的属性之间的交互。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 查看器提供了以下选项卡中浏览 Naive Bayes 挖掘模型使用：  
  
 
  
##  <a name="DependencyNetwork"></a> 依赖关系网络  
 **依赖关系网络**选项卡上的工作方式与同一**依赖关系网络**选项卡上的[!INCLUDE[msCoName](../includes/msconame-md.md)]树查看器。 查看器中的每个节点代表一个属性，而节点之间的线条代表关系。 在查看器中，您可以查看影响可预测属性 Bike Buyer 的状态的所有属性。  
  
#### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>在“依赖关系网络”选项卡中浏览模型  
  
1.  使用**挖掘模型**顶部的列表**挖掘模型查看器**选项卡以切换到`TM_NaiveBayes`模型。  
  
2.  使用**查看器**要切换到列表**Microsoft Naive Bayes 查看器**。  
  
3.  单击`Bike Buyer`节点以确定其依赖项。  
  
     粉色阴影指示所有属性都会对自行车购买行为产生影响。  
  
4.  调整滑块可标识影响最大的属性。  
  
     向下滑动滑块时，将只保留对 [Bike Buyer] 列影响最大的属性。 通过调整滑块，可以发现影响最大的几个属性为：拥有汽车的数量、通勤距离以及子女总数。  
 
  
##  <a name="AttributeProfiles"></a> 属性配置文件  
 **属性配置文件**选项卡说明输入的属性会影响可预测属性的结果的不同状态如何。  
  
#### <a name="to-explore-the-model-in-the-attribute-profiles-tab"></a>在“属性配置文件”选项卡中浏览模型  
  
1.  在中**可预测**框中，验证`Bike Buyer`处于选中状态。  
  
2.  如果**挖掘图例**阻止显示**属性配置文件**，将其移开。  
  
3.  在中**直方图**条框中，选择**5**。  
  
     在我们的模型中，任意一个变量的最大状态数均为 5。  
  
     系统会列出影响该可预测属性的状态的属性以及输入属性的每个状态的值及其在该可预测属性的每个状态中的分布。  
  
4.  在中**特性**列中，找到**Number Cars Owned**。  请注意，自行车购买者（标为 1 的列）与非自行车购买者（标为 0 的列）的直方图的差异。 如果一个人拥有的汽车数量为 0 或 1，则此人很有可能会购买自行车。  
  
5.  双击**Number Cars Owned**自行车购买者中的单元格 （标为 1 的列） 列。  
  
     **挖掘图例**显示更详细的视图。  
  
  
##  <a name="AttributeCharacteristics"></a> 属性特征  
 与**属性特征**选项卡上，可以选择属性和值，若要查看其他属性值的所选的值事例中的出现频率。  
  
#### <a name="to-explore-the-model-in-the-attribute-characteristics-tab"></a>在“属性特征”选项卡中浏览模型  
  
1.  在中**特性**列表中，验证`Bike Buyer`处于选中状态。  
  
2.  设置**值**到**1**。  
  
     在查看器中，您将看到，家中无子女、通勤距离较近和居住在北美洲地区的客户更有可能购买自行车。  
  
  
##  <a name="AttributeDiscrimination"></a> 属性对比  
 与**属性对比**选项卡上，你可以调查自行车购买行为的两个离散值和其他属性值之间的关系。 因为`TM_NaiveBayes`模型有只有两个状态，1 和 0，无需对查看器进行任何更改。  
  
 在查看器中，您会看到，没有汽车的人一般会购买自行车，而有两辆汽车的人一般不会购买自行车。  
  
## <a name="related-tasks"></a>Related Tasks  
 请参阅以下主题以了解其他挖掘模型。  
  
-   [浏览决策树模型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [浏览聚类分析模型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一课  
 [第 5 课： 测试模型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [浏览聚类分析模型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [使用 Microsoft Naive Bayes 查看器浏览模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)   
 [属性对比选项卡&#40;挖掘模型查看器&#41;](../../2014/analysis-services/attribute-discrimination-tab-mining-model-viewer.md)   
 [属性配置文件选项卡&#40;挖掘模型查看器&#41;](../../2014/analysis-services/attribute-profiles-tab-mining-model-viewer.md)   
 [属性特征选项卡&#40;挖掘模型查看器&#41;](../../2014/analysis-services/attribute-characteristics-tab-mining-model-viewer.md)   
 [依赖关系网络选项卡&#40;挖掘模型查看器&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)  
  
  
