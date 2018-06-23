---
title: 浏览 Naive Bayes 模型 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f9160b48-3beb-439c-9694-f084e1afa625
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 36031bb080ff80c14a4f91bca102bd859df1f539
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014209"
---
# <a name="browsing-a-naive-bayes-model"></a>浏览 Naive Bayes 模型
  当你打开 Naïve Bayes 模型使用**浏览**，具有四个不同窗格交互式查看器中显示该模型。 使用该查看器，可以探索相关性，获取有关模型和基础数据的信息。  
  
-   [依赖关系网络](#bkmk_DepNet)  
  
-   [属性配置文件](#bkmk_AttProf)  
  
-   [属性特征](#bkmk_AttChar)  
  
-   [属性对比](#bkmk_AttDisc)  
  
##  <a name="BKMK_Tabs"></a> 浏览该模型  
 该查看器可以帮助您探索由 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 模型发现的输入与输出属性（输入和依赖变量）之间的交互。  
  
 如果你想要使用的 Naïve Bayes 查看器进行试验，使用[分类向导&#40;for Excel 的数据挖掘外接&#41;](classify-wizard-data-mining-add-ins-for-excel.md)向导在数据挖掘功能区中，单击**高级**选项，然后更改要使用的 Naïve Bayes 算法的算法  
  
 这些示例，我们在示例工作簿，使用源数据和分组列， **Yearly Income**，分组五个收入，从**非常低**到**非常高**。 然后 Naïve Bayes 模型分析与每个收入类别相关的因素。  
  
###  <a name="bkmk_DepNet"></a> 依赖关系网络  
 你将使用第一个窗口**依赖关系网络**。 它一目了然地显示哪些输入与选定结果紧密相关。  
  
 ![Naive Bayes 查看器中的依赖关系网络](media/dm13-nb.gif "Naive Bayes 查看器中的依赖关系网络")  
  
##### <a name="explore-the-dependency-network"></a>探索依赖关系网络  
  
1.  首先，单击目标结果， **Yearly Income**，其表示为关系图中的节点。  
  
     目标变量周围突出显示的节点在统计上与此结果相关。 使用查看器底部的图例可了解关系的性质。  
  
2.  单击查看器左侧的滑块并向下拖动。  
  
     此控件根据依赖关系强度筛选独立变量。 向下拖动滑块时，只有最强链接保留在图形中。  
  
3.  具有筛选图形后，单击此按钮时，**复制图形视图**。 然后在 Excel 中选择工作表并按 Ctrl+V。  
  
     此选项可复制所选视图，包括筛选器和突出显示。  
  
 [返回页首](#BKMK_Tabs)  
  
###  <a name="bkmk_AttProf"></a> 属性配置文件  
 **属性配置文件**windows 提供的如何所有其他变量相关的单个结果的可视指示。  
  
##### <a name="explore-the-profiles"></a>探索剖面图  
  
1.  若要隐藏部分值以便于比较结果，请单击列标题并将其拖至另一列下。  
  
     ![属性在 Naive Bayes 查看器中的配置文件](media/dm13-nb-attprof.gif "属性 Naive Bayes 查看器中的配置文件")  
  
2.  单击任何单元格可查看的中值的分布**挖掘图例**。  
  
     因为将显示与不同结果关联的属性，所以很容易找到令人感兴趣的相关性，例如，收入是如何按地区分布的。  
  
3.  若要获取的数据，此视图，请单击**复制到 Excel**。 将在一个新工作表中生成一个表，其中显示了各个属性和结果之间的相关性。 在此 Excel 表中，您可以轻松地隐藏或筛选列。  
  
 [返回页首](#BKMK_Tabs)  
  
###  <a name="bkmk_AttChar"></a> 属性特征  
 **属性特性，而**视图可用于深入探讨特定结果变量和相关的因素。  
  
 ![属性在 Naive Bayes 查看器中的特征](media/dm13-nb-viewer.gif "属性 Naive Bayes 查看器中的特征")  
  
##### <a name="explore-the-attribute-characteristics"></a>探索属性特征  
  
1.  单击**值**和选择从一项**值**。  
  
     在选择目标结果时，图形会更新以显示与该结果关联性最强的因素，并按重要性排序。  
  
     请注意，如果创建模型使用[分析关键影响因素&#40;for Excel 表分析工具&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)选项，您可以创建具有多个可预测属性的模型。 但是，数据挖掘外接程序中的所有其他向导会限制为一个可预测属性。  
  
2.  单击**复制到 Excel**若要创建表，请在新表中，列出与所选的目标结果相关的所有属性的分数。  
  
 [返回页首](#BKMK_Tabs)  
  
###  <a name="bkmk_AttDisc"></a> 属性对比  
 **属性对比**视图可帮助进行比较的两个结果或与所有其他结果的一个结果。  
  
 ![属性在 Naive Bayes 查看器对比](media/dm13-nb-attdisc.gif "属性 Naive Bayes 查看器中的对比")  
  
##### <a name="explore-attribute-discrimination"></a>探索属性对比  
  
1.  使用的控件，**值 1**和**值 2**，以选择你想要比较的结果。  
  
     例如，在此模型中没有一些有趣的属性在低收入组中，因此我们在第一个下拉列表中，选择最低的收入组并选择**所有其他状态**在第二个下拉列表中。  
  
     属性按重要程度排序（根据定型数据计算）。 因此，职业是与收入关联最密切的因素（至少对于此目标组来说是这样）。  
  
     若要查看的确切数字，请单击的彩色的条和视图**挖掘图例**。  
  
2.  请注意，低收入还与欧洲地区相关。  
  
     Naïve Bayes 模型不支持深化；但是，如果要调查与此结果组关联的情况，可以使用查询。 有关查询在这种类型的模型上的信息，请参阅[Naive Bayes 模型查询示例](data-mining/naive-bayes-model-query-examples.md)。  
  
 [返回页首](#BKMK_Tabs)  
  
## <a name="see-also"></a>请参阅  
 [浏览 Excel 中的模型&#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  