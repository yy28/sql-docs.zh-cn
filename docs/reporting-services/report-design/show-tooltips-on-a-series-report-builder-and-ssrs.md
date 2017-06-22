---
title: "在一系列 （报表生成器和 SSRS） 上显示工具提示 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4c9606ff-e1c3-4cf7-a4e7-bb16f1a9e8ab
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5e963b234c5c3babb4dd2302afca2ca06ac249b1
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="show-tooltips-on-a-series-report-builder-and-ssrs"></a>在序列上显示工具提示（报表生成器和 SSRS）
  可以向图表的序列上的每个数据点添加工具提示，以显示与数据点有关的信息，例如，组名、数据点的值，或数据点相对于序列总计的百分比。 用户将鼠标悬停在呈现的分页报表中的数据点时，将看到此信息。  
  
 无法向计算序列添加工具提示。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-a-tooltip-on-each-data-point"></a>指定关于每个数据点的工具提示  
  
1.  右键单击序列，或右键单击“值”区域中的字段，并单击“序列属性”。  
  
2.  单击 **“序列数据”** ，并为 **“工具提示”** 属性键入字符串或表达式。 可以使用任何特定于图表的关键字来表示图表上的另一个元素。 有关详细信息，请参阅 [设置图表上数据点的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [设置图表上数据点的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [更改图例项的文本（报表生成器和 SSRS）](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)   
 [设置图表上序列颜色的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [在报表中添加钻取操作（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  
