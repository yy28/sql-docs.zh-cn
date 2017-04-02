---
title: "将三维效果添加到图表（报表生成器和 SSRS） | Microsoft Docs"
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
ms.assetid: ab9625d8-6557-4a4d-8123-eefa7c066ff5
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# 将三维效果添加到图表（报表生成器和 SSRS）
  三维 (3D) 效果可以使 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中的图表更具深度感并增强视觉效果。 例如，若要强调分离型饼图的某个特定切片，可以旋转并更改图表的透视，以便人们可以首先注意到该切片。 将三维效果应用于图表时，将会禁用所有渐变颜色和阴影类型。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## 将三维效果应用于范围图、面积图、折线图、散点图或极坐标图  
  
1.  右键单击图表区域的任意位置，然后选择“三维效果”。 随即显示“图表区属性”对话框。   
  
2.  在 **“三维选项”**中，选择 **“启用三维”** 选项。  
  
3.  （可选）在“三维选项”中，可以设置各种与三维角度和场景选项相关的属性。 有关这些属性的详细信息，请参阅[图表中的三维效果、凹凸效果和其他效果（报表生成器和 SSRS）](../../reporting-services/report-design/3d-bevel-and-other-effects-in-a-chart-report-builder-and-ssrs.md)。  
  
4.  单击 **“确定”**。  
  
## 将三维效果应用于漏斗图  
  
1.  右键单击图表区域的任意位置，然后选择“三维效果”。 随即显示“图表区属性”对话框。   
  
2.  在 **“三维选项”**中，选择 **“启用三维”** 选项。 单击 **“确定”**。  
  
3.  （可选）若要自定义漏斗图视觉外观，可以转到“属性”窗格，更改漏斗图的特定属性。  
  
    1.  打开“属性”窗格。  
  
    2.  在设计图面上，单击漏斗图的任意位置。 漏斗图序列的属性将显示在“属性”窗格中。  
  
    3.  在 **“常规”** 部分，展开 **CustomAttributes** 节点。  
  
    4.  在 **Funnel3DDrawingStyle** 属性中，选择以圆形或正方形显示漏斗。  
  
    5.  对于 **Funnel3DRotationAngle** 属性，设置介于 -10 和 10 之间的值。 该值决定三维漏斗图显示的倾斜度。  
  
## 将三维效果应用于饼图  
  
1.  右键单击图表区的任意位置，然后选择“三维效果”。 随即显示“图表区属性”对话框。   
  
2.  在 **“三维选项”**中，选择 **“启用三维”** 选项。 单击 **“确定”**。  
  
3.  （可选）在“旋转”中，键入代表饼图水平旋转的整数值。  
  
4.  （可选）在“倾角”中，键入代表饼图垂直倾斜旋转的整数值。  
  
5.  单击 **“确定”**。  
  
## 将三维效果应用于条形图或柱形图  
  
1.  右键单击图表区域的任意位置，然后选择“三维效果”。 随即显示“图表区属性”对话框。   
  
2.  选择 **“启用三维”** 选项。 单击 **“确定”**。  
  
3.  （可选）选择“启用序列聚类分析”选项。 如果图表包含多个条形图序列或柱形图序列，此选项会将该序列显示为聚集。 默认情况下，会并行显示多个条序列或列序列。  
  
4.  单击 **“确定”**。  
  
5.  （可选）若要将圆柱效果添加到条形图或柱形图，请按以下步骤操作：  
  
    1.  打开“属性”窗格。  
  
    2.  在设计图面上，单击序列中的任意条。 序列的属性将显示在“属性”窗格中。  
  
    3.  在 **“常规”** 部分，展开 **CustomAttributes** 节点。  
  
    4.  对于 **DrawingStyle** 属性，指定 **“柱状”** 值。  
  
## 另请参阅  
 [图表中的三维效果、凹凸效果和其他效果（报表生成器和 SSRS）](../../reporting-services/report-design/3d-bevel-and-other-effects-in-a-chart-report-builder-and-ssrs.md)   
 [设置图表格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  