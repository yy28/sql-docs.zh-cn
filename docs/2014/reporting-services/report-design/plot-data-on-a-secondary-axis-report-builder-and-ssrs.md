---
title: 在辅助轴上绘制数据（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 094f39bf-3634-4852-9fc3-3adec4b266e5
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 35b7228fbc975cd1ab658f541e1a5c17ee0790c5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129133"
---
# <a name="plot-data-on-a-secondary-axis-report-builder-and-ssrs"></a>在辅助轴上绘制数据（报表生成器和 SSRS）
  图表有两个轴类型：主轴和辅助轴。 将两个值集与共享共有类别的两个不同数据范围进行比较时，辅助轴将非常有用。  
  
 例如，假设您有一个计算 2008 年 Revenue 和 Tax 的图表。 在这种情况下，对于这两个值集而言，2008 年这一时间段是它们共有的。 但是，在同一个 Y 轴上绘制这两个序列时，我们无法进行有用的比较，因为 Y 轴上的刻度已针对数据集中的最大值进行了优化。 如果在主轴上显示 Revenue，在辅助轴上显示 Tax，则可以在每个序列各自的 Y 轴上分别显示它们，并显示其各自的值范围。 序列仍共享共有的 X 轴。  
  
 在需要对两种以上的序列进行比较的情况下，可考虑使用不同的方法来在图表中比较和显示多个序列。 有关详细信息，请参阅[图表中的多个序列（报表生成器和 SSRS）](multiple-series-on-a-chart-report-builder-and-ssrs.md)。  
  
 此图表的示例可用于示例报表。 有关下载此示例报表和其他内容的详细信息，请参阅 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][报表生成器和报表设计器示例报表](http://go.microsoft.com/fwlink/?LinkId=198283)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-plot-a-series-on-the-secondary-axis"></a>在辅助轴上绘制序列  
  
1.  右键单击图表中的序列，或右键单击要在辅助轴上显示的 **“值”** 区域中的某个字段，然后单击 **“序列属性”**。 随即出现 **“序列属性”** 对话框。  
  
2.  单击 **“轴和图表区”**，然后选择要启用的辅助轴、值轴或类别轴。  
  
## <a name="see-also"></a>请参阅  
 [设置图表上轴标签的格式（报表生成器和 SSRS）](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [指定轴间隔&#40;报表生成器和 SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  