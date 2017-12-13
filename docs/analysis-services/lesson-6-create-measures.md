---
title: "第 7 课： 创建度量值 |Microsoft 文档"
ms.custom: 
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 28d9d9b4cda3c97a555cce45db525cfb4a6c26f5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="lesson-6-create-measures"></a>第 6 课： 创建度量值
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课中，您将创建要包括在您的模型中的度量值。 与你在上一课中创建计算列类似，度量值是通过使用 DAX 公式创建计算。 但是，与计算列不同，度量值是基于用户选择的 *筛选器*进行计算的；例如，添加到数据透视表中的“行标签”字段中的特定列或切片器。 然后，由所应用的度量值计算出筛选器中每个单元的值。 度量值是功能强大、 灵活的计算，想要包括在几乎所有表格模型中来对数值数据执行动态计算。 若要了解详细信息，请参阅[度量值](../analysis-services/tabular-models/measures-ssas-tabular.md)。  
  
若要创建度量值，你将使用*度量值网格*。 默认情况下，每个表都有一个空的度量值网格；但是，您通常不会为每个表创建度量值。 在数据视图中时，度量值网格显示在模型设计器中的表下方。 若要隐藏或显示表的度量值网格，请单击“表”  菜单，然后单击“显示度量值网格” 。  
  
您可以通过在度量值网格中单击一个空单元，然后在编辑栏中键入 DAX 公式，以创建度量值。 在您单击 Enter 完成公式后，该度量值将显示在单元中。 还可以使用标准聚合函数创建度量值，方法是单击某列，然后单击工具栏上的“自动求和”按钮 (**∑**)。 使用自动求和功能创建的度量值将显示在列中，正下方的度量值网格单元格，但可以移动。  
  
在本课中，您将通过在编辑栏中输入一个 DAX 公式并使用“自动求和”功能来创建度量值。  
  
学完本课的估计时间： **30 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 之前在本课程中执行任务，你应完成上一课：[第 5 课： 创建计算列](../analysis-services/lesson-5-create-calculated-columns.md)。  
  
## <a name="create-measures"></a>创建度量值  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>DimDate 表中创建 DaysCurrentQuarterToDate 度量值  
  
1.  在模型设计器中，单击**DimDate**表。  
  
2.  在度量值网格中，单击左上方的空单元。  
  
3.  在公式栏中，键入以下公式：  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    请注意左上角单元格现在包含度量值名称， **DaysCurrentQuarterToDate**后, 跟结果， **92**。
    
      ![作为-表格-lesson6-newmeasure](../analysis-services/media/as-tabular-lesson6-newmeasure.png) 
    
    与计算列，不同的度量值公式可以键入度量值名称后, 跟逗号后, 跟公式的表达式。

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>DimDate 表中创建 DaysInCurrentQuarter 度量值  
  
1.  与**DimDate**表仍处于活动状态的度量值网格在模型设计器中，单击刚创建的度量值下的空单元格。  
  
2.  在公式栏中，键入以下公式：  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    当创建一个不完整期间与前一个期间的比率时，公式必须考虑期间中已消逝的比例，并将其与前一期间中的同一比例进行比较。 在这种情况下，[DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 提供比例已用在当前期间。  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>若要在 FactInternetSales 表中创建 InternetDistinctCountSalesOrder 度量值  
  
1.  单击**FactInternetSales**表。   
  
2.  单击**SalesOrderNumber**列标题。  
  
3.  在工具栏上，单击“自动求和”(**∑**) 按钮旁边的向下箭头，然后选择“DistinctCount” 。  
  
    “自动求和”功能使用 DistinctCount 标准聚合公式自动为所选列创建度量值。  
    
       ![作为-表格-lesson6-newmeasure2](../analysis-services/media/as-tabular-lesson6-newmeasure2.png)
  
4.  在度量值网格中，单击新建度量值，然后在**属性**窗口，请在**度量值名称**，重命名为度量值**InternetDistinctCountSalesOrder**。 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>若要在 FactInternetSales 表中创建其他度量值  
  
1.  通过使用“自动求和”功能，创建和命名下列度量值：  
  
    |“度量值名称”|列|自动求和 (∑)|公式|  
    |----------------|----------|-----------------|-----------|  
    |InternetOrderLinesCount|SalesOrderLineNumber|Count|=COUNTA([SalesOrderLineNumber])|  
    |InternetTotalUnits|OrderQuantity|Sum|=SUM([OrderQuantity])|  
    |InternetTotalDiscountAmount|DiscountAmount|Sum|=SUM([DiscountAmount])|  
    |InternetTotalProductCost|TotalProductCost|Sum|=SUM([TotalProductCost])|  
    |InternetTotalSales|SalesAmount|Sum|=SUM([SalesAmount])|  
    |InternetTotalMargin|Margin|Sum|=SUM([Margin])|  
    |InternetTotalTaxAmt|TaxAmt|Sum|=SUM([TaxAmt])|  
    |InternetTotalFreight|Freight|Sum|=SUM([Freight])|  
  
2.  通过单击的空白单元格中度量值网格中，以及通过使用公式栏中，创建并命名顺序中的以下度量值：  
  
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
转到下一课：[第七课： 创建关键绩效指标](../analysis-services/lesson-7-create-key-performance-indicators.md)。  

  
