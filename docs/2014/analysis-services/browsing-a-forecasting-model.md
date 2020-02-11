---
title: 浏览预测模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- forecasting [data mining]
- mining models, viewing
- mining model, time series
- time series [data mining]
ms.assetid: ad35a528-1949-4048-8678-3b9760c1c88c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 830aea002e8000feeda061f42af9084696ed6fe8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088493"
---
# <a name="browsing-a-forecasting-model"></a>浏览预测模型
  使用 "**浏览**" 打开预测模型时，该模型将显示在交互式查看器中，类似于中[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的时序模型查看器。 查看器有助于您探索趋势、比较序列、创建预测以及获取有关模型和基础数据的信息。  
  
##  <a name="bkmk_Top"></a>浏览模型  
 用于预测模型的**浏览**查看器提供了一个图表视图，其中显示了一段时间内的趋势，并使您可以创建预测和模型视图，它将时间序列表示为决策树或回归树。  
  
-   [图表视图](#bkmk_charts)  
  
-   [模型视图](#bkmk_Model)  
  
 若要试验预测模型，可以使用示例数据工作簿的 "预测" 选项卡上的示例数据，并使用 &#40;"**数据挖掘**" 功能区中的 "[用于 Excel 的数据挖掘外接程序"&#41;](forecast-wizard-data-mining-add-ins-for-excel.md) &#40;或 "**分析**" 功能区中的 "excel 的数据挖掘外接程序" [&#41;](forecast-table-analysis-tools-for-excel.md)生成时序模型。  
  
###  <a name="bkmk_charts"></a>流程图  
 "**图表**" 选项卡显示一段时间内数据系列的趋势以及预测值。 图表的垂直轴表示序列的值，水平轴表示时间。  
  
##### <a name="explore-the-forecasting-chart"></a>探索预测图  
  
1.  此模型包含多个时序，但是为了简化图表，可显示一个时序或少数几个相关时序。  
  
     ![预测模型中的历史预测](media/dm13-forecast-chart-historicpredictions.gif "预测模型中的历史预测")  
  
     使用复选框只选择北美的销售额预测。  
  
2.  单击 "**预测步骤**" 并键入一个新值，以控制要在图表中看到的未来时间值数。  
  
     默认值为 5。  
  
3.  单击 "历史" 或 "未来" 行中的任意点，查看 "**挖掘图例**" 中显示的该时间点的确切值。  
  
4.  该图表同时显示历史数据和未来数据。 注意带阴影背景的虚线。 这些值是基于模型得出的未来预测信息。  
  
     图表的左侧显示历史数据（您用于建立模型的数据）。  
  
5.  选择 "**显示历史预测**" 选项，以了解时序的稳定性。  
  
     ![针对模型中单个序列的预测](media/dm13-forecast-chart-singleseries.gif "针对模型中单个序列的预测")  
  
     历史预测信息是根据序列为该点预测的值，不同于实际历史值。 如果虚线（使用预测的值绘成）与实线（实际值）之间相距甚远，就表示序列的第一部分或许不能准确预测稍后的值。 您可能需要更多数据，这也可能只是一种周期波动的表现。  
  
6.  选择 "**显示偏差**" 选项可在图表中显示误差线。  
  
     通过误差线，您可以直观地了解预测信息的变化范围。 预测信息的可靠性因源数据而异，不过，在您增加预测步骤数时，将会看到偏差稳定增长。  
  
 **技巧**  
  
-   若要切换 "**挖掘图例**" 的显示，请右键单击图表中的任意点。  
  
     可以通过以下方法查看特定的时间范围：单击图表，将时间选定范围拖到图表上，然后再次单击图表以放大选定的范围。  
  
-   若要获取当前图表的副本，请单击 "**复制到 excel**"，然后单击 Excel 中的工作表。 即会使用您设置的所有选项在工作表中插入图形，包括图例。  
  
     但是，此图形是静态的，因此您不能编辑图例或查看基础数据;如果需要更交互式的图表视图，请使用[Visio](viewing-data-mining-models-in-visio-data-mining-add-ins.md)查看器。  
  
-   单击查看器菜单栏中的 " **Abs** "，在绝对曲线和相对曲线之间切换。  
  
     如果图表中包含多个模型，但每个模型的数据比例差异很大，则此选项将非常有用。  
  
     举例来说，如果太平洋地区商店新近开业，销售额很低，则在使用绝对值时，显示太平洋销售额的线可能显示为平的，难以看出实际变化，而其他模型将以更常规的比例显示。  
  
     通过切换视图以使用相对值，您可以规范化不同模型的比例，将差异显示为百分比更改。 如果更改是相对于每个模型的，则可以在同一图形中显示这些模型，而不会出现明显的扭曲。  
  
 [浏览模型](#bkmk_Top)  
  
###  <a name="bkmk_Model"></a>模式  
 还可以将预测模型表示为决策树，或者，在序列基本呈线性时表示为回归模型。  
  
 例如，在此模型中，基于某一特定条件的回归公式中存在差异，因此树拆分为两个分支，每个分支有一个不同的回归公式。  
  
 ![筛选预测模型中单个序列](media/dm13-forecast-model-northamerica.gif "筛选预测模型中单个序列")  
  
##### <a name="explore-the-forecasting-model-as-a-tree"></a>按树的形式探索预测模型  
  
1.  单击 "**树**" 下拉列表并选择要显示的模型。  
  
     为每个可预测属性显示一个单独的树或回归节点。 举例来说，如果您的数据包含欧洲、北美和太平洋的销售额，您将看到三个不同的模型，每个数据序列对应一个模型。  
  
2.  拖动 "**显示级别**" 滑块以筛选出树的较低级别，并将重点放在最重要的拆分上。  
  
3.  单击每个节点可以在 "**挖掘图例**" 中查看一些描述性统计信息。  
  
     鼠标暂停在某个节点上后，工具提示也将显示相同的统计信息以及描述该节点的完整公式。  
  
4.  如果要复制 "**挖掘图例**" 中的信息，请右键单击 "**挖掘图例**"，选择 "**复制**"，然后在 Excel 工作表中单击。 "**复制到 Excel** " 选项将复制图形，而不是统计信息。  
  
 [浏览模型](#bkmk_Top)  
  
## <a name="see-also"></a>另请参阅  
 [在 Excel 中浏览模型 &#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
