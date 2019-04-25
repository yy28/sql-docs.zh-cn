---
title: 第 7 课：创建关键绩效指标 |Microsoft Docs
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ecfedbbc4b7e606f1589f2b5415c5355bb0d95e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62523355"
---
# <a name="lesson-7-create-key-performance-indicators"></a>第 7 课：创建关键绩效指标
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课中，您将创建关键绩效指标 (KPI)。 KPI 用于根据“目标”值度量由“基础”度量值定义的值（也可以是由度量值或绝对值定义的值）的性能。 在报表客户端应用程序中，KPI 可以向业务专业人士提供一种快速简便的方法，使他们了解业务绩效的摘要或确定趋势。 若要了解详细信息，请参阅[Kpi](../analysis-services/tabular-models/kpis-ssas-tabular.md)。  
  
估计的时间才能完成本课程中：**15 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 执行任务之前在本课程中，您应当已完成上一课：[第 6 课：创建度量值](../analysis-services/lesson-6-create-measures.md)。   
  
## <a name="create-key-performance-indicators"></a>创建关键绩效指标  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>创建 InternetCurrentQuarterSalesPerformance KPI  
  
1.  在模型设计器中，单击**FactInternetSales**表 （选项卡）。  
  
2.  在度量值网格中，单击一个空单元。  
  
3.  在表上面的公式栏中，键入以下公式： 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=IFERROR([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    该度量值充当 KPI 的基础度量值。  
  
4.  右键单击**InternetCurrentQuarterSalesPerformance** > **创建 KPI**。   
  
5.  在关键绩效指标 (KPI) 对话框中，在**目标**选择**绝对值**，然后键入**1.1**。  
  
7.  在左侧（低）滑块字段中，输入 **1**，然后在右侧（高）滑块字段中，输入 **1.07**。  
  
8.  在“选择图标样式”中，选择钻石（红色）、三角形（黄色）、圈（绿色）图标类型。
  
    ![as-tabular-lesson7-kpi](../analysis-services/media/as-tabular-lesson7-kpi.png)
    
    > [!TIP]  
    > 请注意**说明**可用图标样式下方的标签。 用于为要使其更易于识别在客户端应用程序中的各种 KPI 元素输入说明。  
  
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
  
5.  在“定义状态阈值”中，滑动左侧（低）滑块字段，直到此字段显示 **0.8**，然后滑动右侧（高）滑块字段，直到此字段显示 **1.03**。  
  
6.  在“选择图标样式”中，选择钻石（红色）、三角形（黄色）、圈（绿色）图标类型，然后单击“确定”。  
  
## <a name="whats-next"></a>下一步是什么？
请转到下一课：[第 8 课：创建透视](../analysis-services/lesson-8-create-perspectives.md)。
  
  
