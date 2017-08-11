---
title: "添加或删除边距 （报表生成器和 SSRS） 在图表中 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91c43f58-5771-4d33-a54d-0e802d2f5cba
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 795435899de548848ca64cec26d212fd8a80f900
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

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
 [在图表 &#40; 的格式设置轴标签报表生成器和 SSRS &#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [轴属性对话框中，轴选项 &#40;报表生成器和 SSRS &#41;](http://msdn.microsoft.com/library/b276e210-7a12-48ae-971b-7dabae51df11)   
 [指定轴间隔 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [为日期或货币 &#40; 的格式轴标签报表生成器和 SSRS &#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [图表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
