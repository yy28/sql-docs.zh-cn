---
title: 指示器（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10545"
- "10547"
- sql12.rtp.rptdesigner.indicatorproperties.general.f1
- sql12.rtp.rptdesigner.indicatorproperties.action.f1
- "10546"
- sql12.rtp.rptdesigner.indicatorproperties.validateandstates.f1
ms.assetid: 2edbd279-be39-4d97-b1b6-ddbc5b17c422
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 042a81dc4850c592542ca0764842b45a7756468d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63209504"
---
# <a name="indicators-report-builder-and-ssrs"></a>指示器（报表生成器和 SSRS）
  指示器是以直观的形式提供单个数据值的状态的最小化仪表。 表示指示器及其状态的图标十分简单，并且即使在以小尺寸使用时也保持有效的外观。  
  
 您可以在报表中使用状态指示器以显示如下内容：  
  
-   通过使用趋于上升、平（无变化）或趋于下降箭头显示趋势。  
  
-   通过使用公认的符号（例如复选标记和感叹号）显示状态。  
  
-   通过使用公认的形状（例如交通灯和标志）显示情况。  
  
-   通过使用显示进展情况的公认的形状和符号（例如正方形中的象限数和星形的数目）显示等级。  
  
 尽管指示器可单独用于面板或自由格式的报表中，但它们最常用于表或矩阵中以便形象地展现行或列中的数据。 下图显示具有交通灯指示器的一个表，它按销售人员和区域展现今年迄今为止的销售额。  
  
 ![rs_IndicatorTableTrafficLight](../media/rs-indicatortabletrafficlight.gif "rs_IndicatorTableTrafficLight")  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供可按原样使用的内置指示器集和指示器图标，但您也可以自定义单独的指示器图标和指示器集以满足您的需要。  
  
 若要详细了解如何将指示器用作 KPI，请参阅[教程：向报表添加 KPI（报表生成器）](../tutorial-adding-a-kpi-to-your-report-report-builder.md)。  
  
