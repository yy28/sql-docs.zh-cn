---
title: 在序列上显示工具提示（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4c9606ff-e1c3-4cf7-a4e7-bb16f1a9e8ab
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6901123f4a28560c504bc9a83522cb108a6d7b12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104924"
---
# <a name="show-tooltips-on-a-series-report-builder-and-ssrs"></a>在序列上显示工具提示（报表生成器和 SSRS）
  可以向图表的序列上的每个数据点添加工具提示，以显示与数据点有关的信息，例如，用户将光标悬停在所呈现报表中的数据点上时，会显示组名、数据点的值，或数据点相对于序列总计的百分比。  
  
 无法向计算序列添加工具提示。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-a-tooltip-on-each-data-point"></a>指定关于每个数据点的工具提示  
  
1.  右键单击序列，或右键单击“值”区域中的字段，并单击“序列属性”   。  
  
2.  单击 **“序列数据”** ，并为 **“工具提示”** 属性键入字符串或表达式。 可以使用任何特定于图表的关键字来表示图表上的另一个元素。 有关详细信息，请参阅 [设置图表上数据点的格式（报表生成器和 SSRS）](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [设置图表上数据点的格式（报表生成器和 SSRS）](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [更改图例项的文本（报表生成器和 SSRS）](chart-legend-change-item-text-report-builder.md)   
 [设置图表上序列颜色的格式（报表生成器和 SSRS）](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [在报表中添加钻取操作（报表生成器和 SSRS）](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  
