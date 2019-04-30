---
title: 折线图（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 194e6679-890d-4a3e-a756-130d32ef7e29
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 68e6ea1c31cea554944824e38926318682b163ce
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63209197"
---
# <a name="line-charts-report-builder-and-ssrs"></a>折线图（报表生成器和 SSRS）
  折线图将序列显示为一组由单个线条连接的点。 折线图用于表示在一段连续时间内发生的大量数据。 有关如何向折线图添加数据的详细信息，请参阅 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)。  
  
 下图显示了一个包含三个序列的折线图。  
  
 ![折线图](../media/rs-linechart.gif "Line chart")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>变体  
  
-   **平滑线图**。 一种使用曲线而不是规则线条的折线图。  
  
-   **渐变线图**。 一种使用渐变线而不是规则线条的折线图。 渐变线图通过使用一种线条来连接各点，这种线条使渐变线图看起来像阶梯或楼梯的梯级一样。  
  
-   **迷你图**。 迷你图是折线图的变体，它仅在 Tablix 或矩阵的单元中显示线条序列。 有关详细信息，请参阅 [迷你图和数据条（报表生成器和 SSRS）](sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="data-considerations-for-line-charts"></a>折线图的数据注意事项  
  
-   为了改善默认折线图的视觉效果，请考虑将序列边框的宽度更改为 3，然后增加阴影偏移量 1。 这样，所生成折线图的线条会粗得多。 如果将图表类型从“折线图”更改为其他类型，则需要将这些属性恢复为其原始值。  
  
-   如果数据集包含空值，则折线图将以占位符线的形式添加空点，以便保持图表上的连续性。 如果不希望看到这些占位符线，请考虑使用非连续图表类型（如条形图或柱形图）来显示数据集。  
  
-   折线图需要至少两个点才能绘制线条。  如果数据集只有一个数据点，则折线图将显示为一个数据点标记。  
  
-   绘制成线条的序列并不会在图表区占太大空间。  因此，折线图经常与其他图表类型（如柱形图）结合使用。 但是，折线图不能与条形图、极坐标图、饼图或形状图等图表类型结合使用。  
  
## <a name="see-also"></a>请参阅  
 [条形图（报表生成器和 SSRS）](bar-charts-report-builder-and-ssrs.md)   
 [柱形图（报表生成器和 SSRS）](column-charts-report-builder-and-ssrs.md)   
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)   
 [图表类型（报表生成器和 SSRS）](chart-types-report-builder-and-ssrs.md)   
 [分区图（报表生成器和 SSRS）](area-charts-report-builder-and-ssrs.md)   
 [图表中的空点和 Null 数据点（报表生成器和 SSRS）](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [图表&#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
