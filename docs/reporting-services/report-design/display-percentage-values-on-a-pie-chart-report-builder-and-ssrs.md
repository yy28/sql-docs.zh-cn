---
title: 在饼图上显示百分比值（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bbc386708543b82fd79c012a40ab94f8001f5815
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56289815"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>在饼图上显示百分比值（报表生成器和 SSRS）
在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中，图例默认显示类别。 有时可能需要在图例或饼图扇区中显示百分比。   

![report-builder-pie-chart-preview-percents](../../reporting-services/media/report-builder-pie-chart-preview-percents.png)

 [教程：向报表添加饼图（报表生成器）](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)逐步介绍了如何向饼图添加百分比（若要先通过示例数据进行尝试的话）。
 
  
## <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>在饼图上显示百分比值  
  
1.  向报表添加一个饼图。 有关详细信息，请参阅[向报表添加图表（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)。  
  
2.  在设计图面上，右键单击饼图并选择“ **显示数据标签**”。 数据标签应显示在饼图上的每个切片上。  
  
3.  在设计图面上，右键单击标签并选择“ **序列标签属性**”。 此时将显示 **“序列标签属性”** 对话框。  
  
4.  在“ **标签数据** ”选项中键入 **#PERCENT** 。  
  
5.  （可选）若要指定标签显示的小数位数，请键入“#PERCENT{P*n*}”，其中 *n* 为要显示的小数位数。 例如，若不显示小数位数，请键入“#PERCENT{P0}”。  
  
## <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>在饼图的图例中显示百分比值  
  
1.  在设计图面上，右键单击饼图并选择“ **序列属性**”。 此时将显示 **“序列属性”** 对话框。  
  
2.  在“ **图例**”的“ **自定义图例文本** ”属性中键入 **#PERCENT** 。  
  
## <a name="see-also"></a>另请参阅  
* [教程：向报表添加饼图（报表生成器）](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [饼图&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [设置图表上图例的格式&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
*  [在饼图外显示数据点标签（报表生成器和 SSRS）](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 
  
