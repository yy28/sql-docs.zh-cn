---
title: "指定对数刻度 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f3092c1c-b128-433d-9a95-983508b2a8d4
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3cbd1de3393757c20cf31c76be12d2911ecf7f9f
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="specify-a-logarithmic-scale-report-builder-and-ssrs"></a>指定对数刻度（报表生成器和 SSRS）
  如果数据按对数成比例，可能需要考虑在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中的图表上使用对数刻度。 这样做可以使数据更容易管理，因而有助于改善图表的外观。 大多数对数刻度都以 10 为底数。  
  
 此功能仅可在值轴上使用。 值轴通常是垂直轴（或 y 轴）。 但在条形图中，值轴是水平轴（或 x 轴）。  
  
 如果轴是采用对数刻度的轴，则与该轴相关的所有其他属性都将采用对数刻度。 例如，如果您指定在轴上采用以 10 为底数的对数刻度，则将轴间隔设置为 2 得到的间隔数量级将是 10 的 2 次幂，也就是 100。 这意味着，您的轴值读数将为 1、100、10000，而不是默认结果 1、10、100、1000、10000。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-a-logarithmic-scale"></a>指定对数刻度  
  
1.  右键单击图表的 y 轴，然后单击“垂直轴属性”。 随即出现“垂直轴属性”对话框。  
  
2.  在“轴选项”中，选择“使用对数刻度”。  
  
3.  在“对数底数”文本框中，键入一个用作对数底数的正值。 如果不指定任何值，则对数底数采用默认值 10。  
  
## <a name="see-also"></a>另请参阅  
 [设置图表上轴标签的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [设置图表格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [将轴标签的格式设置为日期或货币（报表生成器和 SSRS）](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
