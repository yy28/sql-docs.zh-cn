---
title: Analysis Services 教程第 7 课： 创建关键绩效指标 |Microsoft Docs
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e0cd1cfa0c468f28b5cadfc9757671f18206d2cd
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43087562"
---
# <a name="create-key-performance-indicators"></a>创建关键绩效指标

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，您将创建关键绩效指标 (Kpi)。 Kpi 用于测量由定义的值的性能*Base*度量值，针对*目标*同样由度量值或绝对值定义的值。 在报表客户端应用程序中，KPI 可以向业务专业人士提供一种快速简便的方法，使他们了解业务绩效的摘要或确定趋势。 若要了解详细信息，请参阅[Kpi](../tabular-models/kpis-ssas-tabular.md)
  
学完本课的估计时间： **15 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文是表格建模教程应按顺序完成的一部分。 在之前在本课程中执行的任务，您应已完成上一课：[第 6 课： 创建度量值](../tutorial-tabular-1400/as-lesson-6-create-measures.md)。   
  
## <a name="create-key-performance-indicators"></a>创建关键绩效指标  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>创建 InternetCurrentQuarterSalesPerformance KPI  
  
1.  在模型设计器中，单击**FactInternetSales**表。  
  
2.  在度量值网格中，单击一个空单元。  
  
3.  在表上面的公式栏中，键入以下公式： 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    此度量值用作 KPI 的基本度量值。  
  
4.  在度量值网格中，右键单击**InternetCurrentQuarterSalesPerformance** > **创建 KPI**。   
  
5.  在关键绩效指标 (KPI) 对话框中，在**目标**选择**绝对值**，然后键入**1.1**。  
  
7.  在左侧（低）滑块字段中，输入 **1**，然后在右侧（高）滑块字段中，输入 **1.07**。  
  
8.  在“选择图标样式”中，选择钻石（红色）、三角形（黄色）、圈（绿色）图标类型。
  
    ![作为 lesson7 kpi](../tutorial-tabular-1400/media/as-lesson7-kpi.png)
    
    > [!TIP]  
    > 请注意**说明**可用图标样式下方的标签。 按照说明为各种 KPI 元素使其更易于识别在客户端应用程序中。  
  
9. 单击“确定”以完成 KPI。  
  
    在度量值网格中，注意图标旁边**InternetCurrentQuarterSalesPerformance**度量值。 此图标表示此度量值充当 KPI 的基本值。  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>创建 InternetCurrentQuarterMarginPerformance KPI  
  
1.  中的度量值网格**FactInternetSales**表中，单击某个空单元格。  
  
2.  在表上面的公式栏中，键入以下公式：  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  右键单击**InternetCurrentQuarterMarginPerformance** > **创建 KPI**。  
  
4.  在关键绩效指标 (KPI) 对话框中，在**目标**选择**绝对值**，然后键入**1.25**。   
  
5.  在左侧 （低） 滑块字段中，滑动，直到此字段显示**0.8**，然后滑动右侧 （高） 滑块字段，直到此字段显示**1.03**。  
  
6.  在“选择图标样式”中，选择钻石（红色）、三角形（黄色）、圈（绿色）图标类型，然后单击“确定”。  
  
## <a name="whats-next"></a>下一步是什么？

[第 8 课： 创建透视](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)。
  
  
