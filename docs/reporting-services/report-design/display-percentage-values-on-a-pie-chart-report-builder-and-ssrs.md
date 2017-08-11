---
title: "饼图 （报表生成器和 SSRS） 上显示百分比值 |Microsoft 文档"
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
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6c0fdf9d1b694f2f6d49389e913d1c156ba77838
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>在饼图上显示百分比值（报表生成器和 SSRS）
在[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]分页的报表，默认情况下，图例显示的类别。 你可能想在图例或饼图扇区本身中的百分比。   

![report-builder-pie-chart-preview-percents](../../reporting-services/media/report-builder-pie-chart-preview-percents.png)

 [教程： 将饼形图添加到您的报表 （报表生成器）](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)如果你想要首先示例数据来尝试这将指导你完成添加到饼图扇区的百分比。
 
  
## <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>在饼图上显示百分比值  
  
1.  向报表添加一个饼图。 有关详细信息，请参阅[向报表添加图表&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)。  
  
2.  在设计图面上，右键单击饼图并选择“**显示数据标签**”。 数据标签应显示在饼图上的每个切片上。  
  
3.  在设计图面上，右键单击标签并选择“ **序列标签属性**”。 此时将显示 **“序列标签属性”** 对话框。  
  
4.  在“ **标签数据** ”选项中键入 **#PERCENT** 。  
  
5.  （可选）若要指定标签显示的小数位数，请键入“#PERCENT{P*n*}”，其中 *n* 为要显示的小数位数。 例如，若不显示小数位数，请键入“#PERCENT{P0}”。  
  
## <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>在饼图的图例中显示百分比值  
  
1.  在设计图面上，右键单击饼图并选择“ **序列属性**”。 此时将显示 **“序列属性”** 对话框。  
  
2.  在“ **图例**”的“ **自定义图例文本** ”属性中键入 **#PERCENT** 。  
  
## <a name="see-also"></a>另请参阅  
* [教程：向报表添加饼图（报表生成器）](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [饼图 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [设置图表上图例的格式&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
*  [在饼图外显示数据点标签&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 
  
