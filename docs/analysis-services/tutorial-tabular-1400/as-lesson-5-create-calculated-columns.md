---
title: Analysis Services 教程第 5 课： 创建计算的列 |Microsoft Docs
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58a7f38dbbe7a68668418db4d1bef16e08784a08
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43063856"
---
# <a name="create-calculated-columns"></a>创建计算列

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，您创建数据模型中通过添加计算的列。 可以创建计算的列 （作为自定义列） 使用获取数据时，通过使用查询编辑器中，或更高版本在模型设计器类似于您做。 若要了解详细信息，请参阅[计算列](../tabular-models/ssas-calculated-columns.md)。
  
在三个不同表中创建五个新的计算的列。 步骤略有不同的显示有几种方法创建的列、 重命名它们，并将它们放在表中的不同位置中的每个任务。  

本课程也是首次使用数据分析表达式 (DAX)。 DAX 是一种特殊语言用于创建表格模型的可高度自定义公式表达式。 在本教程中，使用 DAX 创建计算的列、 度量值和角色筛选器。 若要了解详细信息，请参阅[表格模型中的 DAX](../tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)。 
  
学完本课的估计时间： **15 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文是表格建模教程应按顺序完成的一部分。 在之前在本课程中执行的任务，您应已完成上一课：[第 4 课： 创建关系](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)。 
  
## <a name="create-calculated-columns"></a>创建计算列  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>在 DimDate 表中创建 MonthCalendar 计算的列  
  
1.  单击**模型**菜单 >**模型视图** > **数据视图**。  
  
    只能在数据视图中使用模型设计器创建计算列。  
  
2.  在模型设计器中，单击**DimDate**表 （选项卡）。  
  
3.  右键单击**CalendarQuarter**列标题，并单击**插入列**。  
  
    一个名为“Calculated Column 1”的新列插入到“Calendar Quarter”列的左侧。  
  
4.  在表上方公式栏中键入以下 DAX 公式： 记忆式键入功能可帮助你键入的完全限定的名称的列和表，并列出可用的函数。  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    然后，将为计算列中的所有行填充值。 如果向下滚动表，将看到行可以具有不同的值为本专栏中，基于每个行中的数据。    
  
5.  为此列重命名**MonthCalendar**。 

    ![as-lesson5-newcolumn](../tutorial-tabular-1400/media/as-lesson5-newcolumn.png) 
  
MonthCalendar 计算列提供可排序的月份名称。  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>在 DimDate 表中创建 DayOfWeek 计算的列  
  
1.  与**DimDate**表仍处于活动状态，单击**列**菜单，并单击**添加列**。  
  
2.  在公式栏中，键入以下公式：  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    完成公式的建立后，按 ENTER。 新列将添加到表的最右侧。  
  
3.  为此列重命名**DayOfWeek**。  
  
4.  单击列标题，并拖动列之间**EnglishDayNameOfWeek**列和**DayNumberOfMonth**列。  
  
    > [!TIP]  
    > 移动表中的列可使表变得更易于浏览。  
  
DayOfWeek 计算列提供可排序的星期几名称。  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>在 DimProduct 表中创建 ProductSubcategoryName 计算的列  
  
  
1.  在中**DimProduct**表中，滚动到最右侧的表。 请注意，最右侧的列被命名为“添加列”（斜体），单击该列标题。  
  
2.  在公式栏中，键入以下公式：  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  为此列重命名**ProductSubcategoryName**。  
  
ProductSubcategoryName 计算的列用于在 DimProduct 表中，其中包括 DimProductSubcategory 表的 EnglishProductSubcategoryName 列中的数据创建层次结构。 层次结构不能跨多个表。 稍后在第 9 课中创建层次结构。  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>在 DimProduct 表中创建 ProductCategoryName 计算的列  
  
1.  与**DimProduct**表仍处于活动状态，单击**列**菜单，并单击**添加列**。  
  
2.  在公式栏中，键入以下公式：  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  为此列重命名**ProductCategoryName**。  
  
ProductCategoryName 计算的列用于在 DimProduct 表中，其中包括 DimProductCategory 表的 EnglishProductCategoryName 列中的数据创建层次结构。 层次结构不能跨多个表。  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>在 FactInternetSales 表中创建 Margin 计算的列  
  
1.  在模型设计器中，选择**FactInternetSales**表。  
  
2.  创建新的计算的列之间**SalesAmount**列和**TaxAmt**列。  
  
3.  在公式栏中，键入以下公式：  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  将此列重命名为“Margin”。  
 
      ![as-lesson5-newmargin](../tutorial-tabular-1400/media/as-lesson5-newmargin.png)
      
    Margin 计算的列用于分析的每个销售的毛利润率。  
  
## <a name="whats-next"></a>下一步是什么？

[第 6 课： 创建度量值](../tutorial-tabular-1400/as-lesson-6-create-measures.md)。
  
  
  
