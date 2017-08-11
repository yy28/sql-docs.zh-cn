---
title: "设置仪表 （报表生成器和 SSRS） 上的范围的格式 |Microsoft 文档"
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
ms.assetid: ffdec8ca-3e95-41cd-850b-9e8c83be4b49
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a4c28739a1b35655f74a16a6757958e0e1bc6e47
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="formatting-ranges-on-a-gauge-report-builder-and-ssrs"></a>设置仪表上范围的格式（报表生成器和 SSRS）
 在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中，仪表范围是仪表刻度上的带区或区域，用于指示仪表上一段重要的值。 使用仪表范围，能以可见方式指示指针值何时进入某个值范围。 范围由开始值和结束值定义。  
  
 还可以使用范围来定义仪表的各个不同分段。 例如，在值从 0 到 10 的仪表上，可以定义从 0 到 3 的值为红色范围，从 4 到 7 的值为黄色范围，从 8 到 10 的值为绿色范围。 如果指定的开始值大于指定的结束值，则值将交换，以使开始值成为结束值，而结束值成为开始值。  
  
 可以使用在刻度上放置指针的相同方式来设置范围。 **“位置”** 和 **“到刻度的距离”** 属性可确定范围的位置。 有关详细信息，请参阅 [仪表（报表生成器和 SSRS）](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [在仪表 &#40; 的格式设置刻度报表生成器和 SSRS &#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [在仪表 &#40; 的格式设置指针报表生成器和 SSRS &#41;](../../reporting-services/report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [在仪表 &#40; 上设置最小值或最大值报表生成器和 SSRS &#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)   
 [教程： 将 KPI 添加到您的报表 &#40;报表生成器 &#41;](../../reporting-services/tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [仪表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
