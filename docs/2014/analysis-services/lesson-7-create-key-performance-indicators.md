---
title: 第 8 课：创建关键绩效指标 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a6c8ac2b-64ba-456f-b418-7bf0afe145d1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 62b4102ba7a8b1ff2d5c833001b90dd74707fdc5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728133"
---
# <a name="lesson-8-create-key-performance-indicators"></a>第 8 课：创建关键绩效指标
  在本课中，您将创建关键绩效指标 (KPI)。 KPI 用于根据“目标”值度量由“基础”度量值定义的值（也可以是由度量值或绝对值定义的值）的性能。 在报表客户端应用程序中，KPI 可以向业务专业人士提供一种快速简便的方法，使他们了解业务绩效的摘要或确定趋势。 若要了解详细信息，请参阅 [KPI（SSAS 表格）](tabular-models/kpis-ssas-tabular.md)。  
  
 估计的时间才能完成本课程中：**15 分钟**  
  
## <a name="prerequisites"></a>先决条件  
 本主题是表格建模教程的一部分，该教程应按顺序学习。 执行任务之前在本课程中，您应当已完成上一课：[第 7 课：创建度量值](lesson-6-create-measures.md)。  
  
## <a name="create-key-performance-indicators"></a>创建关键绩效指标  
  
#### <a name="to-create-an-internet-current-quarter-sales-performance-kpi"></a>创建 Internet Current Quarter Sales Performance KPI  
  
1.  在模型设计器中，单击“Internet Sales”表（选项卡）。  
  
2.  在度量值网格中，单击一个空单元。  
  
3.  在表上面的公式栏中，键入以下公式：  
  
     `Internet Current Quarter Sales Performance :=IFERROR([Internet Current Quarter Sales]/[Internet Previous Quarter Sales Proportion to QTD],BLANK())`  
  
     在您完成公式的建立后，按 Enter。  
  
     该度量值充当 KPI 的基础度量值。  
  
4.  在度量值网格中，右键单击“Internet Current Quarter Sales Performance”度量值，然后单击“创建 KPI”。  
  
     将打开“关键绩效指标”对话框。  
  
5.  在“关键绩效指标”对话框的“定义目标值”中，选择“绝对值”选项。  
  
6.  在中**绝对值**字段中，键入`1.1`，然后按 ENTER。  
  
7.  在中**定义状态阈值**，在左侧 （低） 滑块字段中，键入`1`，然后在右侧 （高） 滑块字段中，键入`1.07`。  
  
8.  在“选择图标样式”中，选择钻石（红色）、三角形（黄色）、圈（绿色）图标类型。  
  
    > [!TIP]  
    >  请注意可用图标样式下方的“说明”可扩展字段。 您可以为不同的 KPI 元素键入说明，以使它们在客户端应用程序中更易于识别。  
  
9. 单击“确定”以完成 KPI。  
  
     在度量值网格中，请注意“Internet Current Quarter Sales Performance”度量值旁的图标。 此图标表示此度量值充当 KPI 的基本值。  
  
#### <a name="to-create-an-internet-current-quarter-margin-performance-kpi"></a>创建 Internet Current Quarter Margin Performance KPI  
  
1.  在“Internet Sales”表的度量值网格中，单击一个空单元。  
  
2.  在表上面的公式栏中，键入以下公式：  
  
     `Internet Current Quarter Margin Performance :=IF([Internet Previous Quarter Margin Proportion to QTD]<>0,([Internet Current Quarter Margin]-[Internet Previous Quarter Margin Proportion to QTD])/[Internet Previous Quarter Margin Proportion to QTD],BLANK())`  
  
     在您完成公式的建立后，按 Enter。  
  
3.  在度量值网格中，右键单击“Internet Current Quarter Margin Performance”度量值，然后单击“创建 KPI”。  
  
4.  在“关键绩效指标”对话框的“定义目标值”中，选择“绝对值”选项。  
  
5.  在中**绝对值**字段中，键入`1.25`。  
  
6.  在“定义状态阈值”中，滑动左侧（低）滑块字段，直到此字段显示 **0.8**，然后滑动右侧（高）滑块字段，直到此字段显示 **1.03**。  
  
7.  在“选择图标样式”中，选择钻石（红色）、三角形（黄色）、圈（绿色）图标类型，然后单击“确定”。  
  
## <a name="next-step"></a>下一步  
 若要继续学习本教程，请转到下一课：[第 9 课：创建透视](lesson-8-create-perspectives.md)。  
  
  
