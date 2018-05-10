---
title: 按规则和分析数据更改多边形、线条和点的显示方式 | Microsoft Docs
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
f1_keywords:
- "10538"
- "10537"
- sql13.rtp.rptdesigner.mapembeddedpolygonlayerproperties.general.f1
- MICROSOFT.REPORTDESIGNER.MAPMARKER.MARKERSTYLE
- sql13.rtp.rptdesigner.mapembeddedlinelayerproperties.general.f1
- sql13.rtp.rptdesigner.mapembeddedpointlayerproperties.general.f1
- "10531"
- "10536"
- sql13.rtp.rptdesigner.maplinelayerproperties.widthrules.f1
ms.assetid: 7f1f5584-37b4-4fa2-ae44-8988c5f0c744
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3e78b0319639852d8bb4cac5be3f3b2157ac0703
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="vary-polygon-line-and-point-display-by-rules-and-analytical-data"></a>按规则和分析数据更改多边形、线条和点的显示方式
  通过设置层的选项、设置层上地图元素的规则或覆盖层上特定嵌入地图元素的选项来控制地图层上多边形、线条和点的显示选项。  
  
 将按特定的优先级顺序应用显示选项（按优先级从低到高的顺序列出）：  
  
1.  在多边形层、线条层和点层上设置的选项应用于该层上的所有地图元素，无论地图元素是否嵌入到报表定义中。  
  
2.  为规则设置的选项应用于层上的所有地图元素。 所有数据可视化选项仅应用于与空间数据关联的地图元素。 数据可视化选项要求您指定不同显示方式所基于的数据字段。 必须首先设置分析数据和空间数据的匹配字段，然后才能应用数据可视化规则。 有关详细信息，请参阅[地图（报表生成器和 SSRS）](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)。  
  
