---
title: 指定对数刻度（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f3092c1c-b128-433d-9a95-983508b2a8d4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dee4f84615d3cff90cdd8bef20cb77be7bf40879
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59941743"
---
# <a name="specify-a-logarithmic-scale-report-builder-and-ssrs"></a>指定对数刻度（报表生成器和 SSRS）
  如果您的数据按对数成比例，您可能需要考虑在图表上使用对数刻度。 这样做可以使数据更容易管理，因而有助于改善图表的外观。 大多数对数刻度都以 10 为底数。  
  
 此功能仅可在值轴上使用。 值轴通常是垂直轴（或 y 轴）。 但在条形图中，值轴是水平轴（或 x 轴）。  
  
 如果轴是采用对数刻度的轴，则与该轴相关的所有其他属性都将采用对数刻度。 例如，如果您指定在轴上采用以 10 为底数的对数刻度，则将轴间隔设置为 2 得到的间隔数量级将是 10 的 2 次幂，也就是 100。 这意味着，您的轴值读数将为 1、100、10000，而不是默认结果 1、10、100、1000、10000。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-a-logarithmic-scale"></a>指定对数刻度  
  
1.  右键单击图表的 y 轴，然后单击“垂直轴属性”。 随即出现“垂直轴属性”对话框。  
  
2.  在“轴选项”中，选择“使用对数刻度”。  
  
3.  在“对数底数”文本框中，键入一个用作对数底数的正值。 如果不指定任何值，则对数底数采用默认值 10。  
  
## <a name="see-also"></a>请参阅  
 [设置图表上轴标签的格式（报表生成器和 SSRS）](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [设置图表格式（报表生成器和 SSRS）](formatting-a-chart-report-builder-and-ssrs.md)   
 [将轴标签的格式设置为日期或货币（报表生成器和 SSRS）](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [图表&#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
