---
title: 在图表中添加或删除边距（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 91c43f58-5771-4d33-a54d-0e802d2f5cba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ce2fcfe65c3b674f89b3174fd1e88421a7bdb853
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106537"
---
# <a name="add-or-remove-margins-from-a-chart-report-builder-and-ssrs"></a>在图表中添加或删除边距（报表生成器和 SSRS）
  在柱形图和散点图中，图表会自动在 x 轴结尾处添加侧边距。 在条形图中，图表会自动在 y 轴结尾处添加侧边距。 在所有其他图表类型中，图表都不会添加侧边距。 您无法更改该边距的大小。  
  
 本主题不适用于饼图、圆环图、漏斗图或棱锥图类型。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-enable-or-disable-side-margins"></a>启用或禁用侧边距  
  
1.  右键单击轴，然后选择“轴属性”  。 将显示“垂直轴属性”  或“水平轴属性”  对话框。  
  
2.  在 **“轴选项”** 页中，设置 **“侧边距”** 属性：  
  
    -   **自动** 图表将基于图表类型确定是否添加侧边距。  
  
    -   **已禁用** 条形图、柱形图和散点图将不具有侧边距。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [设置图表上轴标签的格式（报表生成器和 SSRS）](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [“轴属性”对话框 ->“轴选项”（报表生成器和 SSRS）](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [指定轴间隔（报表生成器和 SSRS）](specify-an-axis-interval-report-builder-and-ssrs.md)   
 [将轴标签的格式设置为日期或货币（报表生成器和 SSRS）](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [图表&#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
