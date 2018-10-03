---
title: 在饼图上显示百分比值（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0853b168b4b7728ffe18e5562b84887205a7cdef
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059047"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>在饼图上显示百分比值（报表生成器和 SSRS）
  默认情况下，图例中显示了类别来标识每个值。 如果使用了类别标签标记饼图，则可能希望在图例中显示百分比。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>在饼图上显示百分比值  
  
1.  向报表添加一个饼图。 有关详细信息，请参阅[向报表添加图表（报表生成器和 SSRS）](add-a-chart-to-a-report-report-builder-and-ssrs.md)。  
  
2.  在设计图面上，右键单击饼图并选择“ **显示数据标签**”。 数据标签应显示在饼图上的每个切片上。  
  
3.  在设计图面上，右键单击标签并选择“ **序列标签属性**”。 此时将显示 **“序列标签属性”** 对话框。  
  
4.  类型`#PERCENT`有关**标签数据**选项。  
  
5.  （可选）若要指定标签显示的小数位数，请键入“#PERCENT{P*n*}”，其中 *n* 为要显示的小数位数。 例如，若不显示小数位数，请键入“#PERCENT{P0}”。  
  
### <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>在饼图的图例中显示百分比值  
  
1.  在设计图面上，右键单击饼图并选择“ **序列属性**”。 此时将显示 **“序列属性”** 对话框。  
  
2.  在中**图例**，类型`#PERCENT`有关**自定义图例文本**属性。  
  
## <a name="see-also"></a>请参阅  
 [饼图&#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [设置图表上的图例的格式&#40;报表生成器和 SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [在饼图外显示数据点标签&#40;报表生成器和 SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [收集饼图上的小切片&#40;报表生成器和 SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
