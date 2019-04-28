---
title: 第 6 课：创建计算的列 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: adc7b7bf3335c8c9c7530d18f4d553492cfe9e1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728635"
---
# <a name="lesson-6-create-calculated-columns"></a>第 6 课：创建计算列
  在本课中，您将通过添加计算列在模型中创建新数据。 计算列基于模型中的现有数据。 了解详细信息，请参阅[计算列（SSAS 表格）](tabular-models/ssas-calculated-columns.md)。  
  
 您将在三个不同的表中创建五个新的计算列。 步骤对于每个任务略有不同。 此处介绍创建新列、重命名这些列以及将它们放入表中不同位置的多种方法。  
  
 估计的时间才能完成本课程中：**15 分钟**  
  
## <a name="prerequisites"></a>先决条件  
 本主题是表格建模教程的一部分，该教程应按顺序学习。 执行任务之前在本课程中，您应当已完成上一课：[第 5 课：创建关系](lesson-4-create-relationships.md)。  
  
## <a name="create-calculated-columns"></a>创建计算列  
  
#### <a name="create-a-month-calendar-calculated-column-in-the-date-table"></a>在 Date 表中创建 Month Calendar 计算列  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“模型”菜单，然后指向“模型视图”，再单击“数据视图”。  
  
     只能在数据视图中使用模型设计器创建计算列。  
  
2.  在模型设计器中，单击“Date”表（选项卡）。  
  
3.  右键单击**日历季度**列中，并单击**插入列**。  
  
     名为的新列**CalculatedColumn1**插入到的左侧**日历季度**列。  
  
4.  在表上面的编辑栏中，键入以下公式。 自动完成功能将帮助您键入列和表的完全限定名称，并且列出可用的函数。  
  
     `=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]`  
  
     在您完成公式的建立后，按 Enter。  
  
     然后，将为计算列中的所有行填充值。 如果在表中向下滚动，将看到行对于此列可以具有不同的值（基于每行中的数据）。  
  
    > [!NOTE]  
    >  如果收到错误，请验证公式中的列名称中更改的列名称匹配[第 3 课：重命名列](rename-columns.md)。  
  
5.  为此列重命名`Month Calendar`。  
  
 Month Calendar 计算列提供可排序的月份名称。  
  
#### <a name="create-a-day-of-week-calculated-column-in-the-date-table"></a>在 Date 表中创建 Day of Week 计算列  
  
1.  在“Date”表仍处于活动状态时，单击“列”菜单，然后单击“添加列”。  
  
     一个新列添加到表的最右侧。  
  
2.  在公式栏中，键入以下公式：  
  
     `=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]`  
  
     在您完成公式的建立后，按 Enter。  
  
3.  列重命名为`Day of Week`。  
  
4.  单击列标题，然后将此列拖到“Day Name”列与“Day of Month”列之间。  
  
    > [!TIP]  
    >  移动表中的列可使表变得更易于浏览。  
  
 Day of Week 计算列为周内的日期提供可排序的名称。  
  
#### <a name="create-a-product-subcategory-name-calculated-column-in-the-product-table"></a>在 Product 表中创建 Product Subcategory Name 计算列  
  
1.  在模型设计器中，选择“Product”表。  
  
2.  滚动到表的最右侧。 请注意，最右侧的列被命名为“添加列”（斜体），单击该列标题。  
  
3.  在公式栏中，键入以下公式。  
  
     `=RELATED('Product Subcategory'[Product Subcategory Name])`  
  
     在您完成公式的建立后，按 Enter。  
  
4.  列重命名为`Product Subcategory Name`。  
  
 Product Subcategory Name 计算列用于在 Product 表中创建一个层次结构，其中包括来自 Product Subcategory 表中 Product Subcategory Name 列的数据。 层次结构不能跨多个表。 您将在第 7 课中创建层次结构。  
  
#### <a name="create-a-product-category-name-calculated-column-in-the-product-table"></a>在 Product 表中创建 Product Category Name 计算列  
  
1.  在“Product”表仍处于活动状态时，单击“列”菜单，然后单击“添加列”。  
  
2.  在公式栏中，键入以下公式：  
  
     `=RELATED('Product Category'[Product Category Name])`  
  
     在您完成公式的建立后，按 Enter。  
  
3.  列重命名为`Product Category Name`。  
  
 Product Category Name 计算列用于在 Product 表中创建一个层次结构，其中包括来自 Product Category 表中 Product Category Name 列的数据。 层次结构不能跨多个表。  
  
#### <a name="create-a-margin-calculated-column-in-the-internet-sales-table"></a>在 Internet Sales 表中创建 Margin 计算列  
  
1.  在模型设计器中，选择“Internet Sales”表。  
  
2.  添加新列。  
  
3.  在公式栏中，键入以下公式：  
  
     `=[Sales Amount]-[Total Product Cost]`  
  
     在您完成公式的建立后，按 Enter。  
  
4.  列重命名为`Margin`。  
  
5.  将此列拖到“Sales Amount”列与“Tax Amt”列之间。  
  
 Margin 计算列用来分析每个（产品）行的毛利润率。  
  
## <a name="next-step"></a>下一步  
 若要继续学习本课程，请转到下一课：[第 7 课：创建度量值](lesson-6-create-measures.md)。  
  
  
