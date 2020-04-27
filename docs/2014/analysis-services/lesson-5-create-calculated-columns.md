---
title: 第6课：创建计算列 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58ba761f3e32f13ddcf81dc9875057195298c705
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66078563"
---
# <a name="lesson-6-create-calculated-columns"></a>第 6 课：创建计算列
  在本课中，将通过添加计算列在模型中创建新数据。 计算列基于模型中的现有数据。 了解详细信息，请参阅[计算列（SSAS 表格）](tabular-models/ssas-calculated-columns.md)。  
  
 将在三个不同的表中创建五个计算列。 步骤对于每个任务略有不同。 这是为了说明有多种方法可用来创建新列、对其进行重命名，以及将其放置在表中的各种位置。  
  
 学完本课的估计时间： **15 分钟**  
  
## <a name="prerequisites"></a>先决条件  
 本主题是表格建模教程的一部分，应当按顺序完成。 在执行本课程中的任务之前，须已完成上一课： [第 5 课：创建关系](lesson-4-create-relationships.md)。  
  
## <a name="create-calculated-columns"></a>创建计算列  
  
#### <a name="create-a-month-calendar-calculated-column-in-the-date-table"></a>在 Date 表中创建 Month Calendar 计算列  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“模型”**** 菜单，然后指向“模型视图”****，再单击“数据视图”****。  
  
     只能在数据视图中使用模型设计器创建计算列。  
  
2.  在模型设计器中，单击“Date”**** 表（选项卡）。  
  
3.  右键单击 "**日历季度**" 列，然后单击 "**插入列**"。  
  
     名为**CalculatedColumn1**的新列将插入到 "**日历季度**" 列的左侧。  
  
4.  在表上面的编辑栏中，键入以下公式。 “自动完成”可帮助你键入列和表的完全限定名称，并将列出可用的函数。  
  
     `=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]`  
  
     在您完成公式的建立后，按 Enter。  
  
     然后，会在计算列中为所有行填充值。 如果在表中向下滚动，会看到，根据每行中的数据，各行中的此列可能具有不同的值。  
  
    > [!NOTE]  
    >  如果收到错误提示，请验证确保公式中的列名与在 [第 3 课：重命名列](rename-columns.md)中更改的列名是否匹配。  
  
5.  将此列重`Month Calendar`命名为。  
  
 Month Calendar 计算列提供可排序的月份名称。  
  
#### <a name="create-a-day-of-week-calculated-column-in-the-date-table"></a>在 Date 表中创建 Day of Week 计算列  
  
1.  在“Date”**** 表仍处于活动状态时，单击“列”**** 菜单，然后单击“添加列”****。  
  
     一个新列添加到表的最右侧。  
  
2.  在公式栏中，键入以下公式：  
  
     `=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]`  
  
     在您完成公式的建立后，按 Enter。  
  
3.  将列重命名`Day of Week`为。  
  
4.  单击列标题，然后将此列拖到“Day Name”**** 列与“Day of Month”**** 列之间。  
  
    > [!TIP]  
    >  移动表中的列可使表变得更易于浏览。  
  
 Day of Week 计算列为周内的日期提供可排序的名称。  
  
#### <a name="create-a-product-subcategory-name-calculated-column-in-the-product-table"></a>在 Product 表中创建 Product Subcategory Name 计算列  
  
1.  在模型设计器中，选择“Product”**** 表。  
  
2.  滚动到表的最右侧。 请注意，最右侧的列名为“添加列”（斜体），单击列标题。****  
  
3.  在公式栏中，键入以下公式。  
  
     `=RELATED('Product Subcategory'[Product Subcategory Name])`  
  
     在您完成公式的建立后，按 Enter。  
  
4.  将列重命名`Product Subcategory Name`为。  
  
 Product Subcategory Name 计算列用于在 Product 表中创建一个层次结构，其中包括来自 Product Subcategory 表中 Product Subcategory Name 列的数据。 层次结构不能跨多个表。 您将在第 7 课中创建层次结构。  
  
#### <a name="create-a-product-category-name-calculated-column-in-the-product-table"></a>在 Product 表中创建 Product Category Name 计算列  
  
1.  在“Product”**** 表仍处于活动状态时，单击“列”**** 菜单，然后单击“添加列”****。  
  
2.  在公式栏中，键入以下公式：  
  
     `=RELATED('Product Category'[Product Category Name])`  
  
     在您完成公式的建立后，按 Enter。  
  
3.  将列重命名`Product Category Name`为。  
  
 Product Category Name 计算列用于在 Product 表中创建一个层次结构，其中包括来自 Product Category 表中 Product Category Name 列的数据。 层次结构不能跨多个表。  
  
#### <a name="create-a-margin-calculated-column-in-the-internet-sales-table"></a>在 Internet Sales 表中创建 Margin 计算列  
  
1.  在模型设计器中，选择“Internet Sales”**** 表。  
  
2.  添加新列。  
  
3.  在公式栏中，键入以下公式：  
  
     `=[Sales Amount]-[Total Product Cost]`  
  
     在您完成公式的建立后，按 Enter。  
  
4.  将列重命名`Margin`为。  
  
5.  将此列拖到“Sales Amount”**** 列与“Tax Amt”**** 列之间。  
  
 Margin 计算列用来分析每个（产品）行的毛利润率。  
  
## <a name="next-step"></a>下一步  
 若要继续学习本课程，请转到下一课： [第 7 课：创建度量值](lesson-6-create-measures.md)。  
  
  
