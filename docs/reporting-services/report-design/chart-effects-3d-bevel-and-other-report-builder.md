---
title: "图表中的三维效果、凹凸效果和其他效果（报表生成器和 SSRS）| Microsoft Docs"
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
f1_keywords: "10156"
ms.assetid: 18ef2119-2931-43ae-9078-f39b460462dd
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 90e2cfecc2090f5d09ac1a7a5fce1e6b4cbcca81
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="chart-effects---3d-bevel-and-other-report-builder"></a>图表效果 - 三维效果、凹凸效果和其他效果（报表生成器）
  三维 (3D) 效果可以使 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中的图表更具深度感并增强视觉效果。 例如，若要强调分离型饼图的某个特定切片，可以旋转并更改图表的透视，以便人们可以首先注意到该切片。 将三维效果应用于图表时，将会禁用所有渐变颜色和阴影类型。  
  
 可以将三维效果应用于单个图表，还可以在同一报表中同时显示二维和三维图表。  
  
 对于所有的图表类型，你都可以通过在“图表区属性”对话框中选择“启用三维”，将三维效果应用到图表区。 有关详细信息，请参阅 [向图表添加三维效果（报表生成器和 SSRS）](../../reporting-services/report-design/chart-effects-add-3d-effects-report-builder.md)。  
  
 为图表增添视觉影响的另外一种方法是在条形图、柱形图、饼图和圆环图中添加凹凸效果、阳文和纹理样式。 有关详细信息，请参阅[向图表添加凹凸效果、阳文和纹理样式（报表生成器和 SSRS）](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="coordinate-based-three-dimensional-charts"></a>基于坐标的三维图表  
 使用基于坐标的图表类型（柱形图、条形图、面积图、点状图、折线图和范围图）时，三维效果显示的图表具有第三条坐标轴，称为“Z 轴”。 通过引入第三条坐标轴，可以使您在图表中应用各种视觉增强效果。  
  
### <a name="changing-the-white-space-in-a-3d-chart"></a>更改三维图表中的空格  
 在三维模式下显示图表区时，每个序列都会沿图表的 Z 轴显示在单独的行中。 若要更改每个序列之间的空格量，可通过更改“三维效果”对话框中的 **“点间隙深度”** 属性来修改图表的点间隙深度。  
  
### <a name="changing-the-projection-of-a-3d-chart"></a>更改三维图表的投影  
 有两种类型的三维投影：倾斜和透视。 图表的倾斜投影可以增加二维图表的深度维度。 绘制的 Z 轴与水平轴和垂直轴的角度是相等的，这三根轴像在二维图表中一样彼此保持垂直。  
  
 透视投影可以通过估计一个视图平面，然后如同从该点查看图表那样重新绘制图表，来对该图表进行转换。 **“旋转”** 值将视图沿垂直方向从地平面 0 度移动到高于地平面 90 度。 **“倾角”** 值将视角向左或向右移动。 如果该值为 0，则相当于二维视图的图表。 **“透视”** 值定义显示投影时使用的失真百分比。 此类投影可以保持图表的比例，但图表的外观会显得失真，所以使用低角度透视是最有效的方法。  
  
> [!NOTE]  
>  倾斜和透视投影是单独的投影类型，所以它们不能在同一个图表中同时使用。  
  
### <a name="clustering-data"></a>聚类分析数据  
 在二维图表中，多个序列的数据并行显示。 聚类分析将每个序列分别显示在三维图表的单独行中。 例如，如果您的图表包含三个序列的数据点，聚类分析会将每个序列沿 Z 轴显示在单独的行中。 默认情况下，会聚集所有以三维形式显示的图表类型。  
  
 可以在条形图和柱形图中禁用聚类分析。 禁用聚类分析时，会在同一行中并行显示多个条形和柱形序列。  
  
## <a name="shape-based-three-dimensional-charts"></a>基于形状的三维图表  
 基于形状的图表类型（饼图、圆环图、漏斗图、棱锥图）可用的三维效果较少。 在使用基于形状的图表类型时，您只能更改旋转值和倾角值。  
  
## <a name="rotations"></a>旋转  
 图表可以从 -90 到 90 度进行水平和垂直旋转。 水平的正角会将图表沿 X 轴逆时针旋转，而垂直的正角则会将图表沿 Y 轴顺时针旋转。  
  
## <a name="highlighting-3d-effects"></a>突出显示三维效果  
 选择图表区时，您可以通过在“属性”窗格中 Area3Dstyle 下出现的 **“明暗度”** 属性，为三维图表添加突出显示样式。 简单的照明样式会对图表区元素应用相同的色调。 真实样式会根据指定的照明角度，更改图表区元素的色调。  
  
## <a name="see-also"></a>另请参阅  
 [设置图表上轴标签的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [设置图表格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [向图表添加三维效果（报表生成器和 SSRS）](../../reporting-services/report-design/chart-effects-add-3d-effects-report-builder.md)  
  
  
