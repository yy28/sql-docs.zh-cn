---
title: 第 6 课：创建度量值 |Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f8ad53f78acb862101ff633f663ea03198825ab
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404659"
---
# <a name="lesson-6-create-measures"></a>第 6 课：创建度量值
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课中，您将创建要包括在您的模型中的度量值。 与上一课中创建的计算列类似，度量值是通过使用 DAX 公式创建的计算。 但是，与计算列不同，度量值是基于用户选择的 *筛选器*进行计算的；例如，添加到数据透视表中的“行标签”字段中的特定列或切片器。 然后，由所应用的度量值计算出筛选器中每个单元的值。 度量值是想要包括在几乎所有表格模型中以对数值数据执行动态计算的功能强大、 灵活的计算。 若要了解详细信息，请参阅[度量值](../tabular-models/measures-ssas-tabular.md)。  
  
若要创建度量值，将使用*度量值网格*。 默认情况下，每个表都有一个空的度量值网格；但是，您通常不会为每个表创建度量值。 在数据视图中时，度量值网格显示在模型设计器中的表下方。 若要隐藏或显示表的度量值网格，请单击“表”  菜单，然后单击“显示度量值网格” 。  
  
您可以通过在度量值网格中单击一个空单元，然后在编辑栏中键入 DAX 公式，以创建度量值。 在您单击 Enter 完成公式后，该度量值将显示在单元中。 还可以使用标准聚合函数创建度量值，方法是单击某列，然后单击工具栏上的“自动求和”按钮 (**∑**)。 使用自动求和功能创建的度量值将显示在列下方的度量值网格单元格中，但可以移动。  
  
在本课中，您将通过在编辑栏中输入一个 DAX 公式并使用“自动求和”功能来创建度量值。  
  
估计的时间才能完成本课程中：**30 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 执行任务之前在本课程中，您应当已完成上一课：[第 5 课：创建计算的列](lesson-5-create-calculated-columns.md)。  
  
## <a name="create-measures"></a>创建度量值  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>在 DimDate 表中创建 DaysCurrentQuarterToDate 度量值  
  
1.  在模型设计器中，单击**DimDate**表。  
  
2.  在度量值网格中，单击左上方的空单元。  
  
3.  在公式栏中，键入以下公式：  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    请注意，左上角单元格现在包含度量值名称， **DaysCurrentQuarterToDate**后, 跟结果**92**。
    
      ![as-tabular-lesson6-newmeasure](media/as-tabular-lesson6-newmeasure.png) 
    
    与计算列不同使用度量值公式可以键入度量值名称后, 跟一个逗号后, 跟公式表达式。

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>在 DimDate 表中创建 DaysInCurrentQuarter 度量值  
  
1.  与**DimDate**表在模型设计器中，度量值网格中仍处于活动状态中，单击刚创建的度量值下方的空单元格。  
  
2.  在公式栏中，键入以下公式：  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    当创建一个不完整期间与前一个期间的比率时，公式必须考虑期间中已消逝的比例，并将其与前一期间中的同一比例进行比较。 在这种情况下，[DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 给出比例当前期间中已消逝。  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>若要在 FactInternetSales 表中创建 InternetDistinctCountSalesOrder 度量值  
  
1.  单击**FactInternetSales**表。   
  
2.  单击**SalesOrderNumber**列标题。  
  
3.  在工具栏上，单击“自动求和”(**∑**) 按钮旁边的向下箭头，然后选择“DistinctCount” 。  
  
    “自动求和”功能使用 DistinctCount 标准聚合公式自动为所选列创建度量值。  
    
       ![as-tabular-lesson6-newmeasure2](media/as-tabular-lesson6-newmeasure2.png)
  
4.  在度量值网格中，单击新建度量值，然后在**属性**窗口，请在**度量值名称**，重命名度量值到**InternetDistinctCountSalesOrder**。 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>若要在 FactInternetSales 表中创建其他度量值  
  
1.  通过使用“自动求和”功能，创建和命名下列度量值：  
  
    |“度量值名称”|“列”|自动求和 (∑)|公式|  
    |----------------|----------|-----------------|-----------|  
    |InternetOrderLinesCount|SalesOrderLineNumber|Count|=COUNTA([SalesOrderLineNumber])|  
    |InternetTotalUnits|OrderQuantity|Sum|=SUM([OrderQuantity])|  
    |InternetTotalDiscountAmount|DiscountAmount|Sum|=SUM([DiscountAmount])|  
    |InternetTotalProductCost|TotalProductCost|Sum|=SUM([TotalProductCost])|  
    |InternetTotalSales|SalesAmount|Sum|=SUM([SalesAmount])|  
    |InternetTotalMargin|Margin|Sum|=SUM([Margin])|  
    |InternetTotalTaxAmt|TaxAmt|Sum|=SUM([TaxAmt])|  
    |InternetTotalFreight|Freight|Sum|=SUM([Freight])|  
  
2.  通过单击某个空单元格在度量值网格中，并使用公式栏，创建并命名以下度量值按顺序：  
  
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
请转到下一课：[第 7 课：创建关键绩效指标](lesson-7-create-key-performance-indicators.md)。  

  
