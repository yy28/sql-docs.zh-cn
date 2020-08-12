---
title: 图表故障排除（报表生成器）| Microsoft Docs
description: 使用沿值轴的数字数据类型的字段（而不是带格式的数字）来显示数值。
ms.date: 01/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 45894eca20fa5762eb4f2e02496e79bd327c8fb3
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689468"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>图表故障排除（报表生成器和 SSRS）
  对以下问题的解答可能在您使用图表时对您有所帮助。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>为什么我的图表对值轴上的值进行计数，而不是求和？  
 大多数图表类型都要求数值放置在通常作为 y 轴的值轴上，以便能够正确地绘制图表。 如果值字段的数据类型是 **String**，则图表将无法显示数值，即使这些字段中包含数字也是如此。 相反，该图表将显示包含该字段中值的行的总行数。 若要避免出现此情况，请确保用于值序列的字段是数字数据类型的，而不是包含格式化数字的字符串。  

## <a name="need-more-help"></a>需要更多帮助？  
   
  请尝试：  
 * Stack Overflow 上的 [SQL Server Reporting Services](https://stackoverflow.com/questions/tagged/reporting-services)  
 * 在 [Microsoft SQL Server UserVoice](https://feedback.azure.com/forums/908035-sql-server) 上提出问题或建议。  
  
## <a name="see-also"></a>另请参阅  
 [图表&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
