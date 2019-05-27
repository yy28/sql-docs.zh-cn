---
title: 更改地图图例、 色阶和关联的规则 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shared.maprulesdistribution.f1
- "10512"
- "10539"
- "10533"
- sql12.rtp.rptdesigner.mappointlayerproperties.typerules.f1
- "10534"
- sql12.rtp.rptdesigner.maplegendproperties.general.f1
- sql12.rtp.rptdesigner.mapdistancescaleproperties.general.f1
- "10516"
- sql12.rtp.rptdesigner.mapcolorscaleproperties.labels.f1
- sql12.rtp.rptdesigner.maplegendtitleproperties.general.f1
- "10514"
- sql12.rtp.rptdesigner.shared.mapruleslegend.f1
- sql12.rtp.rptdesigner.mapcolorscaleproperties.general.f1
- sql12.rtp.rptdesigner.shared.embeddedlabels.f1
- "10513"
- sql12.rtp.rptdesigner.mappointlayerproperties.sizerules.f1
- sql12.rtp.rptdesigner.mapcolorscaletitleproperties.general.f1
- "10510"
- "10509"
- "10540"
- "10517"
ms.assetid: a1d691b2-c5ae-420f-af60-b7c54a7385a4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 35ea86d2e03c903736a5900da3da5c10986a3f9f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106359"
---
# <a name="change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs"></a>更改地图图例、色阶和关联的规则（报表生成器和 SSRS）
  地图中可以包含地图图例、色阶和距离刻度。 地图的这些部分可帮助用户解释地图上的数据可视化。  
  
 图例包括地图的以下各部分：  
  
-   **地图图例** 显示的指导帮助解释可改变地图元素在地图层上的显示的分析数据。 一个地图可以具有多个图例。 对于每一地图层，您可以指定要使用的图例。 一个图例可以为多个地图层提供指导。  
  
-   **色阶** 显示的指导帮助解释地图上的颜色。 一个地图有一个色阶。 多个层可以为色阶提供数据。  
  
-   **距离刻度** 显示的指导帮助解释地图的刻度。 一个地图有一个距离刻度。 当前地图视区缩放值确定距离刻度。  
  
 ![rs_MapElements](../media/rs-mapelements.gif "rs_MapElements")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Viewport"></a> 更改图例相对于视区的位置  
  
#### <a name="to-change-the-position-of-a-legend-relative-to-the-viewport"></a>更改图例相对于视区的位置  
  
1.  在设计视图中，右键单击图例并打开_\<报表项->_**属性**页。  
  
2.  在 **“位置”** 中，通过单击指定图例要在视区中显示的相对位置。  
  
3.  若要在视区之外显示图例，请选择“在视区外显示\<报表项>”。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  在预览中，仅当有来自与该图例相关的规则的结果时，才显示地图图例和色阶。 如果没有要显示的项，则图例不出现在呈现的报表中。  
  
  
  
##  <a name="MapLegend"></a> 更改地图图例的布局  
  
#### <a name="to-change-the-layout-of-a-map-legend"></a>更改地图图例的布局  
  
1.  在“设计”视图中，右键单击图例并打开“图例属性”页。  
  
2.  在 **“图例布局”** 中，单击要用于图例的表布局。 当您单击不同的选项时，设计图面上的布局将发生变化。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="MapLegendTitle"></a> 显示或隐藏地图图例标题  
  
#### <a name="to-show-or-hide-a-map-legend-title"></a>显示或隐藏地图图例标题  
  
-   右键单击设计图面上的地图图例，然后单击“显示图例标题”。  
  
  
  
##  <a name="ColorScaleTitle"></a> 显示或隐藏色阶标题  
  
#### <a name="to-show-or-hide-a-color-scale-title"></a>显示或隐藏色阶标题  
  
-   右键单击设计图面上的色阶，然后单击“显示色阶标题”。  
  
  
  
##  <a name="MoveItems"></a> 将项目移出第一个图例  
 根据需要创建任意数量的附加图例，然后更新每一地图层的规则，以指定要在其中显示规则结果的图例。  
  
#### <a name="to-create-a-new-legend"></a>创建新图例  
  
-   在“设计”视图中，在地图视区之外右键单击地图，然后单击“添加图例”。  
  
     一个新的图例将出现在地图上。  
  
#### <a name="to-display-rule-results-in-a-legend"></a>在图例中显示规则结果  
  
1.  在“设计”视图中，单击地图直到出现“地图”窗格。  
  
2.  右键单击具有您希望，然后单击的数据的层_\<地图元素类型\>_**颜色规则**。  
  
