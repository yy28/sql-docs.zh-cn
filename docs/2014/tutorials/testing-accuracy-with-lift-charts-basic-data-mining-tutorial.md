---
title: 测试准确性，但提升图 （数据挖掘基础教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 822d414b-4a39-473f-80c3-53476e30655a
caps.latest.revision: 48
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8ce5ba972af0b1dda27521dbc5dc58041e386a69
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312555"
---
# <a name="testing-accuracy-with-lift-charts-basic-data-mining-tutorial"></a>测试提升图的准确性（数据挖掘基础教程）
  上**挖掘准确性图表**选项卡上的数据挖掘设计器中，你可以计算以及每个模型进行预测，并比较直接针对其他模型的结果的每个模型的结果。 比较此方法被称为*提升图*。 通常，用提升图或分类准确性对挖掘模型的预测准确性进行度量。 在本教程中，我们将只使用提升图。  
  
 在本主题中，您将完成下列任务：  
  
-   [选择输入的数据](#BKMK_InputData)  
  
-   [配置准确性图表参数](#BKMK_Selecting)  
  
##  <a name="BKMK_InputData"></a> 选择输入的数据  
 测试挖掘模型准确性的第一步是选择将用于测试的数据源。 您将根据测试数据测试模型的准确性，然后将它们与外部数据一起使用。  
  
#### <a name="to-select-the-data-set"></a>若要选择的数据设置  
  
1.  切换到**挖掘准确性图表**数据挖掘设计器中的选项卡[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]和选择**输入选择**选项卡。  
  
2.  在**选择要用于准确性图表的数据集**组中，选择**使用挖掘结构测试事例**。 这是当您创建挖掘结构时留出的测试数据。  
  
     有关其他选项的详细信息，请参阅[选择准确性图表类型和设置图表选项](../../2014/analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)。  
  
##  <a name="BKMK_Selecting"></a> 设置准确性图表参数  
 若要创建准确性图表，必须定义三个内容：  
  
-   应在准确性图表中包含哪些模型？  
  
-   您希望测量哪个可预测的属性？ 一些模型可能有多个目标，但是每个图表一次只能测量一个结果。  
  
     若要使用一个列作为**可预测列名称**在准确性图表，列必须具有的使用类型`Predict`或`Predict Only`。 此外，目标列的内容类型必须为 `Discrete` 或 `Discretized`。 换言之，您无法使用提升图针对连续数值输出测量准确性。  
  
-   是要测量模型的一般准确性还是预测某一特殊值（例如 [Bike Buyer] = ‘是’）时的准确性  
  
#### <a name="to-generate-the-lift-chart"></a>生成提升图  
  
1.  上**输入选择**数据挖掘设计器选项卡下**选择要在提升图中显示的可预测的挖掘模型列**，选中的复选框**同步预测列和值**。  
  
2.  在**可预测列名称**列中，验证**Bike Buyer**选择每个模型。  
  
3.  在**显示**列中，选择每个模型。  
  
     默认情况下，系统会选中挖掘结构中的所有模型。 可以决定不包含某一模型，但对于本教程，请选中所有模型。  
  
4.  在**预测值**列中，选择**1**。 对于具有相同可预测列的每个模型，将自动填充相同的值。  
  
5.  选择**提升图**选项卡。  
  
     当您单击该选项卡时，将执行一个预测查询以获取测试数据的预测结果，并针对已知值比较这些结果。 结果将绘制在图上。  
  
     如果你指定特定的目标结果使用**预测值**选项，提升图绘制随机推测的结果和理想的模型的结果。  
  
    -   随机猜测线显示没有使用任何数据进行预测时模型的准确程度：即两个结果之间的 50-50 拆分。 提升图帮助您可视化模型在与随机猜测进行比较时结果获得改进的程度。  
  
    -   理想模型线表示准确性的上限。 它显示如果您的模型始终预测准确可能获得的最大好处。  
  
     您创建的挖掘模型通常将处于这两种极限情况之间。 与随机推测相比的任何改善被视为可*提升*。  
  
6.  使用图例可以查找表示理想模型和随机推测模型的彩色线。  
  
     你将注意到，`TM_Decision_Tree`模型提供的最大提升，outperforming 聚类分析和 Naive Bayes 模型。  
  
 类似于在本课程中创建一个提升图深入说明，请参阅[提升图&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [测试筛选后的模型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/testing-a-filtered-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [提升图&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [提升图表选项卡&#40;挖掘准确性图表视图&#41;](../../2014/analysis-services/lift-chart-tab-mining-accuracy-chart-view.md)  
  
  