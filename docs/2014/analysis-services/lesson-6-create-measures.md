---
title: 第7课：创建度量值 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef207028ab1b4f6bc084f3f4e515ae37630b771d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078430"
---
# <a name="lesson-7-create-measures"></a>第 7 课：创建度量值
  在本课中，您将创建要包括在您的模型中的度量值。 与您在前一课中创建的计算列类似，度量值从根本上来说是使用 DAX 公式创建的计算。 但是，与计算列不同的是，度量值是基于用户选择的筛选器** 计算的；例如，添加到某个数据透视表的“行标签”字段中的特定列或切片器。   然后，所应用的度量值将计算筛选器中每个单元格的值。 度量值是功能强大的、灵活的计算，您可以将其包含在几乎所有表格模型中，以便对数值数据执行动态计算。 若要了解详细信息，请参阅[度量值（SSAS 表格）](tabular-models/measures-ssas-tabular.md)。  
  
 为了创建度量值，您将使用度量值网格。 默认情况下，每个表都有一个空的度量值网格；不过，通常不会为每个表都创建度量值。 在数据视图中时，度量值网格显示在模型设计器中的表下方。 要隐藏或显示表的度量值网格，请单击“表”菜单，并单击“显示度量值网格”。********  
  
 可以通过以下方式创建度量值：单击度量值网格中的某个空单元格，并在公式栏中键入一个 DAX 公式。 当单击 ENTER 以完成公式时，度量值会显示在单元格中。 还可以通过以下方式使用标准聚合函数创建度量值：单击某个列，并单击工具栏上的“自动求和”按钮 (**∑**)。 使用“自动求和”功能创建的度量值将显示在该列正下方的度量值网格单元中，但是可以根据需要移动它们。  
  
 在本课中，您将通过在编辑栏中输入一个 DAX 公式并使用“自动求和”功能来创建度量值。  
  
 学完本课的估计时间： **30 分钟**  
  
## <a name="prerequisites"></a>必备条件  
 本主题是表格建模教程的一部分，应当按顺序完成。 在执行本课程中的任务之前，应该已完成上一课：[第 6 课：创建计算列](lesson-5-create-calculated-columns.md)。  
  
## <a name="create-measures"></a>创建度量值  
  
#### <a name="to-create-a-days-current-quarter-to-date-measure-in-the-date-table"></a>在 Date 表中创建 Days Current Quarter to Date 度量值  
  
1.  在模型设计器中，单击“Date”**** 表。  
  
2.  如果表下方尚未显示空的度量值网格，请单击“表”**** 菜单，然后单击“显示度量值网格”****。  
  
3.  在度量值网格中，单击左上角的空单元格。  
  
4.  在表上方的公式栏中，键入以下公式：  
  
     `=COUNTROWS( DATESQTD( 'Date'[Date]))`  
  
     在您完成公式的建立后，按 Enter。  
  
     请注意，左上角的单元格现在包含度量值名称、**度量值 1**，后跟结果**30**。 在编辑栏中，度量值名称也位于公式前。  
  
5.  若要重命名该度量值，请在编辑栏中突出显示名称、**度量值 1**，然后键入`Days Current Quarter to Date`，然后按 enter。  
  
    > [!TIP]  
    >  在编辑栏中键入公式时，您还可以首先键入度量值名称后跟冒号 (:)，然后输入一个空格，最后输入公式。 使用此方法，您不必重命名度量值。  
  
#### <a name="to-create-a-days-in-current-quarter-measure-in-the-date-table"></a>在 Date 表中创建 Days in Current Quarter 度量值  
  
1.  当“Date”**** 表在模型设计器中仍处于活动状态时，在度量值网格中，单击刚才创建的度量值下方的空单元。  
  
