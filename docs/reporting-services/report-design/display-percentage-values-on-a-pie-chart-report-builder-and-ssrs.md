---
title: "在饼图上显示百分比值（报表生成器和 SSRS） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 6
---
# 在饼图上显示百分比值（报表生成器和 SSRS）
  默认情况下，图例中显示了类别来标识每个值。 如果使用了类别标签标记饼图，则可能希望在图例中显示百分比。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### 在饼图上显示百分比值  
  
1.  向报表添加一个饼图。 有关详细信息，请参阅[向报表添加图表&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)。  
  
2.  在设计图面上，右键单击饼图并选择“**显示数据标签**”。 数据标签应显示在饼图上的每个切片上。  
  
3.  在设计图面上，右键单击标签并选择“**序列标签属性**”。 此时将显示 **“序列标签属性”** 对话框。  
  
4.  在“ **标签数据**”选项中键入 **#PERCENT**。  
  
5.  （可选）若要指定标签显示的小数位数，请键入“#PERCENT{P*n*}”，其中 *n* 为要显示的小数位数。 例如，若不显示小数位数，请键入“#PERCENT{P0}”。  
  
### 在饼图的图例中显示百分比值  
  
1.  在设计图面上，右键单击饼图并选择“**序列属性**”。 此时将显示 **“序列属性”** 对话框。  
  
2.  在“**图例**”的“**自定义图例文本**”属性中键入 **#PERCENT**。  
  
## 另请参阅  
 [饼图&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [设置图表上图例的格式&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/formatting-the-legend-on-a-chart-report-builder-and-ssrs.md)   
 [在饼图外显示数据点标签&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [收集饼图上的小切片&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  