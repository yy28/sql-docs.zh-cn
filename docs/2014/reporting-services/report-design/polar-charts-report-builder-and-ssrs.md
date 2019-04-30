---
title: 极坐标图（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c9402d8f-202a-4cdf-949e-50f5b1d2b885
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 46e431f85960f0fb5ce93ff80a53a3001c1b666d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63215752"
---
# <a name="polar-charts-report-builder-and-ssrs"></a>极坐标图（报表生成器和 SSRS）
  极坐标图将序列显示为一组位于 360 度圆上、按类别分组的点。 值通过由自圆心测量的点的长度来表示。 点离圆心的距离越远，其值越大。 类别标签显示在图表的周边上。 有关如何将数据添加到坐标图的详细信息，请参阅 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>变体  
  
-   **雷达图**。 雷达图将序列显示为环形线条或区域。 与极坐标图不同的是，雷达图不是以极坐标的形式显示数据。  
  
## <a name="data-considerations-for-polar-charts"></a>极坐标图的数据注意事项  
  
-   雷达图在比较多个类别数据序列方面很有用。  
  
-   极坐标图最常用于以图形表示极坐标数据，其中的每个数据点都是由一个角度和一个距离共同决定的。  
  
-   在同一图表区中，极坐标图不能与任何其他图表类型结合使用。  
  
## <a name="example"></a>示例  
 下例说明了如何使用雷达图。 下表提供了雷达图的示例数据。  
  
|名称|Sales|  
|----------|-----------|  
|Shrubs|61|  
|Seeds|78|  
|Bulbs|60|  
|Trees|38|  
|Flowers|81|  
  
 在本例中，“名称”字段放置在“类别组”区域中。 “销售量”字段放置在“值”区域中。 放置“销售量”字段时，图表的该字段将自动合计。 雷达图根据“销售量”字段中值的个数计算标签的放置位置，该字段包含五个值，因此将标签放在圆上的五个等分点处。 如果“销售量”字段包含三个值，则会将标签放在圆上的三个等分点处。  
  
 下图显示了一个基于前面所提供数据的雷达图示例。  
  
 ![雷达图](../media/rs-radarchart.gif "雷达图")  
  
## <a name="see-also"></a>请参阅  
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)   
 [设置图表格式（报表生成器和 SSRS）](formatting-a-chart-report-builder-and-ssrs.md)   
 [图表类型（报表生成器和 SSRS）](chart-types-report-builder-and-ssrs.md)   
 [折线图（报表生成器和 SSRS）](line-charts-report-builder-and-ssrs.md)   
 [图表中的空白和 Null 数据点（报表生成器和 SSRS）](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
