---
title: 向图表添加空点（报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2b056119-439f-494f-83cf-ee0c05dc6487
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 59c79d4824c7df4709c571d5d46476fd89f3cbe4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106611"
---
# <a name="add-empty-points-to-the-chart-report-builder-and-ssrs"></a>向图表添加空点（报表生成器和 SSRS）
  Null 值在图表中显示为空格或显示为序列中数据点间的空白。 空点是可在由 Null 值创建的空格中插入的数据点。  
  
 默认情况下，空点是通过取包含值的前一个数据点和后一个数据点的平均值而计算的。 您可以更改此默认行为以使所有空点都在零处插入。  
  
 有关详细信息，请参阅[图表中的空点和 Null 数据点（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-empty-points-on-a-chart"></a>在图表中指定空点  
  
1.  打开“属性”窗格。  
  
2.  在设计图面上，右键单击包含 Null 值的序列。 序列的属性将显示在“属性”窗格中。  
  
3.  展开 **EmptyPoint** 节点。  
  
4.  为 Color 属性选择颜色值。  
  
5.  在 **EmptyPoint** 节点中，展开 Marker 节点。  
  
6.  为 MarkerType 属性选择标记类型。  
  
    > [!NOTE]  
    >  您必须选择标记类型以将空点添加到条形图、柱形图或散点图中。 但是，对于面积图、折线图和雷达图，是否选择标记类型是可选的，因为这些图表会填充空格或空白，而不需要指定标记。  
  
7.  设置空点的值。  
  
    1.  在“属性”窗格中，展开 **CustomAttributes** 节点。  
  
    2.  设置 EmptyPointValue 属性。 若要在前一个数据点和后一个数据点的平均值插入空点，请选择 **Average**。 若要在零处插入空点，请选择 **Zero**。  
  
## <a name="see-also"></a>另请参阅  
 [添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [图表类型（报表生成器和 SSRS）](chart-types-report-builder-and-ssrs.md)   
 [在图表中添加刻度分隔线（报表生成器和 SSRS）](add-scale-breaks-to-a-chart-report-builder-and-ssrs.md)   
 [图表&#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
