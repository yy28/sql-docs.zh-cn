---
title: "显示数据点标签饼图 （报表生成器和 SSRS） 外 |Microsoft 文档"
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
ms.assetid: 959b7574-cf43-470b-b592-4944d8a9948f
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2faa5b4e48f86c331ee45913844dc50c54c89e63
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs"></a>在饼图外显示数据点标签（报表生成器和 SSRS）
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，饼图标签经过了优化，可以仅在几个数据切片中显示标签。 如果饼图包含的切片过多，标签可能会重叠。 一种解决方案是在饼图外显示标签，这样可能会为较长的数据标签留出更多的空间。 如果发现标签仍然重叠，可以启用三维来为这些标签留出更多的空间。 这将减小饼图的直径，在饼图周围留出更多的空间。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-data-point-labels-inside-a-pie-chart"></a>在饼图内显示数据点标签  
  
1.  向报表添加一个饼图。 有关详细信息，请参阅[向报表添加图表（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)。  
  
2.  在设计图面上，右键单击图表并选择“显示数据标签”。  
  
### <a name="to-display-data-point-labels-outside-a-pie-chart"></a>在饼图外显示数据点标签  
  
1.  创建一个饼图，并显示数据标签。  
  
2.  打开“属性”窗格。  
  
3.  在设计图面上，单击饼图本身以在“属性”窗格中显示 **“类别”** 属性。  
  
4.  展开 **CustomAttributes** 节点。 此时将显示该饼图的属性列表。  
  
5.  将 **PieLabelStyle** 属性设置为 **Outside**。  
  
6.  将 **PieLineColor** 属性设置为 **Black**。 PieLineColor 属性可为每个数据点标签定义标注线条。  
  
### <a name="to-prevent-overlapping-labels-displayed-outside-a-pie-chart"></a>防止在饼图外显示的标签重叠  
  
1.  创建一个带有外部标签的饼图。  
  
2.  在设计图面上，在饼图外部但在饼图边界之内右键单击，然后选择“图表区属性”。将显示“图表区属性”对话框。  
  
3.  在 **“三维选项”** 选项卡上，选择 **“启用三维”**。  
  
4.  如果希望图表为标签留出更多空间但仍显示二维效果，则将“旋转”和“倾角”属性设置为 **0**。  
  
## <a name="see-also"></a>另请参阅  
 [饼图（报表生成器和 SSRS）](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [收集饼图上的小切片（报表生成器和 SSRS）](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)   
 [在饼图上显示百分比值（报表生成器和 SSRS）](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