3.  单击 **“图例”**。  
  
4.  在“在此图例中显示”下拉列表中，单击要将规则结果显示在其中的图例的名称。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="TemplateStyle"></a> 基于模板样式改变地图元素颜色  
  
#### <a name="to-vary-map-element-colors-based-on-a-template-style"></a>基于模板样式改变地图元素颜色  
  
1.  在“设计”视图中，单击地图直到出现“地图”窗格。  
  
2.  右键单击具有您希望，然后单击的数据的层_\<地图元素类型\>_**颜色规则**。  
  
3.  单击 **“应用模板样式”**。  
  
     模板样式指定字体、边框样式和调色板。 对于在“地图向导”或“地图层向导”中指定的主题，从调色板中为每个地图元素分配一种不同的颜色。 这是适用于不具备关联分析数据的层的唯一选项。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="ColorPalette"></a> 基于调色板改变地图元素颜色  
  
#### <a name="to-vary-map-element-colors-based-on-color-palette"></a>基于调色板改变地图元素颜色  
  
1.  在“设计”视图中，单击地图直到出现“地图”窗格。  
  
2.  右键单击层，具有数据，然后单击_\<地图元素类型\>_**颜色规则**。  
  
3.  单击 **“使用调色板实现数据的可视化效果”**。  
  
     此选项使用内置调色板或您指定的自定义调色板。 根据相关的分析数据，将从调色板中为每个地图元素分配不同的颜色或颜色阴影。  
  
4.  在 **“数据字段”** 中，键入某个字段的名称，该字段包含要通过颜色实现可视化效果的分析数据。  
  
5.  在“调色板”中，从下拉列表选择要使用的调色板的名称。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="ColorRanges"></a> 基于颜色范围改变地图元素颜色  
  
#### <a name="to-vary-map-element-colors-based-on-color-ranges"></a>基于颜色范围改变地图元素颜色  
  
1.  在“设计”视图中，单击地图直到出现“地图”窗格。  
  
2.  右键单击层，具有数据，然后单击_\<地图元素类型\>_**颜色规则**。  
  
3.  单击 **“使用颜色范围实现数据的可视化效果”**。  
  
     此选项结合您在此页上指定的开始颜色、中间颜色和结束颜色以及您在 **“分布”** 页上指定的选项，将相关的分析数据划分到各个范围。 报表处理器将根据每个地图元素的关联数据及其归入的范围，向其分配适当的颜色。  
  
4.  在 **“数据字段”** 中，键入某个字段的名称，该字段包含要通过颜色实现可视化效果的分析数据。  
  
5.  在 **“开始颜色”** 中，指定要用于最低范围的颜色。  
  
6.  在 **“中间颜色”** 中，指定要用于中间范围的颜色。  
  
7.  在 **“结束颜色”** 中，指定要用于最高范围的颜色。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="CustomColors"></a> 基于自定义颜色改变地图元素颜色  
  
#### <a name="to-vary-map-element-colors-based-on-custom-colors"></a>基于自定义颜色改变地图元素颜色  
  
1.  在“设计”视图中，单击地图直到出现“地图”窗格。  
  
2.  右键单击层，具有数据，然后单击_\<地图元素类型\>_**颜色规则**。  
  
3.  单击 **“使用自定义颜色实现数据的可视化效果”**。  
  
     此选项使用您指定的颜色列表。 根据相关的分析数据，将从该列表中为每个地图元素分配一种颜色。 如果地图元素数多于颜色数，则不分配颜色。  
  
4.  在 **“数据字段”** 中，键入某个字段的名称，该字段包含要通过颜色实现可视化效果的分析数据。  
  
5.  在 **“自定义颜色”** 中，单击 **“添加”** 以指定每种自定义颜色。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="DistributionOptions"></a> 为图例设置分布选项  
  
#### <a name="to-set-distribution-options-for-a-legend"></a>为图例设置分布选项  
  
1.  在“设计”视图中，单击地图直到出现“地图”窗格。  
  
2.  右键单击层，具有数据，然后单击_\<地图元素类型\>_**颜色规则**。  
  
3.  选择**实现数据的使用可视化效果**\<规则类型\>选项。 若要使用分布选项，必须根据与层关联的分析数据，在 **“分布”** 页上创建范围。  
  
4.  单击 **“分布”**。  
  
