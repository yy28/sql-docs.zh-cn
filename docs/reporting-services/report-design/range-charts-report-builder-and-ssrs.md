---
title: "范围图 （报表生成器和 SSRS） |Microsoft 文档"
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
ms.assetid: 48e351d3-ac5b-4eda-a4bd-32a0de206a30
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1cdcf1877134ea93ec52b3c7fb70dbfeda536a93
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="range-charts-report-builder-and-ssrs"></a>范围图（报表生成器和 SSRS）
  范围图类型用于显示一组数据点，其中每个数据点都由同一类别的多个值定义。 这些值通过由值轴度量的标记高度来表示。 类别标签显示在类别轴上。 平面范围图用于填充每个数据点的探顶值和探底值之间的区域。  
  
 下图显示了具有三个序列的平面范围图。  
  
 ![范围图](../../reporting-services/report-design/media/rs-rangechart.gif "范围图")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>变体  
  
-   **平滑范围图**。 平滑范围图显示的是曲线而不是直线。  
  
-   **柱形范围图**。 柱形范围图使用柱形图而不是面积图来显示范围。  
  
-   **条形范围图**。 条形范围图使用条形图而不是面积图来显示范围。  
  
## <a name="data-considerations-for-range-charts"></a>范围图的数据注意事项  
  
-   每个数据点的范围图类型都需要两个值。 这些值与定义每个数据点范围的高值和低值相对应。  
  
-   仅当探顶值始终高于探底值时，才可将范围图用于分析。 如果探顶值不高于探底值，请考虑使用折线图。 如果高值低于低值，则范围图将显示这两个值之差的绝对值。  
  
-   如果仅指定了一个值，则范围图的显示方式将与常规面积图的显示方式相同，每个数据点用一个值表示。  
  
-   范围图通常用于以图形方式表示包含数据集中每一类别组的最小值和最大值的数据。  
  
-   范围图不支持在每个数据点上显示标记。  
  
-   与面积图一样，在平面范围图中，如果多个序列中的值相似，这些序列将相互重叠。 在这种情况下，最好使用柱形范围图或者条形范围图，而非平面范围图。  
  
-   可以使用范围条形图创建甘特图。  
  
## <a name="see-also"></a>另请参阅  
 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [图表类型（报表生成器和 SSRS）](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [设置图表格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)  
  
  
