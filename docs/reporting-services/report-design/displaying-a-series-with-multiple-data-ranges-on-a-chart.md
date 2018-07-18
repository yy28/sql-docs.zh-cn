---
title: 在图表中显示包含多个数据区域的序列 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 45da3d39-278e-4760-a4b3-9932c9547cf2
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f3ba9d32e9a6183ae3d7eccb9ab6cd19cc4fa1a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33022504"
---
# <a name="displaying-a-series-with-multiple-data-ranges-on-a-chart"></a>在图表中显示包含多个数据区域的序列

  图表将使用序列中的最小值和最大值计算轴刻度。 图表中的序列包含多个数据区域时，数据点将会变得模糊，在图表中只能轻松地看到少量数据点。 例如，假设报表显示 30 天内的每日销售总额。  
  
 ![包含多个数据区域的图表](../../reporting-services/report-design/media/rs-multipledatarangeschart.gif "Chart with multiple data ranges")  
  
 对于大多数月份而言，销售量通常介于 10 到 40 之间。 然而，为期一周的市场营销活动促使 4 月初的销售量突然增加。 这次销售数据的变化导致数据点的分布不均匀，从而降低了图表的整体可读性。  
  
 有几种不同的方法可以改善可读性：  
  
-   **启用刻度分隔线**。 如果数据分成了两个或更多数据区域组，则可以使用刻度分隔线来删除各数据区域之间的空白。 刻度分隔线是在绘图区绘制的一个条带，表示序列中高值和低值之间的中断。  
  
-   **筛选出不需要的值**。 如果您具有的数据点使重要数据区域在图表中显示时变得模糊，则可以使用报表筛选器删除不需要的数据点。 有关如何在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中向图表添加筛选器的详细信息，请参阅[添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)。  
  
-   **将每个数据区域绘制为不同的序列，以便进行多序列比较**。 如果具有两个以上数据区域，可以考虑将数据区域分隔为不同的序列。 有关详细信息，请参阅 [图表中的多个序列（报表生成器和 SSRS）](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="displaying-multiple-data-ranges-using-scale-breaks"></a>使用刻度分隔线显示多个数据区域  
 启用刻度分隔线后，图表将计算在整个图表中绘制线条的位置。 在各数据区域之间必须有足够的分隔空间，才能绘制刻度分隔线。 默认情况下，数据区域之间的分隔空间至少占图表总空间的 25% 时，才能添加刻度分隔线。  
  
 ![具有刻度分隔线的图表](../../reporting-services/report-design/media/rs-multipledatarangeschart-scalebreak.gif "Chart with scale break")  
  
> [!NOTE]  
>  您不能指定在图表中放置刻度分隔线的位置。 但是，可以修改刻度分隔线的计算方式，这将在本主题的后面部分进行介绍。  
  
 如果启用了刻度分隔线，但是它并未显示（即使数据区域之间有足够的分隔空间），则可以将 CollapsibleSpaceThreshold 属性设置为小于 25 的值。 CollapsibleSpaceThreshold 可指定数据区域间所需的可折叠空间的百分比。 有关详细信息，请参阅[向图表添加刻度分隔线（报表生成器和 SSRS）](../../reporting-services/report-design/add-scale-breaks-to-a-chart-report-builder-and-ssrs.md)。  
  
 图表支持每个图表中最多包含 5 条刻度分隔线；但是，显示多条刻度分隔线会使报表不可读。 如果有两个以上数据区域，可以考虑使用不同方法显示此数据。 有关详细信息，请参阅 [图表中的多个序列（报表生成器和 SSRS）](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="unsupported-scale-break-scenarios"></a>不受支持的刻度分隔线应用场景  
 在下列图表应用场景中不支持刻度分隔线：  
  
-   启用了三维效果的图表。  
  
-   已指定对数值轴。  
  
-   已显式设置值轴的最小值或最大值。  
  
-   图表类型为极坐标图、雷达图、饼图、圆环图、漏斗图、棱锥图或堆积图。  
  
 具有刻度分隔线的图表的示例可用于示例报表。 有关下载此示例报表和其他内容的详细信息，请参阅 [报表生成器和报表设计器示例报表](http://go.microsoft.com/fwlink/?LinkId=198283)。  

## <a name="next-steps"></a>后续步骤

[图表中的多个序列](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md)   
[设置图表的格式](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
[图表中的三维效果、凹凸效果和其他效果](../../reporting-services/report-design/chart-effects-3d-bevel-and-other-report-builder.md)   
[图表](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[“轴属性”对话框 ->“轴选项”](http://msdn.microsoft.com/library/b276e210-7a12-48ae-971b-7dabae51df11)   
[收集饼图上的小切片](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