5.  请选择以下分布类型之一：  
  
    -   **相等间隔**： 指定将数据划分为相等范围间隔的范围。  
  
    -   **相等分布**： 指定用于划分数据以使每个范围具有相同项数的范围。  
  
    -   **最佳**： 指定自动调整分布以创建平衡子范围的范围。  
  
    -   **自定义**： 指定您自己的范围数以控制值的分布。  
  
     有关分布选项的详细信息，请参阅[按规则和分析数据更改多边形、线条和点的显示方式（报表生成器和 SSRS）](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)。  
  
6.  在 **“子范围的数目”** 中，键入要使用的子范围数。 当分布类型为 **“最佳”** 时，将自动计算子范围的数量。  
  
7.  在 **“范围开始”** 中，键入最小范围值。 所有小于此数字的值均与范围最小值相同。  
  
8.  在 **“范围结束”** 中，键入最大范围值。 所有大于此数字的值均与范围最大值相同。  
  
9. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="RuleLegend"></a> 更改规则图例的内容  
  
#### <a name="to-change-the-contents-of-a-color-size-width-or-marker-type-legend"></a>更改颜色、大小、宽度或标记类型图例的内容  
  
1.  在“设计”视图中，单击地图直到出现“地图”窗格。  
  
2.  右键单击层，具有数据，然后单击_\<地图元素类型\>_**规则**。  
  
3.  验证是否选中了“使用\<规则类型>实现数据的可视化效果”。  
  
4.  在 **“数据字段”** 中，验证选择了您要该层上实现可视化的分析数据。  
  
    > [!NOTE]  
    >  如果下拉列表中没有显示任何字段，则右键单击该层，然后单击“层数据”以打开“地图层数据属性”对话框的“分析数据”页，并验证你已为此层指定了分析数据。  
  
5.  单击 **“图例”**。  
  
6.  在 **“在此图例中显示”** 中，选择要用于显示规则结果的地图图例。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="ColorScale"></a> 更改色阶的内容  
  
#### <a name="to-change-the-contents-of-the-color-scale-or-a-color-legend"></a>更改色阶或颜色图例的内容  
  
1.  在“设计”视图中，单击地图直到出现“地图”窗格。  
  
2.  右键单击层，具有数据，然后单击_\<地图元素类型\>_**颜色规则**。  
  
3.  选择要使用的颜色规则选项。 若要在地图图例或色阶中显示项，必须选择“\<使用规则类型>实现数据的可视化效果”选项之一。  
  
4.  在 **“数据字段”** 中，验证选择了您要该层上实现可视化的分析数据。  
  
    > [!NOTE]  
    >  如果下拉列表中没有显示任何字段，则右键单击该层，然后单击“层数据”以打开“地图层数据属性”对话框的“分析数据”页，并验证你已为此层指定了分析数据。  
  
5.  单击 **“图例”**。  
  
6.  在 **“色阶选项”** 中，选择 **“在色阶中显示”** 以便在色阶中显示规则结果。 您可以为多个颜色规则指定此选项。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="HideItems"></a> 从图例中删除所有项目  
  
#### <a name="to-hide-items-based-on-a-rule"></a>基于规则隐藏项目  
  
1.  在“设计”视图中，单击地图直到出现“地图”窗格。  
  
2.  右键单击层，具有数据，然后单击_\<地图元素类型\>_**规则**。  
  
3.  单击 **“图例”**。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="ChangeFormatItems"></a> 更改图例中内容的格式  
 为与地图图例关联的规则设置图例选项。  
  
#### <a name="to-change-the-format-of-content-in-a-legend"></a>更改图例中内容的格式  
  
1.  在“设计”视图中，单击地图直到出现“地图”窗格。  
  
2.  右键单击层，具有数据，然后单击_\<地图元素类型\>_**规则**。  
  
3.  单击 **“图例”**。  
  
4.  **“图例文本”** 显示指定要在图例中显示的数据的关键字。 使用地图关键字和自定义格式可帮助控制图例文本的格式。 例如，#FROMVALUE {C2} 指定一个具有两个小数位的货币格式。 有关详细信息，请参阅 [按规则和分析数据更改多边形、线条和点的显示方式（报表生成器和 SSRS）](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
## <a name="see-also"></a>请参阅  
 [地图（报表生成器和 SSRS）](maps-report-builder-and-ssrs.md)   
 [添加、更改或删除地图或地图层（报表生成器和 SSRS）](add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [自定义地图或地图层的数据和显示（报表生成器和 SSRS）](customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [报表故障排除：映射报表（报表生成器和 SSRS）](troubleshoot-reports-map-reports-report-builder-and-ssrs.md)   
 [地图向导和地图层向导（报表生成器和 SSRS）](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  
