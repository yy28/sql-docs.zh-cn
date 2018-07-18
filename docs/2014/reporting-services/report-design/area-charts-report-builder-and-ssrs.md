---
title: 面积图（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 245b236d-1d55-4744-b752-80bd133502aa
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 84262598ecb49d69eae360b6de3b4e78369e7fc8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37260533"
---
# <a name="area-charts-report-builder-and-ssrs"></a>面积图（报表生成器和 SSRS）
  面积图将序列显示为一组由线连接的点，并填充线下方的所有区域。 有关如何将数据添加到面积图的详细信息，请参阅[图表&#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)。  
  
 下图显示了一个堆积面积图的例子。 这里的数据非常适合用堆积面积图显示，因为这种图表可以显示所有序列的总计以及每个序列在总计中所占的比例。  
  
 ![面积图](../media/areachart.gif "面积图")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>变体  
  
-   **堆积面积图**。 一种多个序列垂直堆积的面积图。 如果图表中只有一个序列，则这种堆积面积图将与一般面积图的显示相同。  
  
-   **百分比堆积面积图**。 一种多个序列垂直堆积以占满整个图表区的面积图。 如果图表中只有一个序列，则这种堆积面积图将与一般面积图的显示相同。  
  
-   **平滑面积图**。 一种由平滑线而非规则线连接数据点的面积图。 如果您更加关注显示走向而非显示各个数据点的值，则应使用平滑面积图而非一般的面积图。  
  
## <a name="data-considerations-for-area-charts"></a>面积图的数据注意事项  
  
-   除折线图之外，面积图是唯一一种连续显示数据的图表类型。 因此，面积图常用来表示在一个连续时间段内出现的数据。  
  
-   百分比堆积面积图对显示在一段时间内出现的成比例数据很有用。  
  
-   如果只有一个序列，则会将堆积面积图绘制成一般的面积图。  
  
-   在一般的面积图中，如果多个序列中的值相似，则面积可能会发生重叠，从而遮挡了重要的数据点值。 可以通过将图表类型更改为堆积面积图来解决此问题，堆积面积图的设计目的就是为了在面积图上显示多个序列。  
  
-   如果堆积面积图中含有间隙，可能是因为数据集包含空值，空值在堆积面积图上将显示为空白区域。 如果数据集包含空值，请考虑在图表中插入空点。 如果添加空点，则会用一种不同的颜色填充图表上的空白区域以指示 Null 或零值。 有关详细信息，请参阅[向图表添加空点&#40;报表生成器和 SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)。  
  
-   面积图类型在行为上与柱形图和折线图非常相似。 如果要在多个序列之间进行比较，请考虑改用柱形图。 如果要分析在一段时间内的走向，请考虑使用折线图。  
  
## <a name="see-also"></a>请参阅  
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)   
 [图表类型（报表生成器和 SSRS）](chart-types-report-builder-and-ssrs.md)   
 [折线图（报表生成器和 SSRS）](line-charts-report-builder-and-ssrs.md)   
 [更改图表类型（报表生成器和 SSRS）](change-a-chart-type-report-builder-and-ssrs.md)   
 [空和 Null 数据点在图表中的&#40;报表生成器和 SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
