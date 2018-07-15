---
title: 指定轴间隔（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 3c619ec718e3471eb6518f6604a65c97cb367508
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304987"
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>指定轴间隔（报表生成器和 SSRS）
  轴间隔用于定义坐标轴上的标签和附带的刻度线的数目。 在值轴上，轴间隔提供图表上数据点的一致度量。 但是，在类别轴上，此功能会导致显示不带轴标签的类别。 可以在轴 Interval 属性中指定所需间隔数。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 根据结果集中的数据在运行时计算间隔数。 有关轴间隔的计算方式的详细信息，请参阅[设置图表上轴标签的格式（报表生成器和 SSRS）](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)。  
  
 本主题不适用于类别轴上的日期或时间值。 默认情况下，`DateTime`值显示为天数。 若要指定不同的日期或时间间隔，如月份或时间间隔，必须设置轴标签的格式并将该轴设置为显示 `DateTime` 类型而不是 `String` 类型的实例。 此外，必须设置 Interval 属性。 有关详细信息，请参阅[将轴标签的格式设置为日期或货币（报表生成器和 SSRS）](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)。  
  
 本主题不适用于饼图、圆环图、漏斗图或棱锥图，因为这些图表没有轴。  
  
> [!NOTE]  
>  类别轴通常是水平轴（或 x 轴）。 但对于条形图来说，类别轴是指垂直轴（或 y 轴）。  
  
 指定不同轴间隔的图表的示例可用于示例报表。 有关下载此示例报表和其他内容的详细信息，请参阅[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][报表生成器和报表设计器示例报表](http://go.microsoft.com/fwlink/?LinkId=198283)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-show-all-category-labels-on-the-x-axis"></a>在 X 轴上显示所有类别标签  
  
1.  右键单击类别轴，然后单击 **“轴属性”**。 随即会打开 **“轴属性”** 对话框。  
  
2.  在中**轴选项**，请设置`Interval`到**1**。 随即显示每个类别组标签。 如果希望在 X 轴上显示所有其他类别组标签，请键入 **2**。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  设置轴间隔后，将禁用所有自动标签。 如果指定轴间隔的值，则可能会遇到不可知的标签行为，具体取决于类别轴上的类别数。  
  
### <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>启用轴上的可变间隔计算  
  
1.  右键单击要更改的图表轴，然后单击 **“轴属性”**。 随即会打开 **“轴属性”** 对话框。  
  
2.  在中**轴选项**，请设置`Interval`到**自动**。该图表将显示适合该轴的最佳类别标签数。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [设置图表格式（报表生成器和 SSRS）](formatting-a-chart-report-builder-and-ssrs.md)   
 [设置图表上数据点的格式&#40;报表生成器和 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [对数据区域中的数据进行排序（报表生成器和 SSRS）](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [“轴属性”对话框 ->“轴选项”（报表生成器和 SSRS）](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [指定对数刻度（报表生成器和 SSRS）](specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [在辅助轴上绘制数据（报表生成器和 SSRS）](plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  
