---
title: "隐藏图表上的图例项（报表生成器和 SSRS） | Microsoft Docs"
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
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# 隐藏图表上的图例项（报表生成器和 SSRS）
默认情况下，添加到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中的非形状图的任何序列将在图例中添加为图例项。 对于饼图、圆环图、漏斗图和棱锥图，添加到图表的任何序列将在图例中添加单个数据点。  
  
 您可以隐藏图例中的任何项。 隐藏图例项时，该项仍将在图表中显示。 当您不希望显示添加到图表的序列的详细信息时，上述功能非常有用。 例如，如果已将计算序列（如移动平均值）添加到图表，可能需要在图例中隐藏该条目，以便仅显示原始序列的详细信息。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## 在图例中隐藏项  
  
1.  右键单击要隐藏的序列，并选择“序列属性”。  
  
2.  单击 **“图例”**。 选择 **“不在图例中显示此序列”** 选项。  
  
    > [!NOTE]  
    >  不能仅针对一个组隐藏序列，而对其他组显示该序列。 如果将字段添加到 **“序列组”** 区域中，将隐藏该组所包含的所有序列。  
  
## 另请参阅  
 [设置图表上图例的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-the-legend-on-a-chart-report-builder-and-ssrs.md)   
 [设置图表上数据点的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [更改图例项的文本（报表生成器和 SSRS）](../../reporting-services/report-design/change-the-text-of-a-legend-item-report-builder-and-ssrs.md)   
 [向图表添加移动平均线（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [“图例属性”对话框，“常规”（报表生成器和 SSRS）](../Topic/Legend%20Properties%20Dialog%20Box,%20General%20\(Report%20Builder%20and%20SSRS\).md)  
  
  