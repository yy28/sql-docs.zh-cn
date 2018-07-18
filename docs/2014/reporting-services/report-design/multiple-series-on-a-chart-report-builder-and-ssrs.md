---
title: 图表中的多个序列（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b99e4398-1fba-4824-958f-5c75d10485ea
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: dea720120f13f1546af8a1ab9bdd572badabb350
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292117"
---
# <a name="multiple-series-on-a-chart-report-builder-and-ssrs"></a>图表中的多个序列（报表生成器和 SSRS）
  当图表中存在多个序列时，必须确定比较这些序列的最佳方式。 可以使用堆积图显示每个序列的相对比例。 如果仅比较两个共享公用类别 (x) 轴的序列，请使用辅助轴。 当显示两个相关数据序列（例如，价格和数量或收入和税收）时，该方法非常有用。 如果图表不可读，请考虑使用多个图表区以增强各序列之间的目视间隔。  
  
 除使用图表功能以外，还必须确定针对您的数据使用哪种图表类型。 如果数据集中的各字段相互关联，请考虑使用范围图。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-stacked-and-100-stacked-charts"></a>使用堆积图和百分比堆积图  
 堆积图通常用于在一个图表区中显示多个序列。 当尝试显示的数据紧密相关时，请考虑使用堆积图。 在一个堆积图中显示的序列最好不超过四个。 如果要比较每个序列在总体中所占的比例，请使用百分比堆积面积图、条形图或柱形图。 这些图表可计算每个序列在相应类别中所占的相对百分比。 有关详细信息，请参阅[分区图（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)、[条形图（报表生成器和 SSRS）](bar-charts-report-builder-and-ssrs.md)和[柱形图（报表生成器和 SSRS）](column-charts-report-builder-and-ssrs.md)。  
  
## <a name="using-the-secondary-axis"></a>使用辅助轴  
 将新序列添加到图表时，将使用主 x 和 y 轴来绘制该序列。 如果要比较的值采用不同的测量单位，请考虑使用“辅助轴”  ，以便可以在不同的轴上绘制两个序列。 当比较具有不同测量单位的值时，辅助轴将非常有用。 辅助轴是在主轴的另一侧绘制的。 图表仅支持主轴和辅助轴。 辅助轴的属性与主轴相同。 有关详细信息，请参阅[在辅助轴上绘制数据（报表生成器和 SSRS）](plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)。  
  
 如果要显示具有不同数据范围的多个序列，请考虑将这些序列放置到不同的图表区。  
  
## <a name="using-chart-areas"></a>使用图表区  
 图表为包括外部边框、图表标题和图例的顶级容器。 默认情况下，图表包含一个默认图表区。 图表区在图表图面上不可见，但您可将图表区视为只包含轴标签、轴标题和一个或多个序列的绘图区的容器。 下图说明了单个图表中的图表区的概念。  
  
 ![显示图表区域的图表](../media/chartareasdiagram.gif "Shows a diagram of a chart area")  
  
 使用 **“图表区属性”** 对话框，可以指定图表区包含的所有序列的二维和三维方向，对齐同一图表中的多个图表区，并设置绘图区颜色的格式。 在仅包含一个默认图表区的图表中定义新的图表区时，该图表区的可用空间水平划分为两部分，新图表区位于第一个图表区的下方。  
  
 每个序列只能连接到一个图表区。 默认情况下，所有序列都将添加到默认图表区。 使用面积图、柱形图、折线图和散点图时，这些序列的任何组合均可显示在同一图表区上。 例如，可以在同一图表区中显示柱形序列和线条序列。 对多个序列使用同一图表区的优点是方便最终用户进行比较。  
  
 在同一图表区中，条形图、雷达图和形状图不能与任何其他图表类型结合使用。 如果希望对条形、雷达或形状类型的多个序列进行比较，则需要执行下列操作之一：  
  
-   将图表区中的所有序列更改为相同图表类型。  
  
-   新建一个图表区，并将一个或多个序列从默认图表区移动到新建的图表区。  
  
 如果要尝试比较具有不同刻度值的数据，在单个图表中使用多个图表区的功能也非常有用。 例如，如果第一个序列包含的数据的范围介于 10 到 20 之间，而第二个序列包含的数据的范围介于 400 到 800 之间，则第一个序列中的值可能会变得很模糊。 请考虑将每个序列分别置于不同的图表区。 有关详细信息，请参阅[指定序列的图表区域（报表生成器和 SSRS）](specify-a-chart-area-for-a-series-report-builder-and-ssrs.md)。  
  
## <a name="using-range-charts"></a>使用范围图  
 范围图中的每个数据点都有两个值。 如果图表包含两个共享同一类别 (x) 轴的序列，则可以使用范围图显示这两个序列之间的差异。 范围图最适合显示呈高低或上下变化的信息。 例如，如果第一个序列包含一月中每天的最高销售额，而第二个序列包含一月中每天的最低销售额，则可以使用范围图显示每天的最高销售额和最低销售额之间的差异。 有关详细信息，请参阅[全距图（报表生成器和 SSRS）](range-charts-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)   
 [在图表中显示包含多个数据区域的序列（报表生成器和 SSRS）](displaying-a-series-with-multiple-data-ranges-on-a-chart.md)   
 [图表类型&#40;报表生成器和 SSRS&#41;](chart-types-report-builder-and-ssrs.md)  
  
  
