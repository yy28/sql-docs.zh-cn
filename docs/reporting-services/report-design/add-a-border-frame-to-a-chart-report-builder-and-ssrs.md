---
title: 向图表添加边框（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: ca0c5040-40bb-4cb7-bc2b-5bcbe73858bb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4a98492ecca7cafebfff34e6438edb39e173d8b8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65571641"
---
# <a name="add-a-border-frame-to-a-chart-report-builder-and-ssrs"></a>向图表添加边框（报表生成器和 SSRS）
  若要增强图表的视觉效果，可以考虑在图表的外部周围使用边框。 可以使用 **“图表属性”** 对话框或“属性”窗格来选择边框。 图表的边框不能应用于任何其他数据区域。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-apply-a-border-to-a-chart"></a>向图表应用边框  
  
1.  右键单击图表上的任意位置并选择“图表属性”  。  
  
    > [!NOTE]  
    >  如果看不到“图表属性”，请在快捷菜单中指向“图表”，然后选择“图表属性”    。  
  
2.  选择 **“边框”** ，然后单击要应用于图表的边框类型。  
  
3.  （可选）选择一个值或键入一个表示边框样式的表达式。  
  
4.  （可选）指定将绘制在图表周围作为边框的线条的颜色。  
  
    > [!NOTE]  
    >  **“线条颜色”** 列表中包括常用颜色。 若要在更多颜色列表中进行选择，请在列表中单击“更多颜色”，或单击列表旁的表达式 (fx) 按钮以打开“表达式”编辑器    。  
  
5.  （可选）指定边框的宽度。 有效值介于 0.25pt 到 20pt 之间。 可以考虑将边框的大小保持在 1pt 到 3pt 之间，以获得最佳视觉效果。  
  
6.  （可选）如果报表包含白色之外的背景色，可以考虑定义同一种颜色的页面颜色。 页面颜色是边框线外部的背景色。  
  
7.  （可选）如果选择“框架”类型，则可为该框架指定样式和颜色。 **“框架填充颜色”** 列表中包括常用颜色。  
  
## <a name="see-also"></a>另请参阅  
 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [设置图表格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [向图表添加凹凸效果、阳文和纹理样式（报表生成器和 SSRS）](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)  
  
  
