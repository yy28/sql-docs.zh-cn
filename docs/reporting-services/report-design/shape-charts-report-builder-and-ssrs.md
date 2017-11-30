---
title: "形状图（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b8404c1-aa89-4350-8bd6-203bc0446ee4
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 21e8493a3a4c471013c5a7e41b600caa61e8238e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="shape-charts-report-builder-and-ssrs"></a>形状图（报表生成器和 SSRS）
  形状图将值数据显示为整体的百分比。 形状图通常用于显示数据集中不同值之间的比例比较结果。 类别由各个形状段来表示。 形状段的大小由值来决定。 形状图与饼图的用法类似，但前者是按从最大到最小的顺序来排列类别。  
  
 漏斗图按逐渐递减的比例来显示值。 漏斗区的大小由序列值在所有值总计中所占的百分比来确定。 例如，您可能使用漏斗图来显示网站访问者的趋势。 漏斗图可能会在顶部显示较宽的区域，表明访问者对主页的点击率；而其他区域将成比例缩小。 有关如何向漏斗图添加数据的详细信息，请参阅 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)。  
  
 下图显示的是漏斗图示例。  
  
 ![漏斗图](../../reporting-services/report-design/media/rs-funnelchart.gif "漏斗图")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>变体  
  
-   **棱锥图**。 棱锥图显示的是成比例数据，以便图表看起来像一个棱锥。  
  
## <a name="data-considerations-for-shape-charts"></a>形状图的数据注意事项  
  
-   形状图的视觉效果较好，因此常用于报表中。 但是，形状图是一种非常简单化的图表类型，可能无法最好地表示数据。 仅当数据聚合成七个数据点或更少数据点时，才考虑使用形状图。 通常，在使用形状图时应当对每个数据区域仅显示一种类别。  
  
-   形状图将每个数据组显示为单独的图表段。 您必须至少添加一个数据字段和一个类别字段。 如果向形状图中添加多个数据字段，则形状图会在同一个图表中显示这些数据字段。  
  
-   形状图最有效的是以排序顺序显示成比例的百分比。 然而，为了保持一致性，图表默认情况下不会对数据集中的值进行排序。 请考虑从高到低对值排序，从而最准确地以漏斗图或棱锥图来表示数据。 有关详细信息，请参阅 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)。  
  
-   当计算比率时，Null 值、空值、负值和零值均无效。 因此，这些值不会显示在形状图中。 若要将这些值类型显示在图表中，需将图表类型更改为除形状图外的其他类型。 有关如何向非形状图添加空点的详细信息，请参阅[向图表添加空点（报表生成器和 SSRS）](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)。  
  
-   若要使用自定义调色板在形状图上定义自己的颜色，请确保调色板中有足够的颜色，从而均用唯一的颜色突出显示各个数据点。 有关详细信息，请参阅 [设置图表上序列颜色的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)。  
  
-   与所有其他图表类型不同的是，形状图将在其图例中显示各个数据点，而不是单个序列。  
  
-   漏斗图将忽略值和类别轴的设置。 如果有多个类别或序列组，则图表图例中将显示组标签。  
  
-   在相同的图表区域中，形状图不能与任何其他图表类型结合使用。 如果必须显示形状图数据与其他类型图表数据之间的比较结果，则需要添加第二个图表区域。  
  
-   您可以在饼图和圆环图中应用其他绘制样式以增加视觉效果。 有关详细信息，请参阅[设置图表上序列颜色的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [设置图表格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [图表中的空点和 Null 数据点（报表生成器和 SSRS）](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [饼图&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
