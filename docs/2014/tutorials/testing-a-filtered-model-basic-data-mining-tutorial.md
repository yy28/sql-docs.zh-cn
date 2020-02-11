---
title: 测试筛选的模型（数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f0d74f8c-600d-4df5-a742-695e6947a071
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: baa4910b2849c4eb2dd04c6d0115c83683ee8bea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63044062"
---
# <a name="testing-a-filtered-model-basic-data-mining-tutorial"></a>测试筛选后的模型（数据挖掘基础教程）
  现在您已确定该`TM_Decision_Tree`模型是最准确的模型，您将自定义该模型以更好地满足[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]目标邮件市场活动的需要。 具体来说，市场部希望了解男客户和女客户是否存在特征差异。 这些信息可帮助他们决定使用哪些杂志进行广告宣传，以及在邮件中推广哪些产品。  
  
## <a name="using-filters"></a>使用筛选器  
 通过筛选，您可以轻松地创建基于数据子集生成的模型。 筛选器只应用于该模型，而且不会更改基础数据源。  
  
 在本课中，您将创建一个针对性别进行了筛选的模型，以预测男性和女性中对自行车购买行为影响最大的特征。  
  
 首先，您将创建`TM_Decision_Tree`模型的副本。  
  
#### <a name="to-copy-the-decision-tree-model"></a>复制决策树模型  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中，选择 " **BasicDataMining**"。  
  
2.  单击 **“挖掘模型”** 选项卡。  
  
3.  右键单击该`TM_Decision_Tree`模型，然后选择 "**新建挖掘模型"。**  
  
4.  在 "**模型名称**" 字段中`TM_Decision_Tree_Male`，键入。  
  
5.  单击“确定”。   
  
 然后为模型创建一个筛选器，用于根据客户的性别选择客户。  
  
#### <a name="to-create-a-case-filter-on-a-mining-model"></a>创建挖掘模型的事例筛选器  
  
1.  右键单击`TM_Decision_Tree_Male`挖掘模型以打开快捷菜单。  
  
     \- 或 -  
  
     选择该模型。 在 **“挖掘模型”** 菜单上，选择 **“设置模型筛选器”**。  
  
2.  在 **“模型筛选器”** 对话框的 **“挖掘结构列”** 文本框中，单击网格中的第一行。  
  
     下拉列表只显示该表中列的名称。  
  
3.  在 "挖掘结构列" 文本框中，选择 "**性别**"。  
  
     文本框左侧的图标会发生改变，以指示所选项是表还是列。  
  
4.  单击 "**运算符**" 文本框，然后从列表中选择等于（=）运算符。  
  
5.  单击 "**值**" 文本框，然后键入**M**。  
  
6.  单击网格中的下一行。  
  
7.  单击 **"确定"** 以关闭 "**模型筛选器**" 对话框。  
  
     筛选器显示在 "**属性**" 窗口中。 或者，您可以从 "**属性**" 窗口启动 "**模型筛选器**" 对话框。  
  
8.  重复上述步骤，但这次在 "**值**" `TM_Decision_Tree_Female`文本框中命名模型和类型 " **F** "。  
  
## <a name="process-the-filtered-models"></a>处理筛选的模型  
 模型经过部署和处理后才能使用。 有关处理模型的详细信息，请参阅[&#40;基本数据挖掘教程&#41;中的处理目标邮件结构中的模型](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)。  
  
#### <a name="to-process-the-filtered-model"></a>处理筛选后的模型  
  
1.  右键单击该模型`TM_Decision_Tree_Male` ，然后选择 "**处理挖掘结构和所有模型**"  
  
2.  单击 "**运行**" 以处理新模型。  
  
3.  处理完成后，单击 "处理" 窗口中的 "**关闭**"。  
  
     你现在可以在 "**挖掘模型**" 选项卡中显示两个新模型。  
  
## <a name="evaluate-the-results"></a>评估结果  
 查看结果并评估筛选后的模型的准确性，与您对前三个模型的操作非常相似。 有关详细信息，请参阅：  
  
 [浏览决策树模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
 [利用提升图测试准确性 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
#### <a name="to-explore-the-filtered-models"></a>浏览筛选后的模型  
  
1.  在**数据挖掘设计器**中选择 "**挖掘模型查看器**" 选项卡。  
  
2.  在 "挖掘模型" 框中`TM_Decision_Tree_Male`，选择。  
  
3.  `3`将**显示级别**幻灯片。  
  
4.  将 "**背景**" 值`1`更改为。  
  
5.  将光标置于标记为 "**全部**" 的节点上，以查看自行车购买者和非自行车购买者的数量。  
  
6.  对`TM_Decision_Tree_Female`执行步骤 1-5。  
  
7.  浏览的`TM_Decision_Tree`结果和为性别筛选的模型。 与所有自行车购买者相比，男性和女性自行车购买者与未经筛选自行车购买者具有一些相同特征，但所有这三个群体也存在一些重要差异。 这是可用于开发[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]市场营销活动的有用信息。  
  
#### <a name="to-test-the-lift-of-the-filtered-models"></a>测试筛选后的模型的提升  
  
1.  切换到数据挖掘设计器中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的 "**挖掘准确性图表**" 选项卡，然后选择 "**输入选择**" 选项卡。  
  
2.  在 "**选择要用于准确性图表的数据集**" 组框中，选择 "**使用挖掘结构测试事例**"。  
  
3.  在数据挖掘设计器的 "**输入选择**" 选项卡上，在 "**选择要在提升图中显示的可预测的挖掘模型列**" 下，选中 "**同步预测列和值**" 复选框。  
  
4.  在 "**可预测列名称**" 列中，验证是否为每个模型选择了 "**自行车购买**者"。  
  
5.  在 "**显示**" 列中，选择每个模型。  
  
6.  在 "**预测值**" 列中`1`，选择。  
  
7.  选择 "**提升图**" 选项卡以显示提升图。  
  
     您现在会注意到，所有三个决策树模型与随机推测模型相比都有了显著提升，而且表现还超过了聚类分析和 Naive-Bayes 模型。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关筛选器的详细信息，请参阅[&#40;Analysis Services 挖掘模型的筛选器-数据挖掘&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)。  
  
 有关如何将筛选器应用于嵌套表的示例，请参阅[数据挖掘的中间教程 &#40;Analysis Services 数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)。  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [利用提升图测试准确性 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一课  
 [第6课：创建和使用预测 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [中级数据挖掘教程 &#40;Analysis Services 数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [挖掘模型任务和操作指南](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [从挖掘模型中删除筛选器](../../2014/analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)   
 [挖掘模型的筛选器 &#40;Analysis Services 数据挖掘&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
