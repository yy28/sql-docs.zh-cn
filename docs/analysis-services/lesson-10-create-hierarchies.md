---
title: "第 10 课：创建层次结构 | Microsoft Docs"
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
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 第 10 课：创建层次结构
在本课中，您将创建层次结构。 层次结构是按级别排列的列的分组；例如，地理层次结构可能具有针对国家/地区、省/市/自治区、县和市的子级别。 层次结构可独立于报表客户端应用程序字段列表中的其他列出现，使客户端用户可以更方便地在报表中导航和包含数据。 若要了解详细信息，请参阅[层次结构（SSAS 表格）](../analysis-services/tabular-models/hierarchies-ssas-tabular.md)。  
  
若要创建层次结构，可使用“关系图视图”中的模型设计器。 在数据视图的模型设计器中不支持创建和管理层次结构。  
  
学完本课的估计时间：**20 分钟**  
  
## 先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本课程中的任务之前，应该已完成上一课：[第 9 课：创建透视](../Topic/Lesson%209:%20Create%20Perspectives.md)。  
  
## 创建层次结构  
  
#### 在 Product 表中创建类别层次结构  
  
1.  在模型设计器中，单击“模型”菜单，然后指向“模型视图”，再单击“关系图视图”。  
  
  
  
2.  右键单击“Product”表，然后单击“创建层次结构”。 一个新的层次结构将出现在表窗口的底部。  
  
3.  在层次结构名称中，通过键入 **Category** 重命名该层次结构，然后按 Enter。  
  
4.  在“Product” 表中，单击“Product Category Name”列，然后将其拖到“Category”层次结构，并在“Category”的顶部释放。  
  
5.  在“Category”层次结构中，右键单击“Product Category Name”列，然后单击“重命名”，键入 **Category**。  
  
    > [!NOTE]  
    > 重命名层次结构中的某列时，不重命名表中的该列。 层次结构中的列只是表中该列的表示形式。  
  
6.  在“Product”表中，单击“Product Subcategory Name”列并将其拖到“Category”层次结构。  
  
7.  将 **Product Subcategory Name** 重命名为 **Subcategory**。  
  
8.  （按顺序）单击并拖动“Model Name”和“Product Name”列，将它们放在“Product Subcategory Name”列下方。 将这些列分别重命名为 **Model** 和 **Product**。  
  
#### 在 Date 表中创建层次结构  
  
1.  在模型设计器中，右键单击“Date”表，然后单击“创建层次结构”。  
  
2.  将该层次结构重命名为 **Calendar**。  
  
3.  按顺序添加下面各列，然后重命名它们：  
  
    |列|重命名为：|  
    |----------|--------------|  
    |Calendar Year|Year|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|季度|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  在“Date”表中，重复上述步骤，创建“Fiscal”层次结构，包括以下各列：  
  
    |列|重命名为：|  
    |----------|--------------|  
    |Fiscal Year|Year|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|季度|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  最后，在“Date”表中，重复上述步骤，创建“Production Calendar”层次结构，包括以下各列：  
  
    |列|重命名为：|  
    |----------|--------------|  
    |Calendar Year|Year|  
    |Week Number Of Year|Week|  
    |Day Of Week|Day|  
  
## 后续步骤  
若要继续学习本教程，请转到下一课：[第 11 课：创建分区](../analysis-services/lesson-11-create-partitions.md)。  
  
  
  
