---
title: "轴标签的格式设置为日期或货币 （报表生成器和 SSRS） |Microsoft 文档"
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
ms.assetid: e9a01a74-2f51-4b35-be3a-a6138568f6cf
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7b8f82c7824a44d46a282eca8d617fb12ac9ade5
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs"></a>将轴标签的格式设置为日期或货币（报表生成器和 SSRS）
当在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表的轴上显示格式设置正确的 DateTime 值时，图表会自动将这些值显示为天数。 若要为 x 轴指定日期/时间间隔，如月份或小时间隔，则必须设置轴标签的格式，并要将轴间隔的类型设置为有效的日期或时间间隔。  
  
> [!NOTE]  
>  在柱形图和散点图中，水平轴（或 x 轴）是类别轴。 在条形图中，垂直轴（或 y 轴）是类别轴。  
  
 X 轴上显示的值的计算结果必须为 <xref:System.DateTime> 数据类型，才能正确地设置时间间隔的格式。 如果您的字段具有数据类型的<xref:System.String>，图表将计算为日期或时间间隔。 有关详细信息，请参阅[图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)。  
  
 向 Y 轴添加数值时，默认情况下，图表不会在显示该数值前设置其格式。 如果数值字段为销售数字，请考虑将其格式设置为货币，以增强图表的可读性。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-format-x-axis-labels-as-monthly-intervals"></a>将 X 轴标签的格式设置为月间隔  
  
1.  右键单击图表的水平轴（或 x 轴），然后选择“水平轴属性”。  
  
2.  在“水平轴属性”对话框中，选择“数字”。  
  
3.  从 **“类别”** 列表中，选择 **“日期”**。 从“类型”列表中，选择要应用到 X 轴标签的日期格式。  
  
4.  选择 **“轴选项”**。  
  
5.  在 **“间隔”**中，键入 **1**。 在 **“间隔类型”** 属性中，选择 **“月”**。  
  
    > [!NOTE]  
    >  如果不指定间隔类型，则图表将按天计算间隔。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-format-y-axis-labels-using-a-currency-format"></a>使用货币格式设置 Y 轴标签的格式  
  
1.  右键单击图表的垂直轴（或 y 轴），然后选择“垂直轴属性”。  
  
2.  在“垂直轴属性”对话框中，选择“数字”。  
  
3.  从 **“类别”** 列表中，选择 **“货币”**。 从“符号”列表中，选择要应用到 Y 轴标签的货币格式。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [设置图表上轴标签的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [设置图表格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [指定对数刻度（报表生成器和 SSRS）](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [指定轴间隔（报表生成器和 SSRS）](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  
