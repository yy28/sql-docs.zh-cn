---
title: "第 6 课：创建计算列 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 第 6 课：创建计算列
在本课中，您将通过添加计算列在模型中创建新数据。 计算列基于模型中的现有数据。 了解详细信息，请参阅[计算列（SSAS 表格）](../analysis-services/tabular-models/calculated-columns-ssas-tabular.md)。  
  
您将在三个不同的表中创建五个新的计算列。 步骤对于每个任务略有不同。 此处介绍创建新列、重命名这些列以及将它们放入表中不同位置的多种方法。  
  
学完本课的估计时间：**15 分钟**  
  
## 先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本课程中的任务之前，须已完成上一课：[第 5 课：创建关系](../analysis-services/lesson-5-create-relationships.md)。  
  
## 创建计算列  
  
#### 在 Date 表中创建 Month Calendar 计算列  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“模型”菜单，然后指向“模型视图”，再单击“数据视图”。  
  
    只能在数据视图中使用模型设计器创建计算列。  
  
2.  在模型设计器中，单击“Date”表（选项卡）。  
  
3.  右键单击“Calendar Quarter”列标题，然后单击“插入列”。  
  
    一个名为“Calculated Column 1”的新列插入到“Calendar Quarter”列的左侧。  
  
4.  在表上面的编辑栏中，键入以下公式。 自动完成功能将帮助您键入列和表的完全限定名称，并且列出可用的函数。  
  
    **=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]**  
  
    在您完成公式的建立后，按 Enter。  
  
    然后，将为计算列中的所有行填充值。 如果在表中向下滚动，将看到行对于此列可以具有不同的值（基于每行中的数据）。  
  
    > [!NOTE]  
    > 如果收到错误提示，请验证确保公式中的列名与在[第 3 课：重命名列](../analysis-services/lesson-3-rename-columns.md)中更改的列名是否匹配。  
  
5.  将此列重命名为“Month Calendar”。  
  
Month Calendar 计算列提供可排序的月份名称。  
  
#### 在 Date 表中创建 Day of Week 计算列  
  
1.  在“Date”表仍处于活动状态时，单击“列”菜单，然后单击“添加列”。  
  
2.  在公式栏中，键入以下公式：  
  
    **=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]**  
  
    在您完成公式的建立后，按 Enter。 新列将添加到表的最右侧。  
  
3.  将此列重命名为“Day of Week”。  
  
4.  单击列标题，然后将此列拖到“Day Name”列与“Day of Month”列之间。  
  
    > [!TIP]  
    > 移动表中的列可使表变得更易于浏览。  
  
Day of Week 计算列为周内的日期提供可排序的名称。  
  
#### 在 Product 表中创建 Product Subcategory Name 计算列  
  
1.  在模型设计器中，选择“Product”表。  
  
2.  滚动到表的最右侧。 请注意，最右侧的列被命名为“添加列”（斜体），单击该列标题。  
  
3.  在公式栏中，键入以下公式。  
  
    **=RELATED('Product Subcategory'[Product Subcategory Name])**  
  
    在您完成公式的建立后，按 Enter。  
  
4.  将此列重命名为“Product Subcategory Name”。  
  
Product Subcategory Name 计算列用于在 Product 表中创建一个层次结构，其中包括来自 Product Subcategory 表中 Product Subcategory Name 列的数据。 层次结构不能跨多个表。 您将在第 7 课中创建层次结构。  
  
#### 在 Product 表中创建 Product Category Name 计算列  
  
1.  在“Product”表仍处于活动状态时，单击“列”菜单，然后单击“添加列”。  
  
2.  在公式栏中，键入以下公式：  
  
    **=RELATED('Product Category'[Product Category Name])**  
  
    在您完成公式的建立后，按 Enter。  
  
3.  将此列重命名为“Product Category Name”。  
  
Product Category Name 计算列用于在 Product 表中创建一个层次结构，其中包括来自 Product Category 表中 Product Category Name 列的数据。 层次结构不能跨多个表。  
  
#### 在 Internet Sales 表中创建 Margin 计算列  
  
1.  在模型设计器中，选择“Internet Sales”表。  
  
2.  添加新列。  
  
3.  在公式栏中，键入以下公式：  
  
    **=[Sales Amount]-[Total Product Cost]**  
  
    在您完成公式的建立后，按 Enter。  
  
4.  将此列重命名为“Margin”。  
  
5.  将此列拖到“Sales Amount”列与“Tax Amt”列之间。  
  
Margin 计算列用来分析每个（产品）行的毛利润率。  
  
## 下一步  
若要继续学习本课程，请转到下一课：[第 7 课：创建度量值](../analysis-services/lesson-7-create-measures.md)。  
  
  
  
