---
title: "使用 Microsoft 时序查看器浏览模型 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], continuous columns
- mining model content, viewing
- Microsoft Time Series Viewer
- charts [Analysis Services]
- Time Series Viewer [Analysis Services]
- continuous columns
- regression algorithms [Analysis Services]
ms.assetid: a77c16cd-1cd0-4fc5-afeb-d1dab30d1e25
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6eaa320911fbba0f46472750bde9293b36430b46
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="browse-a-model-using-the-microsoft-time-series-viewer"></a>使用 Microsoft 时序查看器浏览模型
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序查看器显示由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法生成的挖掘模型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法是一种回归算法，用于在预测方案中创建数据挖掘模型以预测连续列（如产品销量）。 这些时序模型可以包含基于不同算法的信息：  
  
-   ARTxp 算法，针对短期预测进行了优化。  
  
-   ARIMA 算法，针对长期预测进行了优化。  
  
-   ARTxp 和 ARIMA 的混合算法。  
  
 有关这些算法的详细信息，请参阅 [Microsoft Time Series Algorithm](../../analysis-services/data-mining/microsoft-time-series-algorithm.md) 和 [Microsoft Time Series Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)。  
  
> [!NOTE]  
>  若要查看有关模型中使用的公式以及所发现的模式的详细信息，请使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般内容树查看器。 有关详细信息，请参阅[使用 Microsoft 一般内容树查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般内容树查看器（数据挖掘）](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)。  
  
##  <a name="BKMK_ViewerTabs"></a> 查看器的选项卡  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中浏览挖掘模型时，该模型会显示在其相应查看器的数据挖掘设计器的 **“挖掘模型查看器”** 选项卡上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序查看器包含下列选项卡：  
  
-   [Model](#BKMK_Tree)  
  
-   [图表](#BKMK_Charts)  
  
 **注意** 所显示的有关模型内容的信息以及挖掘图例中的信息取决于模型使用的算法。 不过，无论算法组合如何， **“模型”** 和 **“图表”** 选项卡都是相同的。  
  
###  <a name="BKMK_Tree"></a> Model  
 创建时序模型时, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将已完成的模型显示为树。 如果数据包含多个事例序列， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会为每个序列生成单独的树。 例如，您要预测太平洋、北美和欧洲地区的销售。 对每个地区的预测都是事例序列。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会为其中的每个序列生成单独的树。 若要查看某一特定序列，可从 **“树”** 列表中选择该数据序列。  
  
 对于每个树，时序模型都包含一个 **“全部”** 节点，然后分出一系列的节点，这些节点代表算法发现的周期性结构。 单击各个节点可以显示事例数之类的统计信息和公式。  
  
 如果创建模型时只使用 ARTxp，则根节点的 **“挖掘图例”** 只包含事例总数。 对于每个非根节点，“挖掘图例”会包含树杈的更详细的信息：例如，它可能会显示节点的公式和事例数量。 图例中的“规则”  包含标识序列的信息以及规则适用的时间段。 例如，图例文本 `M200 Europe Amount -2` 指示节点表示 M200 Europe 序列在两个时间段之前一段时间的模型。  
  
 如果创建模型时只使用 ARIMA，则 **“模型”** 选项卡包含一个标题为 **“全部”**的单个节点。 根节点的 **“挖掘图例”** 包含 ARIMA 公式。  
  
 如果创建的是混合模型，则根节点只包含事例数和 ARIMA 公式。 在根节点之后，树拆分为对应于各个周期性结构的单独节点。 对于每个非根节点，挖掘图例同时包含 ARTxp 和 ARIMA 算法、节点的公式和节点中的事例数。 首先列出的是 ARTxp 公式，并标记为树节点公式。 接着是 ARIMA 公式。 有关如何解释此信息的详细信息，请参阅 [Microsoft Time Series Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)。  
  
 通常，决策树图在查看器左侧显示最重要的树杈，即 **“全部”** 节点。 在决策树中， **“全部”** 节点之后的树杈最为重要，因为它包含对定型数据中的事例进行最为严格的区分的条件。 在时序模型中，主分支指示最有可能的季节性周期。 **“全部”** 节点之后的树杈显示在分支的右侧。  
  
 您可以展开或折叠决策树中的各个节点，以显示或隐藏各节点后出现的拆分。 您还可以使用 **“决策树”** 选项卡上的选项来设置树的显示方式。 使用 **“显示级别”** 滑块，可以调整树中显示的级别数。 使用 **“默认扩展”** 可以设置模型中所有树的默认显示级别数。  
  
 每个节点背景颜色的底纹表示该节点中所包含的事例数。 若要查找某节点的准确事例数，请将指针放在该节点上以查看该节点的提示信息。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Charts"></a> 图表  
 **“图表”** 选项卡显示一个图形，该图形显示预测属性在一段时间内的行为，还显示五个未来预测值。 图表的垂直轴表示序列的值；水平轴表示时间。  
  
> [!NOTE]  
>  时间轴上使用的时间段取决于数据中使用的单位：它们可表示天、月或甚至秒。  
  
 使用 **Abs** 按钮可以在绝对和相对曲线之间切换。 如果图表包含多个模型，则每个模型的数据小数位数可能会有很大差别。 如果使用绝对曲线，则某一模型可能显示为一条无变化的直线，而另一模型则显示巨大的变化。 出现这种情况的原因是一个模型的刻度比例比另一个模型的刻度比例大的多。 通过切换到相对曲线，小数位数将不再显示绝对值，而是显示变化的百分比。 这样将更容易比较那些基于不同小数位数的模型。  
  
 如果挖掘模型包含多个时序，则可以选择在图表中显示一个或多个时序。 为此，只需单击查看器右边的列表，然后从该列表中选择所需的时序。 如果图表过于复杂，则可以通过选中或清除图例中的时序复选框来筛选显示的时序。  
  
 该图表同时显示历史数据和未来数据。 未来数据带有底纹，以区别于历史数据。 历史数据的数据值显示为实线，预测数据的数据值显示为虚线。 可以通过设置 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的属性来更改用于每个序列的线的颜色。 有关详细信息，请参阅 [更改数据挖掘查看器中使用的颜色](../../analysis-services/data-mining/change-the-colors-used-in-the-data-mining-viewer.md)。  
  
 使用缩放选项可以调整显示的时间范围。 也可以通过以下方法查看特定的时间范围：单击图表，将时间选定范围拖到图表上，然后再次单击图表以放大选定的范围。  
  
 使用 **“预测步骤”** 可以选择要在模型中显示多少个未来时间 **“步骤”**。 如果选择 **“显示偏差”** 复选框，则查看器会提供错误栏，这样您就可以查看预测值的准确度。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Microsoft 时序算法](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [时间时序模型查询示例](../../analysis-services/data-mining/time-series-model-query-examples.md)   
 [数据挖掘模型查看器](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
