---
title: 浏览 Naive Bayes 模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f9160b48-3beb-439c-9694-f084e1afa625
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 65b8bb26a72903644b5985d69efc8adb362fe412
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088483"
---
# <a name="browsing-a-naive-bayes-model"></a>浏览 Naive Bayes 模型
  使用 "**浏览**" 打开一个简单的 Bayes 模型时，该模型将显示在具有四个不同窗格的交互式查看器中。 使用该查看器，可以探索相关性，获取有关模型和基础数据的信息。  
  
-   [依赖关系网络](#bkmk_DepNet)  
  
-   [属性配置文件](#bkmk_AttProf)  
  
-   [属性特征](#bkmk_AttChar)  
  
-   [属性对比](#bkmk_AttDisc)  
  
##  <a name="BKMK_Tabs"></a>浏览模型  
 该查看器可以帮助您探索由 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 模型发现的输入与输出属性（输入和依赖变量）之间的交互。  
  
 如果想要试验 Bayes 查看器，请使用 "[分类向导" &#40;&#41;Excel 数据挖掘外接程序](classify-wizard-data-mining-add-ins-for-excel.md)"向导中的" 数据挖掘 "功能区中，单击"**高级**"选项，然后将算法更改为使用" Bayes "算法  
  
 在这些示例中，我们使用了示例工作簿中的源数据，并按从**极低**到**非常高**的顺序将列、**年收入**分组到五个收入组。 然后 Naïve Bayes 模型分析与每个收入类别相关的因素。  
  
###  <a name="bkmk_DepNet"></a>依赖关系网络  
 您将使用的第一个窗口是**依赖关系网络**。 它一目了然地显示哪些输入与选定结果紧密相关。  
  
 ![Naive Bayes 查看器中的依赖关系网络](media/dm13-nb.gif "Naive Bayes 查看器中的依赖关系网络")  
  
##### <a name="explore-the-dependency-network"></a>探索依赖关系网络  
  
1.  首先，单击目标结果 "**年收入**"，它表示为图形中的一个节点。  
  
     目标变量周围突出显示的节点在统计上与此结果相关。 使用查看器底部的图例可了解关系的性质。  
  
2.  单击查看器左侧的滑块并向下拖动。  
  
     此控件根据依赖关系强度筛选独立变量。 向下拖动滑块时，只有最强链接保留在图形中。  
  
3.  对图形进行筛选后，请单击按钮 "**复制图形视图**"。 然后在 Excel 中选择工作表并按 Ctrl+V。  
  
     此选项可复制所选视图，包括筛选器和突出显示。  
  
 [返回页首](#BKMK_Tabs)  
  
###  <a name="bkmk_AttProf"></a>属性配置文件  
 "**属性配置文件**" 窗口可让你直观地指示所有其他变量与各个结果之间的关系。  
  
##### <a name="explore-the-profiles"></a>探索剖面图  
  
1.  若要隐藏部分值以便于比较结果，请单击列标题并将其拖至另一列下。  
  
     ![Naive Bayes 查看器中的属性配置文件](media/dm13-nb-attprof.gif "Naive Bayes 查看器中的属性配置文件")  
  
2.  单击任意单元可以查看 "**挖掘图例**" 中的值的分布。  
  
     因为将显示与不同结果关联的属性，所以很容易找到令人感兴趣的相关性，例如，收入是如何按地区分布的。  
  
3.  若要获取此视图的基础数据，请单击 "**复制到 Excel**"。 将在一个新工作表中生成一个表，其中显示了各个属性和结果之间的相关性。 在此 Excel 表中，您可以轻松地隐藏或筛选列。  
  
 [返回页首](#BKMK_Tabs)  
  
###  <a name="bkmk_AttChar"></a>属性特征  
 "**属性特征**" 视图可用于对特定结果变量的深度检查和相关因素。  
  
 ![Naive Bayes 查看器中的属性特征](media/dm13-nb-viewer.gif "Naive Bayes 查看器中的属性特征")  
  
##### <a name="explore-the-attribute-characteristics"></a>探索属性特征  
  
1.  单击 "**值**"，然后从**值**中选择一个项。  
  
     在选择目标结果时，图形会更新以显示与该结果关联性最强的因素，并按重要性排序。  
  
     请注意，如果使用 "[分析关键影响因素" &#40;表分析工具 "Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md) " 选项创建模型，则可以创建具有多个可预测属性的模型。 但是，数据挖掘外接程序中的所有其他向导会限制为一个可预测属性。  
  
2.  单击 "**复制到 Excel** " 以在新工作表中创建一个表，其中列出了与所选目标结果相关的所有属性的分数。  
  
 [返回页首](#BKMK_Tabs)  
  
###  <a name="bkmk_AttDisc"></a>属性对比  
 "**属性对比**" 视图有助于比较两个结果或一个结果与所有其他结果。  
  
 ![Naive Bayes 查看器中的属性对比](media/dm13-nb-attdisc.gif "Naive Bayes 查看器中的属性对比")  
  
##### <a name="explore-attribute-discrimination"></a>探索属性对比  
  
1.  使用控件 "**值 1** " 和 "**值 2**" 选择要比较的结果。  
  
     例如，在此模型中，低收入组中有一些有趣的属性，因此我们在第一个下拉列表中选择了最低的收入组，并选择了第二个下拉列表中的**所有其他状态**。  
  
     属性按重要程度排序（根据定型数据计算）。 因此，职业是与收入关联最密切的因素（至少对于此目标组来说是这样）。  
  
     若要查看准确的数字，请单击彩色条并查看 "**挖掘图例**"。  
  
2.  请注意，低收入还与欧洲地区相关。  
  
     Naïve Bayes 模型不支持深化；但是，如果要调查与此结果组关联的情况，可以使用查询。 有关此类模型的查询的信息，请参阅[Naive Bayes Model Query 示例](data-mining/naive-bayes-model-query-examples.md)。  
  
 [返回页首](#BKMK_Tabs)  
  
## <a name="see-also"></a>另请参阅  
 [在 Excel 中浏览模型 &#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
