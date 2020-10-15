---
title: 在图表中添加或删除边距（报表生成器）| Microsoft Docs
description: 在报表生成器中添加或删除柱形图或散点图的边距。 改善分页报表的可读性或外观。
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 91c43f58-5771-4d33-a54d-0e802d2f5cba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bbe5af103737cb9b4a5ba7e063f19b9cd6c1da41
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935359"
---
# <a name="add-or-remove-margins-from-a-chart-report-builder-and-ssrs"></a>在图表中添加或删除边距（报表生成器和 SSRS）
对于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中的柱形图和散点图，图表会自动在 x 轴结尾处添加侧边距。 在条形图中，图表会自动在 y 轴结尾处添加侧边距。 在所有其他图表类型中，图表都不会添加侧边距。 您无法更改该边距的大小。  
  
 本主题不适用于饼图、圆环图、漏斗图或棱锥图类型。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-enable-or-disable-side-margins"></a>启用或禁用侧边距  
  
1.  右键单击轴，然后选择“轴属性”。 将显示“垂直轴属性”或“水平轴属性”对话框。  
  
2.  在 **“轴选项”** 页中，设置 **“侧边距”** 属性：  
  
    -   **自动** 图表将基于图表类型确定是否添加侧边距。  
  
    -   **已禁用** 条形图、柱形图和散点图将不具有侧边距。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [设置图表上轴标签的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [“轴属性”对话框 ->“轴选项”（报表生成器和 SSRS）](/previous-versions/sql/)   
 [指定轴间隔（报表生成器和 SSRS）](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [将轴标签的格式设置为日期或货币（报表生成器和 SSRS）](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [图表&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
