---
title: 隐藏图表上的图例项（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 04eafb5e3fe9a1ebbf6073b706f1635a43a715b1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="chart-legend---hide-items-report-builder"></a>图表图例 - 隐藏项（报表生成器）
默认情况下，添加到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中的非形状图的任何序列将在图例中添加为图例项。 对于饼图、圆环图、漏斗图和棱锥图，添加到图表的任何序列将在图例中添加单个数据点。  
  
 您可以隐藏图例中的任何项。 隐藏图例项时，该项仍将在图表中显示。 当您不希望显示添加到图表的序列的详细信息时，上述功能非常有用。 例如，如果已将计算序列（如移动平均值）添加到图表，可能需要在图例中隐藏该条目，以便仅显示原始序列的详细信息。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-hide-an-item-from-display-in-the-legend"></a>在图例中隐藏项  
  
1.  右键单击要隐藏的序列，并选择“序列属性”。  
  
2.  单击 **“图例”**。 选择 **“不在图例中显示此序列”** 选项。  
  
    > [!NOTE]  
    >  不能仅针对一个组隐藏序列，而对其他组显示该序列。 如果将字段添加到 **“序列组”** 区域中，将隐藏该组所包含的所有序列。  
  
## <a name="see-also"></a>另请参阅  
 [设置图表上图例的格式（报表生成器和 SSRS）](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
 [设置图表上数据点的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [更改图例项的文本（报表生成器和 SSRS）](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)   
 [向图表添加移动平均线（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [“图例属性”对话框 ->“常规”（报表生成器和 SSRS）](http://msdn.microsoft.com/library/db718f8f-f185-422f-871c-96f0749e5893)  
  
  
