---
title: "添加凹凸效果、 阳文和纹理样式为图 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 737cfc80-b39e-497c-817b-b46693deb58f
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2081d22c9e0aefd82cda5dff97b8ece503fdd9b0
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="chart-effects---add-bevel-emboss-or-texture-report-builder"></a>图表效果-添加凹凸效果、 阳文和纹理 （报表生成器）
  当使用某些图表类型时，您可以指定绘制样式以增加图表的视觉效果。 这些绘制效果仅适用于图表的序列。 它们对其他图表元素不起任何作用。  
  
 当使用的是饼图或圆环图的任何变体时，可以指定软边或凹陷绘制样式，这类似于可应用到图像的凹凸效果或阳文效果。  
  
 当使用的是条形图或柱状图的任何变体时，可以对各个图条或图柱应用纹理样式，例如柱状、楔形和亮转暗。  
  
 除了上述绘制样式外，还可以向许多图表元素添加边框和阴影，以制造一种具有深度的错觉。 有关设置图表格式的其它方法的详细信息，请参阅 [设置图表格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-bevel-or-emboss-styles-to-a-pie-or-doughnut-chart"></a>向饼图或圆环图添加凹凸效果或阳文样式  
  
1.  在 **“视图”** 选项卡上，选择 **“属性”** 以打开“属性”窗格。  
  
2.  选择要增强的饼图或圆环图。 选择图表中的一个数据字段，而不是整个图表。  
  
3.  在“属性”窗格中，展开 **CustomAttributes** 节点。  
  
4.  对于 PieDrawingStyle，从下拉列表中选择一种样式。  
  
> [!NOTE]  
>  不能在同一个图表上具有三维和凹凸效果或阳文样式。 如果已为图表启用三维样式，将看不到 PieDrawingStyle 属性。  
  
 ![与凹陷绘制样式的饼图](../../reporting-services/report-design/media/rs-piedrawingeffects-concave.gif "凹陷绘制样式与饼形图")  
  
### <a name="to-add-texture-styles-to-a-bar-or-column-chart"></a>向条形图或柱状图中添加纹理样式  
  
1.  选择要增强的条形图或柱状图。 选择图表中的一个数据字段，而不是整个图表。  
  
2.  打开“属性”窗格。  
  
3.  展开 **CustomAttributes** 节点。  
  
4.  对于 DrawingStyle，从下拉列表中选择一种样式。  
  
> [!NOTE]  
>  不能在同一个图表上具有三维和凹凸效果或阳文样式。 如果已为图表启用三维样式，将看不到 PieDrawingStyle 属性。  
  
 ![条形图 LightToDark 绘制效果](../../reporting-services/report-design/media/rs-bardrawingeffects-lighttodark.gif "LightToDark 绘制效果条形图")  
  
## <a name="see-also"></a>另請參閱  
 [条形图（报表生成器和 SSRS）](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [柱形图 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)   
 [饼图 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [格式设置图表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)  
  
  
