---
title: "图表故障排除（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4f7c1005a361e5eae7a7d1b674691df6e7444d46
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>图表故障排除（报表生成器和 SSRS）
  对以下问题的解答可能在您使用图表时对您有所帮助。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>为什么我的图表对值轴上的值进行计数，而不是求和？  
 大多数图表类型都要求数值放置在通常作为 y 轴的值轴上，以便能够正确地绘制图表。 如果值字段的数据类型是 **String**，则图表将无法显示数值，即使这些字段中包含数字也是如此。 相反，该图表将显示包含该字段中值的行的总行数。 若要避免出现此情况，请确保用于值序列的字段是数字数据类型的，而不是包含格式化数字的字符串。  
  
## <a name="see-also"></a>另请参阅  
 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
