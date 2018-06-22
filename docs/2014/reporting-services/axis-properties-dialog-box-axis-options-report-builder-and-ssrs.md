---
title: 轴属性对话框，轴选项 （报表生成器和 SSRS） |Microsoft 文档
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.axisproperties.axisoptions.f1
- "10138"
ms.assetid: b276e210-7a12-48ae-971b-7dabae51df11
caps.latest.revision: 10
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 947b985ef25eec47ec8f064c752c5dad49fdf30b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016771"
---
# <a name="axis-properties-dialog-box-axis-options-report-builder-and-ssrs"></a>“轴属性”对话框 ->“轴选项”（报表生成器和 SSRS）
  选择**轴选项**上**水平**或**VerticalAxis 属性**对话框中，可以定义图表指定轴的外观。 在以前版本的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中，默认情况下，图表会在 X 轴上显示所有标签。 但在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2008 中，图表会跳过一些标签，以使生成的图表更加整洁，并避免标签冲突。 有关详细信息，请参阅[设置图表上轴标签的格式（报表生成器和 SSRS）](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>“常规”  
 **启用刻度分隔线**  
 选择此选项可在必要时启用图表以绘制小数位数分隔符。 启用此选项后，图表将自动计算数据集中高点与低点之间是否存在足够的差异以绘制小数位数分隔符。  
  
 **反转方向**  
 选择此选项可以反转图表的方向。 例如，默认情况下，柱形图在图表的左侧显示 Y 轴，并从左向右显示类别。 选择了此选项后，图表将在其右侧显示 Y 轴并从右向左显示类别。  
  
 **使用交错颜色**  
 选择此选项以将条带线添加到图表中，然后选择一种颜色或键入表达式。 条带线是图表区域的阴影带，可在网格线之间形成明暗交错的区域。 这些条带线对于突出显示轴上的重复样式非常有用。  
  
 **始终包括零**  
 选择此选项可以在轴刻度上始终包括零。 如果此选项未启用，则图表不会在轴上标记零值。 包括零值在数据集包含负值或零值时将非常有用。  
  
 **标量轴**  
 选择此选项可以在连续刻度上显示一组轴值。 例如，如果数据集包含一月、三月和十一月的数据，则非标量轴仅显示这些月份，而标量轴将显示一年中的所有月份。  
  
 **使用对数刻度**  
 选择此选项以指示轴刻度为对数刻度。 当轴包含正的数值时，此选项仅能用于 Y 轴。  
  
 当轴设置为使用对数刻度时，在框中键入要使用的对数底数。 默认情况下，图表对轴的对数刻度使用底数 10。 当轴是数轴时，此选项仅能用于 Y 轴。  
  
 **最低要求**  
 键入一个表示 X 轴最小值的表达式或值。 如果省略此参数，最小值将由数据集返回的数据决定。  
  
 **最大值**  
 键入一个表示 X 轴最大值的表达式或值。 如果省略此参数，最大值将由数据集返回的数据决定。  
  
 **间隔**  
 键入表示轴标签之间间隔的表达式或值。 例如，键入 1 将在轴上显示每个类别标签。 键入 2 将每隔一个类别标签显示一次。 如果省略，则将基于数据集中的值自动计算标签。  
  
 **间隔类型**  
 键入表示指定间隔的间隔类型的表达式或值。 例如，如果希望间隔为两天，则需指定间隔为 **2** ，间隔类型为 **天** 。  
  
 **侧边距**  
 键入一个表达式或选择一个值，以添加或去除图表元素与图表边之间的边距。 如果将此选项设置为 **“自动”**，则会添加侧边距。  
  
## <a name="see-also"></a>请参阅  
 [设置图表上轴标签的格式（报表生成器和 SSRS）](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [图表（报表生成器和 SSRS）](report-design/charts-report-builder-and-ssrs.md)   
 [设置图表上序列颜色的格式（报表生成器和 SSRS）](report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [指定轴间隔（报表生成器和 SSRS）](report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [将轴标签的格式设置为日期或货币（报表生成器和 SSRS）](report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [辅助轴上绘制数据&#40;报表生成器和 SSRS&#41;](report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)   
 [迷你图和数据条（报表生成器和 SSRS）](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [添加或从图表中删除边距&#40;报表生成器和 SSRS&#41;](report-design/add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
  