2.  在公式栏中，键入以下公式：  
  
     `Days in Current Quarter :=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))`  
  
     请注意，在此公式中，首先包含了后跟一个冒号 (:) 的度量值名称。  
  
     在您完成公式的建立后，按 Enter。  
  
 在创建不完整期间与上一期间之间的对比率时，公式必须考虑该期间已过时间的比例，并将其与上一期间中的同一时间比例进行比较。 在此情况下，[Days Current Quarter to Date]/[Days in Current Quarter] 给出当前期间中已消逝的比例。  
  
#### <a name="to-create-an-internet-distinct-count-sales-order-measure-in-the-internet-sales-table"></a>在 Internet Sales 表中创建 Internet Distinct Count Sales Order 度量值  
  
1.  在模型设计器中，单击“Internet Sales”**** 表（选项卡）。  
  
     如果尚未显示度量值网格，请右键单击“Internet Sales”**** 表（选项卡），然后单击“显示度量值网格”****。  
  
2.  单击“Sales Order Number”**** 列标题。  
  
3.  在工具栏上，单击“自动求和”按钮 (**∑**) 旁边的向下箭头，并选择“DistinctCountDistinctCount”。****  
  
     “自动求和”功能会自动使用 DistinctCount 标准聚合公式为所选的列创建一个度量值。  
  
     请注意，度量值网格中该列之下的顶部单元现包含度量值名称 **Distinct Count Sales Order Number**。 使用“自动求和”功能创建的度量值将自动放入关联列下方度量值网格中的最顶部单元中。  
  
4.  在度量值网格中，单击新度量值，然后在“属性”**** 窗口的“度量值名称”**** 中，将度量值重命名为 **Internet Distinct Count Sales Order**。  
  
#### <a name="to-create-additional-measures-in-the-internet-sales-table"></a>在 Internet Sales 表中创建额外的度量值  
  
1.  使用“自动求和”功能创建并命名以下度量值：  
  
    |“度量值名称”|列|自动求和 (∑)|公式|  
    |------------------|------------|-------------------|-------------|  
    |Internet Order Lines Count|Sales Order Line Number|Count|=COUNT([Sales Order Line Number])|  
    |Internet Total Units|Order Quantity|SUM|=SUM([Order Quantity])|  
    |Internet Total Discount Amount|Discount Amount|SUM|=SUM([Discount Amount])|  
    |Internet Total Product Cost|Total Product Cost|SUM|=SUM([Total Product Cost])|  
    |Internet Total Sales|Sales Amount|SUM|=SUM([Sales Amount])|  
    |Internet Total Margin|Margin|SUM|=SUM([Margin])|  
    |Internet Total Tax Amt|税额|SUM|=SUM([Tax Amt])|  
    |Internet Total Freight|Freight|SUM|=SUM([Freight])|  
  
2.  通过在度量值网格中单击一个空单元并使用编辑栏，创建并命名以下度量值：  
  
    > [!IMPORTANT]  
    >  您必须按顺序创建下列度量值；后面度量值中的公式引用较早的度量值。  
  
    |“度量值名称”|公式|  
    |------------------|-------------|  
    |Internet Previous Quarter Margin|=CALCULATE([Internet Total Margin],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Margin|=TOTALQTD([Internet Total Margin],'Date'[Date])|  
    |Internet Previous Quarter Margin Proportion to QTD|=[Internet Previous Quarter Margin]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
    |Internet Previous Quarter Sales|=CALCULATE([Internet Total Sales],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Sales|=TOTALQTD([Internet Total Sales],'Date'[Date])|  
    |Internet Previous Quarter Sales Proportion to QTD|=[Internet Previous Quarter Sales]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
  
 为 Internet Sales 表创建的度量值可用来分析关键的财务数据，如用户选择的筛选器定义的物料的销售、成本和毛利润率。  
  
## <a name="next-step"></a>下一步  
 若要继续学习本教程，请转到下一课：[第 8 课：创建关键绩效指标](lesson-7-create-key-performance-indicators.md)。  
  
  
