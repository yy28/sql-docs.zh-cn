---
title: Analysis Services 教程第 6 课：创建度量值 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 715fe6144cc430e545feb3c484d148531cff6ec9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207351"
---
# <a name="create-measures"></a>创建度量值

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，将创建要包含在模型中度量值。 与你创建的计算列类似，度量值是通过使用 DAX 公式创建的计算。 但是，与计算列不同的度量值计算基于所选的用户*筛选器*。 例如，特定列或切片器添加到数据透视表中的行标签字段。 然后，由所应用的度量值计算出筛选器中每个单元的值。 度量值是你想要包括在几乎所有表格模型中以对数值数据执行动态计算的功能强大、 灵活的计算。 若要了解详细信息，请参阅[度量值](../tabular-models/measures-ssas-tabular.md)。
  
若要创建度量值，请使用*度量值网格*。 默认情况下，每个表具有一个空的度量值网格;但是，您通常不要创建每个表的度量值。 在数据视图中时，度量值网格显示在模型设计器中的表下方。 若要隐藏或显示表的度量值网格，请单击“表”  菜单，然后单击“显示度量值网格”  。  
  
可以通过单击度量值网格中的空单元格，然后在编辑栏中键入一个 DAX 公式创建度量值。 当您单击 ENTER 填写公式，该度量值会显示在单元格。 您还可以创建度量值使用标准聚合函数，通过单击某个列，然后单击自动求和按钮 (**∑**) 工具栏上。 使用自动求和功能创建的度量值显示在列下方的度量值网格单元格中，但可以移动。  
  
在本课中，您将创建度量值，通过这两个输入 DAX 公式在公式栏中，并使用自动求和功能。  
  
估计的时间才能完成本课程中：**30 分钟**  
  
## <a name="prerequisites"></a>系统必备  

本文是表格建模教程应按顺序完成的一部分。 执行任务之前在本课程中，您应当已完成上一课：[第 5 课：创建计算的列](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)。  
  
## <a name="create-measures"></a>创建度量值  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>在 DimDate 表中创建 DaysCurrentQuarterToDate 度量值  
  
1.  在模型设计器中，单击**DimDate**表。  
  
2.  在度量值网格中，单击左上方的空单元。  
  
3.  在公式栏中，键入以下公式：  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    请注意，左上角单元格现在包含度量值名称， **DaysCurrentQuarterToDate**后, 跟结果**92**。 结果不相关现在因为应用用户筛选器。
    
      ![as-lesson6-newmeasure](../tutorial-tabular-1400/media/as-lesson6-newmeasure.png) 
    
    与计算列不同使用度量值公式可以键入度量值名称后, 跟一个冒号和公式表达式。

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>在 DimDate 表中创建 DaysInCurrentQuarter 度量值  
  
1.  与**DimDate**表在模型设计器中，度量值网格中仍处于活动状态中，单击你创建的度量值下方的空单元格。  
  
2.  在公式栏中，键入以下公式：  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    当创建一个不完整期间与前一期间之间的比率。 该公式必须计算已过，并且将其与相同的比例比较在以前的时间段中的时间段的比例。 在这种情况下，[DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 给出比例当前期间中已消逝。  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>若要在 FactInternetSales 表中创建 InternetDistinctCountSalesOrder 度量值  
  
1.  单击**FactInternetSales**表。   
  
2.  单击**SalesOrderNumber**列标题。  
  
3.  在工具栏上，单击“自动求和”(**∑**) 按钮旁边的向下箭头，然后选择“DistinctCount”  。  
  
    “自动求和”功能使用 DistinctCount 标准聚合公式自动为所选列创建度量值。  
    
       ![as-lesson6-newmeasure2](../tutorial-tabular-1400/media/as-lesson6-newmeasure2.png)
  
4.  在度量值网格中，单击新建度量值，然后在**属性**窗口，请在**度量值名称**，重命名度量值到**InternetDistinctCountSalesOrder**。 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>若要在 FactInternetSales 表中创建其他度量值  
  
1.  通过使用“自动求和”功能，创建和命名下列度量值：  

    |“列”|度量值名称|自动求和 (∑)|公式|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|Sum|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|Sum|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|Sum|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|Sum|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|Sum|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|Sum|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|Sum|=SUM([Freight])|  
  
2.  通过单击度量值网格中的空单元格并使用公式栏中，创建，按顺序的以下自定义度量值：  
  
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
  
对于 FactInternetSales 表创建的度量值可以用于分析关键财务数据，例如销售额、 成本和毛利润率的用户所选筛选器定义的项。  
  
## <a name="whats-next"></a>下一步是什么？

[第 7 课：创建关键绩效指标](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)。  

  
