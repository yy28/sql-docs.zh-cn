---
title: 在序列上显示工具提示（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4c9606ff-e1c3-4cf7-a4e7-bb16f1a9e8ab
caps.latest.revision: 5
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: ae6fc4bd445be2aab739aa23b42d1aa5a6198879
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125055"
---
# <a name="show-tooltips-on-a-series-report-builder-and-ssrs"></a>在序列上显示工具提示（报表生成器和 SSRS）
  可以向图表的序列上的每个数据点添加工具提示，以显示与数据点有关的信息，例如，用户将光标悬停在所呈现报表中的数据点上时，会显示组名、数据点的值，或数据点相对于序列总计的百分比。  
  
 无法向计算序列添加工具提示。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-a-tooltip-on-each-data-point"></a>指定关于每个数据点的工具提示  
  
1.  右键单击序列，或右键单击“值”区域中的字段，并单击“序列属性”。  
  
2.  单击 **“序列数据”** ，并为 **“工具提示”** 属性键入字符串或表达式。 可以使用任何特定于图表的关键字来表示图表上的另一个元素。 有关详细信息，请参阅[图表上的格式设置数据点&#40;报表生成器和 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [格式设置图表上的数据点&#40;报表生成器和 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [更改图例项的文本（报表生成器和 SSRS）](chart-legend-change-item-text-report-builder.md)   
 [设置图表上序列颜色的格式（报表生成器和 SSRS）](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [在报表中添加钻取操作（报表生成器和 SSRS）](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  