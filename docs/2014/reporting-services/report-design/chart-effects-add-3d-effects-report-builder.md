---
title: 将三维效果添加到图表（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ab9625d8-6557-4a4d-8123-eefa7c066ff5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 07934e74138f17317eb0258e2b3ad0fa6d26254a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106314"
---
# <a name="add-3d-effects-to-a-chart-report-builder-and-ssrs"></a>将三维效果添加到图表（报表生成器和 SSRS）
  三维 (3D) 效果可以使图表具有深度并增强视觉效果。 例如，若要强调分离型饼图的某个特定切片，可以旋转并更改图表的透视，以便人们可以首先注意到该切片。 将三维效果应用于图表时，将会禁用所有渐变颜色和阴影类型。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-apply-3d-effects-to-a-range-area-line-scatter-or-polar-chart"></a>将三维效果应用于范围图、面积图、折线图、散点图或极坐标图  
  
1.  右键单击图表区域的任意位置，然后选择“三维效果”。 随即显示“图表区属性”对话框。   
  
2.  在 **“三维选项”** 中，选择 **“启用三维”** 选项。  
  
3.  （可选）在“三维选项”中，可以设置各种与三维角度和场景选项相关的属性。 有关这些属性的详细信息，请参阅 [图表中的三维效果、凹凸效果和其他效果（报表生成器和 SSRS）](chart-effects-3d-bevel-and-other-report-builder.md)。  
  
4.  单击“确定” 。  
  
### <a name="to-apply-3d-effects-to-a-funnel-chart"></a>将三维效果应用于漏斗图  
  
1.  右键单击图表区域的任意位置，然后选择“三维效果”。 随即显示“图表区属性”对话框。   
  
2.  在 **“三维选项”** 中，选择 **“启用三维”** 选项。 单击“确定” 。  
  
3.  （可选）若要自定义漏斗图视觉外观，可以转到“属性”窗格，更改漏斗图的特定属性。  
  
    1.  打开“属性”窗格。  
  
    2.  在设计图面上，单击漏斗图的任意位置。 漏斗图序列的属性将显示在“属性”窗格中。  
  
    3.  在 **“常规”** 部分，展开 **CustomAttributes** 节点。  
  
    4.  在 **Funnel3DDrawingStyle** 属性中，选择以圆形或正方形显示漏斗。  
  
    5.  对于 **Funnel3DRotationAngle** 属性，设置介于 -10 和 10 之间的值。 该值决定三维漏斗图显示的倾斜度。  
  
### <a name="to-apply-3d-effects-to-a-pie-chart"></a>将三维效果应用于饼图  
  
1.  右键单击图表区的任意位置，然后选择“三维效果”。 随即显示“图表区属性”对话框。   
  
2.  在 **“三维选项”** 中，选择 **“启用三维”** 选项。 单击“确定” 。  
  
3.  （可选）在“旋转”中，键入代表饼图水平旋转的整数值。  
  
4.  （可选）在“倾角”中，键入代表饼图垂直倾斜旋转的整数值。  
  
5.  单击“确定” 。  
  
### <a name="to-apply-3d-effects-to-a-bar-or-column-chart"></a>将三维效果应用于条形图或柱形图  
  
1.  右键单击图表区域的任意位置，然后选择“三维效果”。 随即显示“图表区属性”对话框。   
  
2.  选择 **“启用三维”** 选项。 单击“确定” 。  
  
3.  （可选）选择“启用序列聚类分析”选项。 如果图表包含多个条形图序列或柱形图序列，此选项会将该序列显示为聚集。 默认情况下，会并行显示多个条序列或列序列。  
  
4.  单击“确定” 。  
  
5.  （可选）若要将圆柱效果添加到条形图或柱形图，请按以下步骤操作：  
  
    1.  打开“属性”窗格。  
  
    2.  在设计图面上，单击序列中的任意条。 序列的属性将显示在“属性”窗格中。  
  
    3.  在 **“常规”** 部分，展开 **CustomAttributes** 节点。  
  
    4.  对于 **DrawingStyle** 属性，指定 **“柱状”** 值。  
  
## <a name="see-also"></a>请参阅  
 [图表中的三维效果、凹凸效果和其他效果（报表生成器和 SSRS）](chart-effects-3d-bevel-and-other-report-builder.md)   
 [设置图表格式（报表生成器和 SSRS）](formatting-a-chart-report-builder-and-ssrs.md)   
 [图表&#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
