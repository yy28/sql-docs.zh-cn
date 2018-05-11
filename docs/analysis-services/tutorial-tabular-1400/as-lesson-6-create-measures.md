---
title: Analysis Services 教程第 6 课： 创建度量值 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fcb305b93d90d83975701e0943542b95ea6c244e
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="create-measures"></a>创建度量值

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，你可以创建您的模型中包含度量值。 类似于你创建的计算列，度量值是通过使用 DAX 公式创建计算。 但是，与不同的是计算列，来计算度量值基于用户所选*筛选器*。 例如，一个特定列或切片器添加到数据透视表中的行标签字段。 然后，由所应用的度量值计算出筛选器中每个单元的值。 度量值是你想要在几乎所有的表格模型，以对数值数据执行动态计算中包括的功能强大、 灵活的计算。 若要了解详细信息，请参阅[度量值](../tabular-models/measures-ssas-tabular.md)。
  
若要创建的度量值，请使用*度量值网格*。 默认情况下，每个表具有空度量值网格;但是，你通常不要创建每个表的度量值。 在数据视图中时，度量值网格显示在模型设计器中的表下方。 若要隐藏或显示表的度量值网格，请单击“表”  菜单，然后单击“显示度量值网格” 。  
  
你可以通过单击的空白单元格中度量值网格中，然后在公式栏中键入 DAX 公式创建度量值。 当你单击 ENTER 填写公式中，度量值，然后显示的单元格中。 你还可以创建通过单击列，然后单击自动求和按钮使用标准聚合函数的度量值 (**∑**) 在工具栏上。 使用自动求和功能创建的度量值显示在列中，正下方的度量值网格单元格，但可以移动。  
  
在本课程中，你将创建度量值，通过这两个输入 DAX 公式在公式栏中，并通过使用自动求和功能。  
  
学完本课的估计时间： **30 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文摘自表格建模教程中，应按顺序完成。 之前在本课程中执行任务，你应完成上一课：[第 5 课： 创建计算的列](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)。  
  
## <a name="create-measures"></a>创建度量值  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>DimDate 表中创建 DaysCurrentQuarterToDate 度量值  
  
1.  在模型设计器中，单击**DimDate**表。  
  
2.  在度量值网格中，单击左上方的空单元。  
  
3.  在公式栏中，键入以下公式：  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    请注意左上角单元格现在包含度量值名称， **DaysCurrentQuarterToDate**后, 跟结果， **92**。 结果是不相关此时因为任何用户筛选器已不应用。
    
      ![作为 lesson6 newmeasure](../tutorial-tabular-1400/media/as-lesson6-newmeasure.png) 
    
    与计算列，不同的度量值公式可以键入度量值名称后, 跟冒号后, 跟公式的表达式。

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>DimDate 表中创建 DaysInCurrentQuarter 度量值  
  
1.  与**DimDate**表的度量值网格在模型设计器中仍处于活动状态，请单击下你创建的度量值的空单元格。  
  
2.  在公式栏中，键入以下公式：  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    当创建一个不完整期间与以前的时间段之间的比率。 该公式必须计算已过，并且将其与相同的比例比较在以前的时间段中的段的比例。 在这种情况下，[DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 提供比例已用在当前期间。  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>若要在 FactInternetSales 表中创建 InternetDistinctCountSalesOrder 度量值  
  
1.  单击**FactInternetSales**表。   
  
2.  单击**SalesOrderNumber**列标题。  
  
3.  在工具栏上，单击“自动求和”(**∑**) 按钮旁边的向下箭头，然后选择“DistinctCount” 。  
  
    “自动求和”功能使用 DistinctCount 标准聚合公式自动为所选列创建度量值。  
    
       ![as-lesson6-newmeasure2](../tutorial-tabular-1400/media/as-lesson6-newmeasure2.png)
  
4.  在度量值网格中，单击新建度量值，然后在**属性**窗口，请在**度量值名称**，重命名为度量值**InternetDistinctCountSalesOrder**。 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>若要在 FactInternetSales 表中创建其他度量值  
  
1.  通过使用“自动求和”功能，创建和命名下列度量值：  

    |列|度量值名称|自动求和 (∑)|公式|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|SUM|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|SUM|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|SUM|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|SUM|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|SUM|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|SUM|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|SUM|=SUM([Freight])|  
  
2.  通过单击的空白单元格中度量值网格中，以及通过使用公式栏中，创建，下列顺序的自定义度量值：  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
为 FactInternetSales 表创建的度量值可以用于分析关键财务数据，例如销售、 成本和利润率由用户选定的筛选器定义的项。  
  
## <a name="whats-next"></a>下一步是什么？

[第 7 课： 创建关键绩效指标](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)。  

  
