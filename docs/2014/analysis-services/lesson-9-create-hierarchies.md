---
title: 第10课：创建层次结构 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
author: minewiskan
ms.author: owend
ms.openlocfilehash: b6b57669eed30abf010b9d2775950bf0cd6c6e67
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84542149"
---
# <a name="lesson-10-create-hierarchies"></a>第 10 课：创建层次结构
  在本课中，您将创建层次结构。 层次结构是按级别排列的列的分组；例如，地理层次结构可能具有针对国家/地区、省/市/自治区、县和市的子级别。 层次结构在报告客户端应用程序字段列表中可以与其他列分开显示，这使得客户端用户更容易在其中导航以及将其包括在报表中。 若要了解详细信息，请参阅[层次结构（SSAS 表格）](tabular-models/hierarchies-ssas-tabular.md)。  
  
 若要创建层次结构，可使用“关系图视图”** 中的模型设计器。 在数据视图的模型设计器中不支持创建和管理层次结构。  
  
 本课预计完成时间：**20 分钟**  
  
## <a name="prerequisites"></a>先决条件  
 本主题是表格建模教程的一部分，应当按顺序完成。 在执行本课程中的任务之前，应该已完成上一课： [第 9 课：创建透视](lesson-8-create-perspectives.md)。  
  
## <a name="create-hierarchies"></a>创建层次结构  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>在 Product 表中创建类别层次结构  
  
1.  在模型设计器中，单击 `Model` 菜单，指向 "**模型视图**"，然后单击 "**关系图视图**"。  
  
    > [!TIP]  
    >  使用位于模型设计器右上角的 Minimap 控件可更改您在关系图视图中查看对象的方式。 如果您在关系图视图中重新定位对象，则当您保存项目时，将保留该视图。  
  
2.  在模型设计器中，右键单击 `Product` 表，然后单击 "**创建层次结构**"。 一个新的层次结构将出现在表窗口的底部。  
  
3.  在层次结构名称中，通过键入重命名该层次结构， `Category` 然后按 enter。  
  
4.  在 `Product` 表中，单击 " **Product Category Name** " 列，然后将其拖到 `Category` 层次结构中，然后在该名称的顶部释放 `Category` 。  
  
5.  在 `Category` 层次结构中，右键单击 "**产品类别名称**" 列，然后单击 "**重命名**"，然后键入 `Category` 。  
  
    > [!NOTE]  
    >  重命名层次结构中的某个列不会重命名表中的该列。 层次结构中的列只是表中该列的表示形式。  
  
6.  在 `Product` 表中，右键单击 "**产品子类别名称**" 列，然后在上下文菜单中指向 "**添加到层次结构**"，然后单击 "添加" `Category` 。  
  
7.  将**产品子类别名称**重命名为 `Subcategory` 。  
  
8.  通过使用 "单击并拖动" 或使用上下文菜单中的 "**添加到层次结构**" 命令，添加 "**型号名称**" 和 "**产品名称**" 列（按顺序），并将其放在 "**产品子类别名称**" 列下。 分别重命名这些列 `Model` 和 `Product` 。  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>在 Date 表中创建层次结构  
  
1.  在模型设计器中，右键单击“Date”**** 表，然后单击“创建层次结构”****。  
  
2.  将该层次结构重命名为 **Calendar**。  
  
3.  按顺序添加下面各列，然后重命名它们：  
  
    |列|重命名为：|  
    |------------|----------------|  
    |Calendar Year|年龄|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|季度|  
    |Month Calendar|月份|  
    |Day Of Month|天|  
  
4.  在“Date”**** 表中，重复上述步骤，创建“Fiscal”**** 层次结构，包括以下各列：  
  
    |列|重命名为：|  
    |------------|----------------|  
    |Fiscal Year|年龄|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|季度|  
    |Month Calendar|月份|  
    |Day Of Month|天|  
  
5.  最后，在“Date”**** 表中，重复上述步骤，创建“Production Calendar”**** 层次结构，包括以下各列：  
  
    |列|重命名为：|  
    |------------|----------------|  
    |Calendar Year|年龄|  
    |Week Number Of Year|周|  
    |Day Of Week|天|  
  
## <a name="next-steps"></a>后续步骤  
 若要继续学习本教程，请转到下一课： [第 11 课：创建分区](lesson-10-create-partitions.md)。  
  
  
