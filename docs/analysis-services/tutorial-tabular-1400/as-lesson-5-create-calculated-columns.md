---
title: "Analysis Services 教程第 5 课： 创建计算的列 |Microsoft 文档"
description: "描述如何在 Analysis Services tutorial 项目中创建计算的列。"
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: daed9d78d8b88bcf8088d8b19b4a34ba3a9f16c0
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2018
---
# <a name="create-calculated-columns"></a>创建计算列

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，你通过创建数据在模型中添加计算的列。 你可以创建计算的列 （作为自定义列） 时使用获取数据，使用查询编辑器中，或更高版本在模型设计器类似你在此处执行操作。 若要了解详细信息，请参阅[计算列](../tabular-models/ssas-calculated-columns.md)。
  
在三个不同的表创建五个新的计算的列。 步骤会略有不同的演示通过多种方式创建列，请重命名它们，并将其放在各种位置表中每个任务。  

本课程中也是您首次使用数据分析表达式 (DAX)。 DAX 是一种特殊语言来创建的表格模型可高度自定义公式的表达式。 在本教程中，你可以使用 DAX 创建计算的列、 度量值和角色筛选器。 若要了解详细信息，请参阅[表格模型中的 DAX](../tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)。 
  
学完本课的估计时间： **15 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文摘自表格建模教程中，应按顺序完成。 之前在本课程中执行任务，你应完成上一课：[第 4 课： 创建关系](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)。 
  
## <a name="create-calculated-columns"></a>创建计算列  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>DimDate 表中创建 MonthCalendar 计算的列  
  
1.  单击**模型**菜单 >**模型视图** > **数据视图**。  
  
    只能在数据视图中使用模型设计器创建计算列。  
  
2.  在模型设计器中，单击**DimDate**表 （选项卡）。  
  
3.  右键单击**CalendarQuarter**列标题并单击**插入列**。  
  
    一个名为“Calculated Column 1”的新列插入到“Calendar Quarter”列的左侧。  
  
4.  在表上方公式栏中，键入以下 DAX 公式： 记忆式键入功能可帮助你键入的完全限定的名称的列和表，并列出可用的函数。  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    然后，将为计算列中的所有行填充值。 如果你向下滚动浏览表，你将看到行可以具有不同的值，此列，在基于每个行中的数据。    
  
5.  该列重命名为**MonthCalendar**。 

    ![as-lesson5-newcolumn](../tutorial-tabular-1400/media/as-lesson5-newcolumn.png) 
  
MonthCalendar 计算列提供的可排序月份名称。  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>DimDate 表中创建 DayOfWeek 计算的列  
  
1.  与**DimDate**表仍处于活动状态，单击**列**菜单，，然后单击**添加列**。  
  
2.  在公式栏中，键入以下公式：  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    在构建公式完后，按 ENTER。 新列将添加到表的最右侧。  
  
3.  重命名为列**DayOfWeek**。  
  
4.  单击列标题，并拖动列之间**EnglishDayNameOfWeek**列和**DayNumberOfMonth**列。  
  
    > [!TIP]  
    > 移动表中的列可使表变得更易于浏览。  
  
DayOfWeek 计算列提供的可排序日期星期几名称。  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>在中的 DimProduct 表中创建 ProductSubcategoryName 计算的列  
  
  
1.  在**DimProduct**表中，滚动到最右侧的表。 请注意，最右侧的列被命名为“添加列”（斜体），单击该列标题。  
  
2.  在公式栏中，键入以下公式：  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  重命名为列**ProductSubcategoryName**。  
  
ProductSubcategoryName 计算的列用于在 DimProduct 表中，将其包括在 DimProductSubcategory 表的 EnglishProductSubcategoryName 列的数据创建层次结构。 层次结构不能跨多个表。 更高版本在 Lesson 9 创建层次结构。  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>在中的 DimProduct 表中创建 ProductCategoryName 计算的列  
  
1.  与**DimProduct**表仍处于活动状态，单击**列**菜单，，然后单击**添加列**。  
  
2.  在公式栏中，键入以下公式：  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  重命名为列**ProductCategoryName**。  
  
ProductCategoryName 计算的列用于在 DimProduct 表中，将其包括在 DimProductCategory 表的 EnglishProductCategoryName 列的数据创建层次结构。 层次结构不能跨多个表。  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>在 FactInternetSales 表中创建边距计算的列  
  
1.  在模型设计器中，选择**FactInternetSales**表。  
  
2.  创建新的计算的列之间**SalesAmount**列和**TaxAmt**列。  
  
3.  在公式栏中，键入以下公式：  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  将此列重命名为“Margin”。  
 
      ![as-lesson5-newmargin](../tutorial-tabular-1400/media/as-lesson5-newmargin.png)
      
    边距计算的列用于分析每个销售的利润边距。  
  
## <a name="whats-next"></a>下一步是什么？

[第 6 课： 创建度量值](../tutorial-tabular-1400/as-lesson-6-create-measures.md)。
  
  
  
