---
title: "第 6 课： 创建计算的列 |Microsoft 文档"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: be1b5d0bbe08a51ec4ffd6873a8f8295125d13db
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-5-create-calculated-columns"></a>第 5 课： 创建计算的列
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课中，您将通过添加计算列在模型中创建新数据。 计算列基于模型中的现有数据。 若要了解详细信息，请参阅[计算列](../analysis-services/tabular-models/ssas-calculated-columns.md)。  
  
您将在三个不同的表中创建五个新的计算列。 步骤对于每个任务略有不同。 此处介绍创建新列、重命名这些列以及将它们放入表中不同位置的多种方法。  
  
学完本课的估计时间： **15 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 之前在本课程中执行任务，你应完成上一课：[第 4 课： 创建关系](../analysis-services/lesson-4-create-relationships.md)。 
  
## <a name="create-calculated-columns"></a>创建计算列  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>DimDate 表中创建 MonthCalendar 计算的列  
  
1.  单击**模型**菜单 >**模型视图** > **数据视图**。  
  
    只能在数据视图中使用模型设计器创建计算列。  
  
2.  在模型设计器中，单击**DimDate**表 （选项卡）。  
  
3.  右键单击**CalendarQuarter**列标题并单击**插入列**。  
  
    一个名为“Calculated Column 1”的新列插入到“Calendar Quarter”列的左侧。  
  
4.  在表上面的编辑栏中，键入以下公式。 自动完成功能将帮助您键入列和表的完全限定名称，并且列出可用的函数。  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    然后，将为计算列中的所有行填充值。 如果在表中向下滚动，将看到行对于此列可以具有不同的值（基于每行中的数据）。    
  
5.  该列重命名为**MonthCalendar**。 

    ![作为-表格-lesson5-newcolumn](../analysis-services/media/as-tabular-lesson5-newcolumn.png) 
  
MonthCalendar 计算列提供的可排序月份名称。  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>DimDate 表中创建 DayOfWeek 计算的列  
  
1.  与**DimDate**表仍处于活动状态，请单击**列**菜单，，然后单击**添加列**。  
  
2.  在公式栏中，键入以下公式：  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    在构建公式完后，按 ENTER。 新列将添加到表的最右侧。  
  
3.  重命名为列**DayOfWeek**。  
  
4.  在列标题中，单击并拖动列之间**EnglishDayNameOfWeek**列和**DayNumberOfMonth**列。  
  
    > [!TIP]  
    > 移动表中的列可使表变得更易于浏览。  
  
DayOfWeek 计算列提供的可排序日期星期几名称。  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>在中的 DimProduct 表中创建 ProductSubcategoryName 计算的列  
  
  
1.  在**DimProduct**表中，滚动到最右侧的表。 请注意，最右侧的列被命名为“添加列”（斜体），单击该列标题。  
  
2.  在公式栏中，键入以下公式。  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  重命名为列**ProductSubcategoryName**。  
  
ProductSubcategoryName 计算的列用于在将其包括 EnglishProductSubcategoryName 列的数据在 DimProductSubcategory 表中的 DimProduct 表中创建层次结构。 层次结构不能跨多个表。 将更高版本在 Lesson 9 创建层次结构。  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>在中的 DimProduct 表中创建 ProductCategoryName 计算的列  
  
1.  与**DimProduct**表仍处于活动状态，单击**列**菜单，，然后单击**添加列**。  
  
2.  在公式栏中，键入以下公式：  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  重命名为列**ProductCategoryName**。  
  
ProductCategoryName 计算的列用于在将其包括 EnglishProductCategoryName 列的数据在 DimProductCategory 表中的 DimProduct 表中创建层次结构。 层次结构不能跨多个表。  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>在 FactInternetSales 表中创建边距计算的列  
  
1.  在模型设计器中，选择**FactInternetSales**表。  
  
2.  添加新列。  
  
3.  在公式栏中，键入以下公式：  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  将此列重命名为“Margin”。  
  
5.  将列之间拖动**SalesAmount**列和**TaxAmt**列。 
 
      ![作为-表格-lesson5-newmargin](../analysis-services/media/as-tabular-lesson5-newmargin.png)
      
    边距计算的列用于分析每个销售的利润边距。  
  
## <a name="whats-next"></a>下一步是什么？
转到下一课： [6 课： 创建度量值](../analysis-services/lesson-6-create-measures.md)。
  
  
  
