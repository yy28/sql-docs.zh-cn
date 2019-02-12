---
title: 图表中的位置标签（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5db74e0b-8be8-4b47-b386-faab56dffa9b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cfc294f1ae01241dbcabfff954aa42c242f6aad7
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56018229"
---
# <a name="position-labels-in-a-chart-report-builder-and-ssrs"></a>图表中的位置标签（报表生成器和 SSRS）
  由于每种图表类型都具有不同的形状，因此应将数据点标签放在最佳位置上以免对图表产生干扰。 标签的默认位置因图表类型而异：  
  
-   在堆积图中，标签只能位于序列内部。  
  
-   在漏斗图或棱锥图中，标签位于列的外部。  
  
-   在饼图中，标签位于饼图的各切片内部。  
  
-   在条形图中，标签位于表示数据点的图条的外部。  
  
-   在极坐标图中，标签位于表示数据点的圆形区域的外部。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-position-of-point-labels-in-a-pie-chart"></a>更改点标签在饼图中的位置  
  
1.  创建一个饼图。  
  
2.  在设计图面上，右键单击该图表并选择“显示数据标签”。  
  
3.  打开“属性”窗格。 在 **“视图”** 选项卡上，单击 **“属性”**。  
  
4.  在设计图面上，单击该图表。 该图表的属性将显示在“属性”窗格中。  
  
5.  在 **“常规”** 部分，展开 **CustomAttributes** 节点。 此时将显示该饼图的属性列表。  
  
6.  为 PieLabelStyle 属性选择一个值。  
  
### <a name="to-change-the-position-of-point-labels-in-a-funnel-or-pyramid-chart"></a>更改点标签在漏斗图或棱锥图中的位置  
  
1.  创建一个漏斗图或棱锥图。  
  
2.  在设计图面上，右键单击该图表并选择“显示数据标签”。  
  
3.  打开“属性”窗格。 在 **“视图”** 选项卡上，单击 **“属性”**  
  
4.  在设计图面上，单击该图表。 该图表的属性将显示在“属性”窗格中。  
  
5.  在 **“常规”** 部分，展开 **CustomAttributes** 节点。 此时将显示该漏斗图的属性列表。  
  
6.  对于漏斗图，请为 FunnelLabelStyle 属性选择一个值。 对于凌锥图，请为 PyramidLabelStyle 属性选择一个值。  
  
    > [!NOTE]  
    >  当此属性设置为 `OutsideInColumn` 值时，标签会绘制在垂直图柱中。 列的位置无法更改。  
  
### <a name="to-change-the-position-of-point-labels-in-a-bar-chart"></a>更改点标签在条形图中的位置  
  
1.  创建一个条形图。  
  
2.  在设计图面上，右键单击该图表并选择“显示数据标签”。  
  
3.  打开“属性”窗格。 在 **“视图”** 选项卡上，单击 **“属性”**  
  
4.  在设计图面上，单击该图表。 该图表的属性将显示在“属性”窗格中。  
  
5.  在 **“常规”** 部分，展开 **CustomAttributes** 节点。 此时将显示该条形图的属性列表。  
  
6.  为 BarLabelStyle 属性选择一个值。  
  
 当条形图标签样式设置为 `Outside` 时，只要图表区放得下，标签就将位于图条的外部。 如果标签在图表区内图条以外的区域放不下，则标签将位于最靠近图条末尾的图条内。  
  
### <a name="to-change-the-position-of-point-labels-in-an-area-column-line-or-scatter-chart"></a>更改点标签在面积图、柱形图、折线图或散点图中的位置  
  
1.  创建一个面积图、柱形图、折线图或散点图。  
  
2.  在设计图面上，右键单击该图表并选择“显示数据标签”。  
  
3.  打开“属性”窗格。 在 **“视图”** 选项卡上，单击 **“属性”**  
  
4.  在设计图面上，单击序列。 序列的属性将显示在“属性”窗格中。  
  
5.  在“数据”  部分中，展开 **DataPoint** 节点，然后展开 **Label**节点。  
  
6.  为 Position 属性选择一个值。  
  
## <a name="see-also"></a>请参阅  
 [饼图（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)   
 [条形图（报表生成器和 SSRS）](bar-charts-report-builder-and-ssrs.md)   
 [设置图表上轴标签的格式（报表生成器和 SSRS）](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [将轴标签的格式设置为日期或货币（报表生成器和 SSRS）](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [在饼图外显示数据点标签（报表生成器和 SSRS）](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [设置图表上数据点的格式（报表生成器和 SSRS）](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
  
  
