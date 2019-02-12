---
title: 嵌套数据区域（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 15c2bc9b-428a-47ac-9630-8dde925d0595
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1b35399504c840d81573366401ea8f4978f47f58
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026048"
---
# <a name="nested-data-regions-report-builder-and-ssrs"></a>嵌套数据区域（报表生成器和 SSRS）
  可以在一个数据区域（如矩阵）内嵌套另一个数据区域（如图表），通常用于简明显示数据摘要或提供可视显示和表或矩阵显示。  
  
 例如，对于包含在行中按商店分组和在列中按季度分组的销售订单的矩阵（也称为 Tablix），可以向角单元添加表或图表以汇总所有商店的销售额，或者向矩阵列标题添加图表以显示该列中的销售额数据在所有销售额中所占的百分比。  
  
 ![rs_NestedDataRegion](../media/rs-nesteddataregion.gif "rs_NestedDataRegion")  
  
 在此图中，角单元中的饼图和行中的迷你图为嵌套数据区域。  
  
 根据定义，嵌套数据区域基于相同报表数据集。 嵌套数据区域不能基于不同数据集。 若要显示不同数据集的数据，请考虑使用钻取报表或子报表。 有关详细信息，请参阅 [钻取、深化、子报表和嵌套数据区域（报表生成器和 SSRS）](drillthrough-drilldown-subreports-and-nested-data-regions.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-scope-for-a-nested-data-region"></a>了解嵌套数据区域的作用域  
 嵌套数据区域中的数据的作用域是通过它在父数据区域中的放置位置来自动定义的。 例如，嵌套到 Tablix 角单元的图表数据的作用域是在针对数据集、Tablix 数据区域和图表数据区域应用筛选器之后绑定到 Tablix 数据区域的数据集中的数据。 嵌套到 Tablix 单元的 Tablix 的作用域与角单元的作用域相同，但前者还包括在应用相应组筛选器之后嵌套到的目标单元的行组和列组成员身份。 有关作用域的详细信息，请参阅[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 以下列表说明了以下 Tablix 区域中的单元的作用域：  
  
-   **Tablix 角** 作用域是在应用数据集和外部 Tablix 的筛选器和排序表达式之后链接到 Tablix 数据区域的数据区域中的数据。  
  
-   **Tablix 列组** 在应用数据集、外部 Tablix 和列组的筛选器和排序表达式之后，最内部列组中的数据。  
  
-   **Tablix 行组** 在应用数据集、外部 Tablix 和行组的筛选器和排序表达式之后，最内部行组中的数据。  
  
-   **Tablix 正文** 在应用数据集、外部 Tablix 以及行组和列组的筛选器和排序表达式之后，由行组和列组的交集表示的最内部组中的数据。  
  
 有关详细信息，请参阅 [Tablix 数据区域（报表生成器和 SSRS）](tablix-data-region-areas-report-builder-and-ssrs.md)。  
  
## <a name="nesting-a-chart-sparkline-or-data-bar-in-a-tablix"></a>在 Tablix 中嵌套图表、迷你图或数据条  
 将图表（包括迷你图或数据条）添加到 Tablix 列组头行或组尾行时，或者添加到 Tablix 正文单元时，传递到该图表的数据的作用域为该单元的数据子集。 默认情况下，将图表添加到 Tablix 单元时，将展开图表维度以填充该单元。  
  
> [!NOTE]  
>  若要更好地控制 Tablix 单元中的图表大小，请首先将该图表添加到一个矩形，然后再将该矩形添加到 Tablix 单元。  
  
 默认情况下，图表图例颜色由图表序列中的数据点颜色来确定。 若要控制颜色以使嵌套图表数据区域针对同一数据类别全部使用相同颜色，必须对数据使用自定义颜色并设置排序表达式。 有关详细信息，请参阅[对多个形状图指定一致的颜色（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)和[对数据区域中的数据进行排序（报表生成器和 SSRS）](sort-data-in-a-data-region-report-builder-and-ssrs.md)。  
  
## <a name="nesting-a-gauge-or-an-indicator-in-a-tablix"></a>在 Tablix 中嵌套仪表或指示器  
 可以在表、矩阵或列表中嵌套仪表或指示器，以便显示关键绩效指标 (KPI)。 将仪表或指示器放置到表内部时，将为 Tablix 中的每个行呈现一个仪表或指示器。 有关向 Tablix 中添加指示器的详细信息，请参阅[指示器（报表生成器和 SSRS）](indicators-report-builder-and-ssrs.md)。  
  
### <a name="adding-a-gauge-to-a-tablix"></a>向 Tablix 中添加仪表  
 可以通过两种方式向 Tablix 数据区域添加仪表：  
  
-   单击 Tablix 单元内的区域并插入仪表。 此时将显示 **“选择仪表类型”** 对话框。 选择仪表类型之后，仪表数据区域则被放置到选定的 Tablix 单元内。 您可能需要调整 Tablix 大小以设置仪表格式。  
  
-   单击表外部区域并插入仪表。 此时将显示 **“选择仪表类型”** 对话框。 选择仪表类型之后，仪表数据区域则被放置到报表的左上角。 在添加数据并设置此仪表的格式之后，请将其拖放到 Tablix 单元内部。  
  
 与图表类似，传递到仪表的数据集的作用域为该单元的数据子集。 将仪表放置到 Tablix 单元内部时，该仪表将始终仅聚合一行数据。  
  
 如果 Tablix 中的数据包含分组，则嵌套在 Tablix 内部的仪表数据区域不会自动继承此组。 您必须向仪表中添加匹配的组表达式才能显示 Tablix 上的相同信息。 例如，如果 Tablix 中的数据按产品分组，则必须向仪表中添加产品组表达式以显示相同数据。 有关详细信息，请参阅[仪表（报表生成器和 SSRS）](gauges-report-builder-and-ssrs.md)和[在数据区域添加或删除组（报表生成器和 SSRS）](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
 必须设置仪表刻度上将显示的最小值和最大值。 若要指定仪表的最大值，可以使用表达式，例如 `=Max!MyField.Value`。 但是，由于此表达式仅在单元数据的作用域内计算，因此，Tablix 中所有行的各仪表的最大值将各不相同。 这样，可能很难理解对 Tablix 中各仪表之间的比较。 或者，还可以为最大值指定静态值。 Tablix 中的所有行均将显示具有此最大值的仪表。 有关详细信息，请参阅[设置仪表的最小值或最大值（报表生成器和 SSRS）](set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)。  
  
 如果仪表上的数据太大，请考虑使用刻度乘数减少显示的数字量。 若要指定乘数，可以右键单击刻度并选择“刻度属性”。 打开 **“刻度属性”** 对话框时，指定 **“乘数”** 的值。  
  
## <a name="nesting-a-table-or-matrix-and-a-chart-in-a-list"></a>在列表中嵌套表/矩阵和图表  
 若要在列表中嵌套多个数据区域，请首先添加一个矩形，然后将数据区域添加到该矩形中。  
  
 您可以为列表数据区域定义组，然后添加 Tablix 和图表以提供同一数据的不同视图。 为此，必须为嵌入的 Tablix 和图表定义相同的组和排序表达式。 根据定义，Tablix 和图表使用父列表数据区域的数据集中的数据。  
  
> [!NOTE]  
>  默认情况下，将列表数据区域添加到设计图面时，列表包括详细信息行。 通过添加组行和删除详细信息行可以更改该默认设置。 有关详细信息，请参阅[利用 Tablix 数据区域的灵活性（报表生成器和 SSRS）](exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)。  
  
 有关详细信息，请参阅[了解组（报表生成器和 SSRS）](understanding-groups-report-builder-and-ssrs.md)和[添加、移动或删除表、矩阵或列表（报表生成器和 SSRS）](add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)   
 [仪表（报表生成器和 SSRS）](gauges-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [设置报表项的格式（报表生成器和 SSRS）](formatting-report-items-report-builder-and-ssrs.md)   
 [教程：向报表添加 KPI&#40;报表生成器&#41;](../tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [设置仪表上刻度的格式（报表生成器和 SSRS）](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)  
  
  
