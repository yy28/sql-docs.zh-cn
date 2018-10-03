---
title: 向图表添加棱台、浮雕和纹理样式（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 737cfc80-b39e-497c-817b-b46693deb58f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 2e6e59b2562928d22a3d9e0b74830d630d77728d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072007"
---
# <a name="add-bevel-emboss-and-texture-styles-to-a-chart-report-builder-and-ssrs"></a>向图表添加凹凸效果、阳文和纹理样式（报表生成器和 SSRS）
  当使用某些图表类型时，您可以指定绘制样式以增加图表的视觉效果。 这些绘制效果仅适用于图表的序列。 它们对其他图表元素不起任何作用。  
  
 当使用的是饼图或圆环图的任何变体时，可以指定软边或凹陷绘制样式，这类似于可应用到图像的凹凸效果或阳文效果。  
  
 当使用的是条形图或柱状图的任何变体时，可以对各个图条或图柱应用纹理样式，例如柱状、楔形和亮转暗。  
  
 除了上述绘制样式外，还可以向许多图表元素添加边框和阴影，以制造一种具有深度的错觉。 设置图表格式的其他方法的详细信息，请参阅[设置图表格式&#40;报表生成器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-bevel-or-emboss-styles-to-a-pie-or-doughnut-chart"></a>向饼图或圆环图添加凹凸效果或阳文样式  
  
1.  在 **“视图”** 选项卡上，选择 **“属性”** 以打开“属性”窗格。  
  
2.  选择要增强的饼图或圆环图。 选择图表中的一个数据字段，而不是整个图表。  
  
3.  在“属性”窗格中，展开 **CustomAttributes** 节点。  
  
4.  对于 PieDrawingStyle，从下拉列表中选择一种样式。  
  
> [!NOTE]  
>  不能在同一个图表上具有三维和凹凸效果或阳文样式。 如果已为图表启用三维样式，将看不到 PieDrawingStyle 属性。  
  
 ![带有凹形绘制样式的饼图](../media/rs-piedrawingeffects-concave.gif "带有凹形绘制样式的饼图")  
  
### <a name="to-add-texture-styles-to-a-bar-or-column-chart"></a>向条形图或柱状图中添加纹理样式  
  
1.  选择要增强的条形图或柱状图。 选择图表中的一个数据字段，而不是整个图表。  
  
2.  打开“属性”窗格。  
  
3.  展开 **CustomAttributes** 节点。  
  
4.  对于 DrawingStyle，从下拉列表中选择一种样式。  
  
> [!NOTE]  
>  不能在同一个图表上具有三维和凹凸效果或阳文样式。 如果已为图表启用三维样式，将看不到 PieDrawingStyle 属性。  
  
 ![具有 LightToDark 绘制效果的条形图](../media/rs-bardrawingeffects-lighttodark.gif "具有 LightToDark 绘制效果的条形图")  
  
## <a name="see-also"></a>请参阅  
 [条形图&#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [柱形图（报表生成器和 SSRS）](column-charts-report-builder-and-ssrs.md)   
 [饼图&#40;报表生成器和 SSRS&#41;](pie-charts-report-builder-and-ssrs.md)   
 [设置图表格式&#40;报表生成器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)  
  
  
