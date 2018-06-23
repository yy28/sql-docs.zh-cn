---
title: 测试筛选后的模型 （数据挖掘基础教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f0d74f8c-600d-4df5-a742-695e6947a071
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0dfb4b3ae34b230c591071f02cdaa9b0984cf05e
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312545"
---
# <a name="testing-a-filtered-model-basic-data-mining-tutorial"></a>测试筛选后的模型（数据挖掘基础教程）
  现在，您可以确定`TM_Decision_Tree`模型是最准确的您将自定义模型以更好地满足的需求[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]客户发送目标邮件营销活动。 具体来说，市场部希望了解男客户和女客户是否存在特征差异。 信息可以帮助他们决定哪些杂志用于广告和要在其邮件功能的产品。  
  
## <a name="using-filters"></a>使用筛选器  
 通过筛选，您可以轻松地创建基于数据子集生成的模型。 筛选器只应用于该模型，而且不会更改基础数据源。  
  
 在本课中，您将创建一个针对性别进行了筛选的模型，以预测男性和女性中对自行车购买行为影响最大的特征。  
  
 首先将使一份`TM_Decision_Tree`模型。  
  
#### <a name="to-copy-the-decision-tree-model"></a>复制决策树模型  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，在解决方案资源管理器，选择**BasicDataMining**。  
  
2.  单击 **“挖掘模型”** 选项卡。  
  
3.  右键单击`TM_Decision_Tree`模型，并选择**新建挖掘模型。**  
  
4.  在**模型名称**字段中，键入`TM_Decision_Tree_Male`。  
  
5.  单击“确定” 。  
  
 然后为模型创建一个筛选器，用于根据客户的性别选择客户。  
  
#### <a name="to-create-a-case-filter-on-a-mining-model"></a>创建挖掘模型的事例筛选器  
  
1.  右键单击`TM_Decision_Tree_Male`挖掘模型，以打开快捷菜单。  
  
     --或者--  
  
     选择该模型。 在 **“挖掘模型”** 菜单上，选择 **“设置模型筛选器”**。  
  
2.  在 **“模型筛选器”** 对话框的 **“挖掘结构列”** 文本框中，单击网格中的第一行。  
  
     下拉列表只显示该表中列的名称。  
  
3.  在挖掘结构列文本框中，选择**性别**。  
  
     文本框左侧的图标会发生改变，以指示所选项是表还是列。  
  
4.  单击**运算符**文本框并选择从列表中的等号 （=） 运算符。  
  
5.  单击**值**文本框，然后键入**M**。  
  
6.  单击网格中的下一行。  
  
7.  单击**确定**关闭**模型筛选器**对话框。  
  
     筛选器显示在**属性**窗口。 或者，你可以启动**模型筛选器**对话框从**属性**窗口。  
  
8.  重复上述步骤，但这次命名模型`TM_Decision_Tree_Female`和类型**F**中**值**文本框。  
  
## <a name="process-the-filtered-models"></a>处理筛选的模型  
 模型经过部署和处理后才能使用。 处理模型的详细信息，请参阅[目标邮寄结构中的处理模型&#40;Basic Data Mining Tutorial&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)。  
  
#### <a name="to-process-the-filtered-model"></a>处理筛选后的模型  
  
1.  右键单击`TM_Decision_Tree_Male`模型，并选择**处理挖掘结构和所有模型**s  
  
2.  单击**运行**来处理新模型。  
  
3.  处理完成后，单击**关闭**这两个处理窗口上。  
  
     你现在有两个新的模型中显示**挖掘模型**选项卡。  
  
## <a name="evaluate-the-results"></a>评估结果  
 查看结果并评估筛选后的模型的准确性，与您对前三个模型的操作非常相似。 有关详细信息，请参阅：  
  
 [浏览决策树模型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
 [测试准确性，但提升图&#40;数据挖掘基础教程&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
#### <a name="to-explore-the-filtered-models"></a>浏览筛选后的模型  
  
1.  选择**挖掘模型查看器**选项卡中**数据挖掘设计器**。  
  
2.  在挖掘模型中，选择`TM_Decision_Tree_Male`。  
  
3.  滑动**显示级别**到`3`。  
  
4.  更改**后台**值赋给`1`。  
  
5.  将光标放置标记的节点在**所有**若要查看与非自行车购买者的自行车购买者数。  
  
6.  重复步骤 1-5 的`TM_Decision_Tree_Female`。  
  
7.  浏览的结果`TM_Decision_Tree`和模型筛选的性别。 与所有自行车购买者相比，男性和女性自行车购买者与未经筛选自行车购买者具有一些相同特征，但所有这三个群体也存在一些重要差异。 这是有用的信息，[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]可用于开发其市场营销活动。  
  
#### <a name="to-test-the-lift-of-the-filtered-models"></a>测试筛选后的模型的提升  
  
1.  切换到**挖掘准确性图表**数据挖掘设计器中的选项卡[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]和选择**输入选择**选项卡。  
  
2.  在**选择要用于准确性图表的数据集**组中，选择**使用挖掘结构测试事例**。  
  
3.  上**输入选择**数据挖掘设计器选项卡下**选择要在提升图中显示的可预测的挖掘模型列**，选中的复选框**同步预测列和值**。  
  
4.  在**可预测列名称**列中，验证**Bike Buyer**选择每个模型。  
  
5.  在**显示**列中，选择每个模型。  
  
6.  在**预测值**列中，选择`1`。  
  
7.  选择**提升图**选项卡以显示提升图。  
  
     您现在会注意到，所有三个决策树模型与随机推测模型相比都有了显著提升，而且表现还超过了聚类分析和 Naive-Bayes 模型。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关筛选器的详细信息，请参阅[挖掘模型的筛选器&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)。  
  
 有关如何将筛选器应用于嵌套表的示例，请参阅[中间 Data Mining Tutorial &#40;Analysis Services-数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)。  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [测试准确性，但提升图&#40;数据挖掘基础教程&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一课  
 [第 6 课： 创建和使用预测&#40;数据挖掘基础教程&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [中间数据挖掘教程&#40;Analysis Services-数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [挖掘模型任务和操作指南](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [从挖掘模型中删除筛选器](../../2014/analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)   
 [挖掘模型的筛选器&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  