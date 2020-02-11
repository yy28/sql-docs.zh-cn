---
title: 散点图（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2520ae24-0609-4890-807d-3267018aba8e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dde53428c738fc30595d17b62175b50835fe7ec2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105042"
---
# <a name="scatter-charts-report-builder-and-ssrs"></a>散点图（报表生成器和 SSRS）
  散点图将序列显示为一组点。 值由点在图表中的位置表示。 类别由图表中的不同标记表示。 散点图通常用于比较跨类别的聚合数据。 有关如何将数据添加到散点图的详细信息，请参阅 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)  
  
 下图显示的是散点图示例。  
  
 ![散点图](../media/rs-scatterchart.gif "散点图")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>变体  
  
-   **气泡.** 气泡图根据气泡的大小来显示数据点的两个值之间的差。 气泡越大，两个值之间的差就越大。  
  
-   三维**气泡图**。 以三维形式显示的气泡图。  
  
## <a name="data-considerations-for-a-scatter-chart"></a>散点图的数据注意事项  
  
-   散点图通常用于显示和比较数值，例如科学数据、统计数据和工程数据。  
  
-   当要在不考虑时间的情况下比较大量数据点时，请使用散点图。 散点图中包含的数据越多，比较的效果就越好。  
  
-   气泡图要求每个数据点具有两个值（探顶值和探底值）。  
  
-   对于处理值的分布和数据点的分簇，散点图都很理想。 如果数据集中包含非常多的点（例如，几千个点），那么散点图便是最佳图表类型。 在点状图中显示多个序列看上去非常混乱，这种情况下，应避免使用点状图， 而应考虑使用折线图。  
  
-   默认情况下，散点图以圆圈显示数据点。 如果在散点图中有多个序列，请考虑将每个点的标记形状更改为方形、三角形、菱形或其他形状。  
  
## <a name="see-also"></a>另请参阅  
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)   
 [图表类型（报表生成器和 SSRS）](chart-types-report-builder-and-ssrs.md)   
 [设置图表格式（报表生成器和 SSRS）](formatting-a-chart-report-builder-and-ssrs.md)   
 [折线图（报表生成器和 SSRS）](line-charts-report-builder-and-ssrs.md)  
  
  
