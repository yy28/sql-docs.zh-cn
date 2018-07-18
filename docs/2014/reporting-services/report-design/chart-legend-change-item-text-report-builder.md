---
title: 更改图例项的文本（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9e82fa34-17ed-494f-b25d-03dcc353a21f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b9e18fe47a84785d7450a481c1eb6f1173b8bcf9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292127"
---
# <a name="change-the-text-of-a-legend-item-report-builder-and-ssrs"></a>更改图例项的文本（报表生成器和 SSRS）
  在图表的“值”区域中放入一个字段时，会自动生成一个包含此字段名称的图例项。 对于除形状图以外的其他图表，每个图例项会连接到图表上的单个序列，而对于形状图，图例会连接到单个数据点而不是单个序列。  
  
 在形状图上，可以更改图例项的文本，以便显示有关单个数据点的详细信息。 例如，如果你想要在图例中按百分比显示数据点的值，您可以使用一个关键字如`#PERCENT`。 可以一起追加 .NET Framework 格式代码和关键字，以便应用数字和日期格式。 有关关键字的详细信息，请参阅[设置图表上数据点的格式（报表生成器和 SSRS）](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)。  
  
 ![清晰图表](../media/sharpchart.png "清晰图表")  
  
 在非形状图上，可以更改图例项的文本。 例如，如果序列名称是“Series1”，您可能希望将该文本更改为更具说明性的名称，例如“Sales for 2008”。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-shape-chart"></a>修改在形状图的图例中显示的文本  
  
1.  右键单击某一序列，或右键单击“值”区域中的字段，并选择“序列属性”。  
  
2.  单击 **“图例”** ，并在 **“自定义图例文本”** 框中键入关键字。  
  
 下表提供了用于“自定义图例文本”属性的特定于图表的关键字示例。 有关关键字的详细信息，请参阅[设置图表上数据点的格式（报表生成器和 SSRS）](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)。  
  
|关键字|Description|图例中的显示文本示例|  
|-------------|-----------------|---------------------------------------------------|  
|`#PERCENT{P1}`|显示包含一个小数位的总计值百分比。|85.0%|  
|`#VALY`|显示数据字段的实际数值。|17000|  
|`#VALY{C2}`|将数据字段的实际数值显示为包含两个小数位的货币。|$17000.00|  
|`#AXISLABEL (#PERCENT{P0})`|显示类别字段的文本表示形式，后跟每个类别在图表上显示的百分比。|Michael Blythe (85%)|  
  
> [!NOTE]  
>  仅当“序列组”区域中没有指定的字段时，才能在运行时计算 #AXISLABEL 关键字。  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-non-shape-chart"></a>修改在非形状图的图例中显示的文本  
  
1.  右键单击某一序列，或右键单击“值”区域中的字段，并选择“序列属性”。  
  
2.  单击 **“图例”** ，并在 **“自定义图例文本”** 框中键入图例标签。 随即用该文本更新序列。  
  
## <a name="see-also"></a>请参阅  
 [设置图表上的图例的格式&#40;报表生成器和 SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [设置图表上序列颜色的格式（报表生成器和 SSRS）](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [隐藏图表上的图例项（报表生成器和 SSRS）](chart-legend-hide-items-report-builder.md)  
  
  