> [!NOTE]  
>  您可以将指示器作为报表部件与报表分开发布。 [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ComparingIndicatorsToGauges"></a> 将指示器与仪表进行比较  
 尽管在外观上差别很大，但指示器就是简单的仪表。 指示器和仪表都显示单个数据值。 主要差别就是仪表具有元素（如框架和指针）。 指示器只具有状态、图标和（可选）标签。 指示器状态类似于仪表范围。  
  
 与仪表一样，指示器位于仪表面板内。 在您想要通过使用 **“指示器属性”** 对话框或“属性”窗格配置某一指示器时，需要选择指示器，而非面板。 否则，可用选项将应用于仪表面板选项，并且您不能配置指示器。 下图显示了指示器仪表面板中的一个选定指示器。  
  
 ![rs_GaugePanelWithIndicator](../media/rs-gaugepanelwithindicator.gif "rs_GaugePanelWithIndicator")  
  
 仪表可能比指示器的显示效果更好，具体取决于您描绘数据值的方式。 有关详细信息，请参阅 [仪表（报表生成器和 SSRS）](gauges-report-builder-and-ssrs.md)。  
  
  
##  <a name="ChoosingIndicatorTypes"></a> 选择要使用的指示器类型  
 使用正确的指示器集是立即传达数据含义的关键，无论数据是处于详细信息行中、表或矩阵的行或列组中，还是单独位于表体或面板中。 内置指示器集具有三个或者更多的图标。 这些图标在形状和/或颜色上各不相同。 每个图标都传达一种不同的数据状态。  
  
 下表列出了内置的指示器集，并描述它们的一些常见用途。  
  
|指示器集|指示器类型|  
|-------------------|--------------------|  
|![Rs_DirectionalIcons](../media/rs-directionalicons.gif "Rs_DirectionalIcons")|方向：通过使用上升、下降、平（无变化）、趋于上升或趋于下降箭头指示趋势。|  
|![Rs_SymbolIcons](../media/rs-symbolicons.gif "Rs_SymbolIcons")|符号：通过使用公认的符号（例如复选标记和感叹号）指示状态。|  
|![Rs_ShapeIcons](../media/rs-shapeicons.gif "Rs_ShapeIcons")|形状：通过使用公认的形状（例如交通标志和菱形形状）指示情况。|  
|![rs_RatingIcons](../media/rs-ratingicons.gif "rs_RatingIcons")|等级：通过使用显示进展值的公认的形状和符号（例如正方形中的象限数）指示等级。|  
  
 您选择某一指示器集后，可通过在针对指示器的对话框中或“属性”窗格中设置其属性，自定义该集中每个指示器图标的外观。 可以使用内置的颜色、图标和大小来配置指示器，也可以使用表达式来配置指示器。  
  
  
##  <a name="CustomizingIndicators"></a> 自定义指示器  
 可以对指示器进行自定义，以便满足您的需要。 您可以按以下方式修改指示器集以及某一集内的单独指示器图标：  
  
-   更改指示器图标的颜色。 例如，您可能希望将某一指示器集的配色方案设置为单色，或者使用并非默认颜色的其他颜色。  
  
-   更改指示器集中的图标。 例如，您可能要在一个指示器集中使用星形、圆形和正方形图标。  
  
-   指定指示器的开始值和结束值。 例如，您可能希望为 75% 的指示器值使用一个图标，以扭曲数据显示。  
  
-   将图标添加到指示器集。 例如，您可能希望向指示器集添加其他图标，以便以更详细的方式区分指示器值。  
  
-   从指示器集中删除图标，以便通过只使用几个图标使数据显示更简单。  
  
 有关详细信息，请参阅 [更改指示器图标和指示器集（报表生成器和 SSRS）](change-indicator-icons-and-indicator-sets-report-builder-and-ssrs.md)。  
  
  
##  <a name="UsingIndicatorsInTablesMatrices"></a> 在表和矩阵中使用指示器  
 指示器的简单形状使其很适合在表和矩阵中使用。 指示器甚至在小尺寸下效果也很好。 这使它们可用于报表的详细信息行或组行中。  
  
 下图显示具有一个表的报表，该表使用方向指示器集“四个箭头(彩色)”来指示销售额。 报表中的指示器图标配置为使用蓝色阴影来代替默认颜色：红色、黄色和绿色。  
  
 ![rs_IndicatorReportBlueArrows](../media/rs-indicatorreportbluearrows.gif "rs_IndicatorReportBlueArrows")  
  
 有关添加、更改和删除指示器的详细信息，请参阅 [添加或删除指示器（报表生成器和 SSRS）](add-or-delete-an-indicator-report-builder-and-ssrs.md)。  
  
 在您首次向报表添加一个指示器时，该指示器配置为使用默认值。 然后，您可以更改这些默认值，以便指示器以您所需的方式描绘数据。 您可以更改指示器图标的外观、指示器选择要使用的图标的方式，并可以更改指示器集使用的图标。 有关详细信息，请参阅 [更改指示器图标和指示器集（报表生成器和 SSRS）](change-indicator-icons-and-indicator-sets-report-builder-and-ssrs.md)。  
  
 默认情况下，指示器配置为使用百分比作为度量单位，并且自动检测数据中的最小值和最大值。 指示器集中的每个图标都具有百分比范围。 百分比范围的数目依赖于图标集中图标的数目，但这些范围具有相同的大小和顺序。 例如，如果图标集具有五个图标，则有五个百分比范围，每个范围占总大小的 20%。 第一个范围以 0 开始、以 20 结束，第二个范围以 20 开始、以 40 结束，依此类推。 报表上的指示器使用的图标来自其百分比范围在指示器数据值处于的范围内的指示器集。 对于图标集中的每个图标，您可以更改百分比范围。 可以通过提供值或表达式来显式设置最小值和最大值。 您可以将度量单位更改为数值。 在此情况下，不要为数据指定最小值或最大值。 而是为指示器使用的每个图标仅提供开始值和结束值。 有关详细信息，请参阅 [设置和配置度量单位（报表生成器和 SSRS）](set-and-configure-measurement-units-report-builder-and-ssrs.md)。  
  
 指示器通过同步指定作用域内的指示器数据值，提供数据值。 默认情况下，作用域是指示器的父容器，例如包含指示器的表或矩阵。 您可以通过根据报表的布局选择不同的作用域，更改指示器的同步。 指示器可以忽略同步。 有关详细信息，请参阅 [设置同步作用域（报表生成器和 SSRS）](set-synchronization-scope-report-builder-and-ssrs.md)。  
  
 有关了解和设置报表作用域的常规信息，请参阅[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 指示器仅使用单个值。 如果您需要显示多个数据值，则应使用迷你图或数据条来代替指示器。 它们可以表示多个数据值，即使在小尺寸下也简单、易于理解，并且适合在表和矩阵中使用。 有关详细信息，请参阅 [迷你图和数据条（报表生成器和 SSRS）](sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
  
##  <a name="SizingIndicatators"></a> 调整指示器的大小以便提供最佳的视觉效果  
 除了颜色、方向和形状外，您还可以使用大小来提供最佳的指示器视觉效果。 假定某一报表使用指示器来显示客户对不同类型自行车的满意度。 指示器使用的图标可以根据客户满意度配置为不同的大小。 满意度越高，在报表中出现的图标就越大。 下图显示了自行车的销售报表以及反映销售额的图标大小。  
  
 您可以使用表达式基于指示器使用的字段值动态设置星形的大小。 有关详细信息，请参阅 [使用表达式指定指示器的大小（报表生成器和 SSRS）](specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs.md)。  
  
 若要了解有关编写和使用表达式的详细信息，请参阅[表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)。  
  
  
##  <a name="IncludingIndicatorsInGauges"></a> 在仪表面板中包括指示器和仪表  
 指示器始终位于仪表面板内。 仪表面板是可以包括一个或多个仪表和状态指示器的顶级容器。 仪表面板可以包含子仪表或指示器，也可以包含相邻仪表或指示器。 如果您使用指示器作为仪表的子级，则可以通过显示在仪表中显示的数据值的状态，进一步地展现数据。 例如，仪表内的指示器可以显示一个绿色圆圈，向您指示仪表指向的值处于值范围的上 33% 中。 如果并排使用仪表和指示器，您可以通过不同的方式表示数据。 在任何一种情况下，指示器和仪表都可以使用相同或不同的数据字段。  
  
 下图显示一个与仪表并排且处于仪表内的指示器。  
  
 ![rs_GaugePanelWithIndicatorAndGauge](../media/rs-gaugepanelwithindicatorandgauge.gif "rs_GaugePanelWithIndicatorAndGauge")  
  
 有关详细信息，请参阅 [在仪表面板中包括指示器和仪表（报表生成器和 SSRS）](include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs.md)。  
  
 有关使用仪表的详细信息，请参阅 [仪表（报表生成器和 SSRS）](gauges-report-builder-and-ssrs.md)。  
  
  
##  <a name="SequenceIndicatorStates"></a> 指示器状态的序列  
 **“指示器属性”** 对话框的 **“值和状态”** 选项卡中指示器状态的序列影响在指示器状态的起始值和结束值重叠时将为数据值显示的指示器图标。  
  
 无论您是使用百分比还是数字状态度量单位，都可能会发生此情况。 在您使用数字度量单位时更有可能发生此情况，因为您为此度量值提供特定值。 在您对报表数据值进行四舍五入时也更有可能发生此情况，因为这往往会使数据更离散。  
  
 下面的方案描述当在“3 个箭头(彩色)”方向指示器中更改由三个状态构成的序列时，将会如何影响数据的可视化。 默认情况下，该序列为：  
  
1.  红色向下箭头  
  
2.  黄色水平箭头  
  
3.  绿色向上箭头  
  
 下面的方案显示对于四个不同的状态序列及其值范围，这些序列是如何影响数据可视化的。  
  
 在这些方案中，“3 个箭头(彩色)”指示器使用数字状态度量。  
  
|状态序列|起始值|结束值|  
|--------------------|-----------------|---------------|  
|Red|0|3500|  
|Yellow|3500|5000|  
|绿色|5000|10000|  
  
 红色向下箭头显示值 3500，而黄色水平箭头显示值 5000。  
  
|状态序列|起始值|结束值|  
|--------------------|-----------------|---------------|  
|绿色|5000|10000|  
|Yellow|3500|5000|  
|Red|0|3500|  
  
 黄色水平箭头显示值 3500，而绿色向上箭头显示值 5000。  
  
|状态序列|起始值|结束值|  
|--------------------|-----------------|---------------|  
|绿色|5000|10000|  
|Red|0|3500|  
|Yellow|3500|5000|  
  
 红色向下箭头显示值 3500，而绿色向上箭头显示值 5000。  
  
|状态序列|起始值|结束值|  
|--------------------|-----------------|---------------|  
|Yellow|3500|5000|  
|Red|0|3500|  
|绿色|5000|10000|  
  
 黄色向下箭头现在显示值 3500 和 5000。  
  
 总之，计算将开始，并且在指示器状态列表和报表的顶部将显示与具有数据适合的值范围的第一个指示器状态相关联的指示器图标。 通过更改指示器状态的序列，您可以影响数据值的可视化。  
  
  
##  <a name="HowTo"></a> 操作指南主题  
 本节列出的过程说明如何添加、更改和删除指示器，如何配置和自定义指示器，以及如何在仪表中使用指示器。  
  
-   [添加或删除指示器（报表生成器和 SSRS）](add-or-delete-an-indicator-report-builder-and-ssrs.md)  
  
-   [更改指示器图标和指示器集（报表生成器和 SSRS）](change-indicator-icons-and-indicator-sets-report-builder-and-ssrs.md)  
  
-   [设置和配置度量单位（报表生成器和 SSRS）](set-and-configure-measurement-units-report-builder-and-ssrs.md)  
  
-   [设置同步作用域（报表生成器和 SSRS）](set-synchronization-scope-report-builder-and-ssrs.md)  
  
-   [使用表达式指定指示器的大小（报表生成器和 SSRS）](specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs.md)  
  
-   [在仪表面板中包括指示器和仪表（报表生成器和 SSRS）](include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs.md)  
  
  
## <a name="see-also"></a>请参阅  
 [仪表（报表生成器和 SSRS）](gauges-report-builder-and-ssrs.md)   
 [迷你图和数据条（报表生成器和 SSRS）](sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)  
  
  
