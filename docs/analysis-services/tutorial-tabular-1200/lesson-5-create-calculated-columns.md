---
title: 第 5 课：创建计算的列 |Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df9b5a6d490b33b9aea786290acb7454d0066453
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404179"
---
# <a name="lesson-5-create-calculated-columns"></a>第 5 课：创建计算列
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课中，您将通过添加计算列在模型中创建新数据。 计算列基于模型中的现有数据。 若要了解详细信息，请参阅[计算列](../tabular-models/ssas-calculated-columns.md)。  
  
您将在三个不同的表中创建五个新的计算列。 步骤对于每个任务略有不同。 此处介绍创建新列、重命名这些列以及将它们放入表中不同位置的多种方法。  
  
估计的时间才能完成本课程中：**15 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 执行任务之前在本课程中，您应当已完成上一课：[第 4 课：创建关系](lesson-4-create-relationships.md)。 
  
## <a name="create-calculated-columns"></a>创建计算列  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>在 DimDate 表中创建 MonthCalendar 计算的列  
  
1.  单击**模型**菜单 >**模型视图** > **数据视图**。  
  
    只能在数据视图中使用模型设计器创建计算列。  
  
2.  在模型设计器中，单击**DimDate**表 （选项卡）。  
  
3.  右键单击**CalendarQuarter**列标题，并单击**插入列**。  
  
    一个名为“Calculated Column 1”的新列插入到“Calendar Quarter”列的左侧。  
  
4.  在表上面的编辑栏中，键入以下公式。 自动完成功能将帮助您键入列和表的完全限定名称，并且列出可用的函数。  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    然后，将为计算列中的所有行填充值。 如果在表中向下滚动，将看到行对于此列可以具有不同的值（基于每行中的数据）。    
  
5.  为此列重命名**MonthCalendar**。 

    ![as-tabular-lesson5-newcolumn](media/as-tabular-lesson5-newcolumn.png) 
  
MonthCalendar 计算列提供可排序的月份名称。  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>在 DimDate 表中创建 DayOfWeek 计算的列  
  
1.  与**DimDate**表仍处于活动状态时，单击**列**菜单，并单击**添加列**。  
  
2.  在公式栏中，键入以下公式：  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    完成公式的建立后，按 ENTER。 新列将添加到表的最右侧。  
  
3.  为此列重命名**DayOfWeek**。  
  
4.  列标题中，单击并拖动列之间**EnglishDayNameOfWeek**列和**DayNumberOfMonth**列。  
  
    > [!TIP]  
    > 移动表中的列可使表变得更易于浏览。  
  
DayOfWeek 计算列提供可排序的星期几名称。  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>在 DimProduct 表中创建 ProductSubcategoryName 计算的列  
  
  
1.  在中**DimProduct**表中，滚动到最右侧的表。 请注意，最右侧的列被命名为“添加列”（斜体），单击该列标题。  
  
2.  在公式栏中，键入以下公式。  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  为此列重命名**ProductSubcategoryName**。  
  
ProductSubcategoryName 计算的列用于在 DimProduct 表，其中包括 DimProductSubcategory 表的 EnglishProductSubcategoryName 列中的数据中创建层次结构。 层次结构不能跨多个表。 将稍后在第 9 课中创建层次结构。  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>在 DimProduct 表中创建 ProductCategoryName 计算的列  
  
1.  与**DimProduct**表仍处于活动状态，单击**列**菜单，并单击**添加列**。  
  
2.  在公式栏中，键入以下公式：  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  为此列重命名**ProductCategoryName**。  
  
ProductCategoryName 计算的列用于在 DimProduct 表，其中包括 DimProductCategory 表的 EnglishProductCategoryName 列中的数据中创建层次结构。 层次结构不能跨多个表。  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>在 FactInternetSales 表中创建 Margin 计算的列  
  
1.  在模型设计器中，选择**FactInternetSales**表。  
  
2.  添加新列。  
  
3.  在公式栏中，键入以下公式：  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  将此列重命名为“Margin”。  
  
5.  将列之间拖动**SalesAmount**列和**TaxAmt**列。 
 
      ![as-tabular-lesson5-newmargin](media/as-tabular-lesson5-newmargin.png)
      
    Margin 计算的列用于分析的每个销售的毛利润率。  
  
## <a name="whats-next"></a>下一步是什么？
请转到下一课：[第 6 课：创建度量值](lesson-6-create-measures.md)。
  
  
  