3.  为所选的嵌入地图元素设置的选项。 请注意，覆盖层选项时，您对报表定义所做的更改是永久性的。 可以更改数据字段值和覆盖显示选项，以自定义层上多边形、线条和点的特定显示方式。  
  
 除了控制层上地图元素的显示方式之外，还可以控制层的透明度以允许穿过后来绘制的层显示先前绘制的层。 有关更改对地图或整个地图层有影响的选项的详细信息，请参阅[自定义地图或地图层的数据和显示（报表生成器和 SSRS）](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Rules"></a> 了解规则  
 可以设置四种规则类型，以允许报表处理器自动调整层上地图元素的显示属性。 地图元素类型（多边性、线条或点）不同，规则也将随之不同。  
  
-   **多边形：** 改变多边形颜色。  
  
    -   **多边形中心点。** 对于在每个多边形的中心点显示的标记，改变标记颜色、标记大小和标记类型。  
  
-   **线条：** 改变线条颜色和线条宽度。  
  
-   **点：** 对于为每个点显示的标记，改变标记颜色、标记大小和标记类型。  
  
##  <a name="Color"></a> 了解颜色规则  
 颜色规则应用于多边形、线条和表示点或多边形中心点的标记的填充颜色。  
  
 颜色规则支持四个选项：  
  
-   应用模板样式： 在向导中选择的主题定义层的模板样式。 主题设置字体样式、边框样式和调色板。  
  
-   使用调色板实现数据的可视化效果： 通过名称指定调色板。 报表处理器通过分步调试调色板中的每种颜色，然后应用调色板中每种颜色的后续较淡阴影来设置层中每个地图元素的颜色。  
  
-   使用颜色范围实现数据的可视化效果： 指定开始颜色、中间颜色和结束颜色， 然后指定分布选项。 报表处理器使用分布选项值来创建生成与热度地图类似显示方式的一组颜色。 热度地图显示与温度有关的颜色。 例如，刻度为 0 到 100 时，低值是蓝色的，表示冷，高值是红色的，表示热。  
  
-   使用自定义颜色实现数据的可视化效果： 指定一组颜色。 报表处理器通过分步调试您指定的值，设置层中每个地图元素的颜色。  
  
 默认调色板包括白色。 若要避免白色和调色板中的其他颜色对比强烈，请在调色板中指定一种淡颜色作为开始颜色。  
  
 若要将不与数据关联的地图元素显示为无颜色，请为层上的地图元素的默认颜色设置 **“无颜色”** 。  
  
### <a name="color-scale"></a>色阶  
 默认情况下，所有颜色规则值除了显示在第一个图例中，还显示在色阶中。 色阶设计用于显示一个颜色范围。 选择将最重要的数据显示在色阶中。  
  
 若要使某些值不显示在色阶中，请清除每层上每个颜色规则的色阶选项。  
  
##  <a name="Width"></a> 了解线条宽度规则  
 宽度规则应用于线条。 宽度规则支持二个选项：  
  
-   使用默认线条宽度： 指定线条宽度（磅）。  
  
-   使用线条宽度实现数据的可视化效果： 设置线条的最小和最大宽度，指定要用于改变宽度的数据字段，然后指定要应用于该数据的分布选项。  
  
##  <a name="Size"></a> 了解标记大小规则  
 大小规则应用于表示点或多边形中心点的标记。 大小规则支持二个选项：  
  
-   使用默认标记大小： 指定大小（磅）。  
  
-   使用大小实现数据的可视化效果： 设置标记的最小和最大大小，指定要用于改变大小的数据字段，然后指定要应用于该数据的分布选项。  
  
##  <a name="Marker"></a> 了解标记类型规则  
 标记类型规则应用于表示点或多边形中心点的标记。 标记类型规则支持二个选项：  
  
-   使用默认标记类型： 指定可用标记类型之一。  
  
-   使用标记实现数据的可视化效果： 指定一组标记并指定它们的使用顺序。 标记类型包括 **Circle**、 **Diamond**、 **Pentagon**、 **PushPin**、 **Rectangle**、 **Star**、 **Triangle**、 **Trapezoid**和 **Wedge**。  
  
##  <a name="Distribution"></a> 了解分布选项  
 若要创建值的分布，可以将数据分成若干范围。 指定分布类型、子范围数以及范围的最小值和最大值。  
  
 在以下列表中，假定你有三个地图元素和六个具有以下值的相关分析值：1、10、200、2000、4777、8999，范围为 1 到 9999。  
  
-   **相等间隔。** 创建将数据划分为相等范围间隔的范围。 例如，三个范围将为 0-2999, 3000-5999, 6000-8999。 子范围 1：1, 10, 200, 500。 子范围 2：4777。 子范围 3：8999。 此方法不考虑数据的分布方式。 很大的值或很小的值会使分布结果扭曲。  
  
-   **相等分布。** 创建用于划分数据以使每个范围具有相同项数的范围。 对于示例数据，三个范围将为 0-10, 11-500, 501-8999。 子范围 1：1、10。 子范围 2：200、500。 子范围 3：4777, 8999。 此方法如果创建跨很大或很小范围的划分，会使分布结果扭曲。  
  
-   **最佳。** 创建自动调整分布以创建平衡子范围的范围。 子范围数由算法决定。  
  
-   **自定义：** 指定您自己的范围数以控制值的分布。 对于示例数据，你可以指定 3 个范围：1-2、3-8、9。  
  
 分布值由规则使用，以改变地图元素显示值。  
  
##  <a name="Legends"></a> 了解图例和图例项  
 自动从您为每个层指定的规则创建图例项。 规则选项控制创建多少个项以及在哪个图例中显示。 默认情况下，所有规则的所有项目都将添加到第一个图例。 若要将项移出第一个图例，请创建所需数目的其他图例，对于每个规则指定要用于显示规则所确定的项的图例。 若要基于规则隐藏项，请指定空白图例名称。  
  
 若要控制图例显示的位置，请使用“图例属性”对话框来指定相对于地图视区的位置。 有关详细信息，请参阅 [更改地图图例、色阶和关联的规则（报表生成器和 SSRS）](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)。  
  
 图例自动展开以显示图例标题或图例文本。 若要设置图例项的文本的格式，请使用地图图例关键字和自定义格式。 有关详细信息，请参阅 [To change the format of content in a legend](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md#ChangeFormatItems)。  
  
 下表显示您可以使用的不同格式的示例：  
  
|关键字和格式|Description|图例中的显示文本示例|  
|------------------------|-----------------|---------------------------------------------------|  
|`#FROMVALUE {C0}`|显示不带小数、带货币符号的总计值|$400|  
|`#FROMVALUE {C2}`|显示带 2 位小数、带货币符号的总计值。|$400.55|  
|`#TOVALUE`|显示数据字段的实际数值。|10000|  
|`#FROMVALUE{N0} - #TOVALUE{N0}`|显示范围开始和范围结束的实际数值。|10 - 790|  
  
## <a name="see-also"></a>另请参阅  
 [更改地图图例、色阶和关联的规则（报表生成器和 SSRS）](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)   
 [地图（报表生成器和 SSRS）](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [地图向导和地图层向导（报表生成器和 SSRS）](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  
