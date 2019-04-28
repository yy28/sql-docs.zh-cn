---
title: 设置图表格式（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10214"
- sql12.rtp.rptdesigner.calculatedseriesproperties.fill.f1
- sql12.rtp.rptdesigner.serieslabelproperties.fill.f1
- sql12.rtp.rptdesigner.legendproperties.fill.f1
- "10149"
- sql12.rtp.rptdesigner.seriesproperties.shadow.f1
- sql12.rtp.rptdesigner.seriesproperties.markers.f1
- "10255"
- sql12.rtp.rptdesigner.charttitleproperties.fill.f1
- "10154"
- "10170"
- "10173"
- sql12.rtp.rptdesigner.seriesproperties.fill.f1
- "10169"
- "10158"
- sql12.rtp.rptdesigner.chartareaproperties.fill.f1
- sql12.rtp.rptdesigner.charttitleproperties.shadow.f1
- "10246"
- "10150"
- sql12.rtp.rptdesigner.calculatedseriesproperties.borders.f1
- sql12.rtp.rptdesigner.chartproperties.fill.f1
- "10159"
- sql12.rtp.rptdesigner.majorgridlineproperties.gridlineoptions.f1
- "10160"
- sql12.rtp.rptdesigner.serieslabelproperties.font.f1
- "10182"
- "10163"
- "10164"
- "10253"
- "10216"
- "10171"
- "10257"
- sql12.rtp.rptdesigner.chartareaproperties.border.f1
- sql12.rtp.rptdesigner.calculatedseriesproperties.shadow.f1
- sql12.rtp.rptdesigner.chartproperties.border.f1
- sql12.rtp.rptdesigner.minorgridlineproperties.gridlineoptions.f1
- sql12.rtp.rptdesigner.chartareaproperties.shadow.f1
- sql12.rtp.rptdesigner.charttitleproperties.borders.f1
- sql12.rtp.rptdesigner.charttitleproperties.font.f1
- "10247"
ms.assetid: d3984300-c766-42f8-b7c4-863123d67c99
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cea1d745b677bfa67f6847f2b42ed3701914f1e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62654595"
---
# <a name="formatting-a-chart-report-builder-and-ssrs"></a>设置图表格式（报表生成器和 SSRS）
  为图表定义数据并且该图表按预期方式显示之后，您可添加格式设置以改善整体外观效果并突出显示关键数据点。 可以从“属性”对话框修改最常用的格式设置选项，此对话框在右键单击某图表元素以显示其快捷菜单时出现。 每个图表元素都有其相对应的对话框。 有关图表元素的详细信息，请参阅 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)。  
  
 与图表相关的所有属性都位于“属性”窗格中，但是其中许多属性都可以从对话框中进行设置。 如果要对这些序列进行格式设置，可以使用自定义属性指定特定于序列的属性，这些属性只存在于“属性”窗格内的 **CustomAttributes** 属性类别中。  
  
 若要使用最少的步骤有效地设置图表的格式，请更改默认边框样式、调色板和绘制样式。 这三种功能可在图表中产生最大程度的视觉效果变化。 绘制样式只适用于饼图、圆环图、条形图和柱形图。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="in-this-section"></a>本节内容  
 [设置图表上序列颜色的格式（报表生成器和 SSRS）](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)  
 讨论如何使用调色板定义颜色、如何定义自己的调色板，以及如何根据表达式定义颜色。  
  
 [设置图表上轴标签的格式（报表生成器和 SSRS）](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)  
 讨论如何显示网格线、刻度线和标题，以及如何设置轴刻度上数字和日期的格式。  
  
 [设置图表上图例的格式（报表生成器和 SSRS）](chart-legend-formatting-report-builder.md)  
 讨论如何对图表图例中的项进行重新排序和格式设置。  
  
 [设置图表上数据点的格式（报表生成器和 SSRS）](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
 讨论如何放置数据点标签以及如何设置图表中每个序列的数据点标记的格式。  
  
 [图表中的三维效果、凹凸效果和其他效果（报表生成器和 SSRS）](chart-effects-3d-bevel-and-other-report-builder.md)  
 讨论您可以对图表应用的各种三维效果。  
  
 [向图表添加边框（报表生成器和 SSRS）](add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)  
 说明如何向图表添加边框。  
  
## <a name="see-also"></a>请参阅  
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)   
 [向图表添加边框（报表生成器和 SSRS）](add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)   
 [使用调色板定义图表上的颜色（报表生成器和 SSRS）](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [向图表添加凹凸效果、阳文和纹理样式（报表生成器和 SSRS）](chart-effects-add-bevel-emboss-or-texture-report-builder.md)  
  
  
