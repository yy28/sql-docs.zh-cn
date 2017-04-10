---
title: "向图表添加凹凸效果、阳文和纹理样式（报表生成器和 SSRS） | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 737cfc80-b39e-497c-817b-b46693deb58f
caps.latest.revision: 6
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# 向图表添加凹凸效果、阳文和纹理样式（报表生成器和 SSRS）
  当使用某些图表类型时，您可以指定绘制样式以增加图表的视觉效果。 这些绘制效果仅适用于图表的序列。 它们对其他图表元素不起任何作用。  
  
 当使用的是饼图或圆环图的任何变体时，可以指定软边或凹陷绘制样式，这类似于可应用到图像的凹凸效果或阳文效果。  
  
 当使用的是条形图或柱状图的任何变体时，可以对各个图条或图柱应用纹理样式，例如柱状、楔形和亮转暗。  
  
 除了上述绘制样式外，还可以向许多图表元素添加边框和阴影，以制造一种具有深度的错觉。 有关设置图表格式的其它方法的详细信息，请参阅[设置图表格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### 向饼图或圆环图添加凹凸效果或阳文样式  
  
1.  在 **“视图”** 选项卡上，选择 **“属性”** 以打开“属性”窗格。  
  
2.  选择要增强的饼图或圆环图。 选择图表中的一个数据字段，而不是整个图表。  
  
3.  在“属性”窗格中，展开 **CustomAttributes** 节点。  
  
4.  对于 PieDrawingStyle，从下拉列表中选择一种样式。  
  
> [!NOTE]  
>  不能在同一个图表上具有三维和凹凸效果或阳文样式。 如果已为图表启用三维样式，将看不到 PieDrawingStyle 属性。  
  
 ![带有凹焊缝绘制样式的饼图](../../reporting-services/report-design/media/rs-piedrawingeffects-concave.png "带有凹焊缝绘制样式的饼图")  
  
### 向条形图或柱状图中添加纹理样式  
  
1.  选择要增强的条形图或柱状图。 选择图表中的一个数据字段，而不是整个图表。  
  
2.  打开“属性”窗格。  
  
3.  展开 **CustomAttributes** 节点。  
  
4.  对于 DrawingStyle，从下拉列表中选择一种样式。  
  
> [!NOTE]  
>  不能在同一个图表上具有三维和凹凸效果或阳文样式。 如果已为图表启用三维样式，将看不到 PieDrawingStyle 属性。  
  
 ![具有 LightToDark 绘制效果的条形图](../../reporting-services/report-design/media/rs-bardrawingeffects-lighttodark.gif "具有 LightToDark 绘制效果的条形图")  
  
## 另请参阅  
 [条形图（报表生成器和 SSRS）](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [柱形图（报表生成器和 SSRS）](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)   
 [饼图（报表生成器和 SSRS）](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [设置图表格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)  
  
  