---
title: 第 10 课： 创建层次结构 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 51f8d7b6616f6f14621209561146916cb4b0acd1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187281"
---
# <a name="lesson-10-create-hierarchies"></a>第 10 课：创建层次结构
  在本课中，您将创建层次结构。 层次结构是按级别排列的列的分组；例如，地理层次结构可能具有针对国家/地区、省/市/自治区、县和市的子级别。 层次结构可独立于报表客户端应用程序字段列表中的其他列出现，使客户端用户可以更方便地在报表中导航和包含数据。 若要了解详细信息，请参阅[层次结构（SSAS 表格）](tabular-models/hierarchies-ssas-tabular.md)。  
  
 若要创建层次结构，可使用“关系图视图”中的模型设计器。 在数据视图的模型设计器中不支持创建和管理层次结构。  
  
 学完本课的估计时间： **20 分钟**  
  
## <a name="prerequisites"></a>必要條件  
 本主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本课程中的任务之前，应该已完成上一课：[第 9 课：创建透视](lesson-8-create-perspectives.md)。  
  
## <a name="create-hierarchies"></a>创建层次结构  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>在 Product 表中创建类别层次结构  
  
1.  在模型设计器中，单击`Model`菜单，然后指向**模型视图**，然后单击**关系图视图**。  
  
    > [!TIP]  
    >  使用位于模型设计器右上角的 Minimap 控件可更改您在关系图视图中查看对象的方式。 如果您在关系图视图中重新定位对象，则当您保存项目时，将保留该视图。  
  
2.  在模型设计器中，右键单击`Product`表，并单击**创建层次结构**。 一个新的层次结构将出现在表窗口的底部。  
  
3.  在层次结构名称中，通过重命名层次结构键入`Category`，然后按 ENTER。  
  
4.  在中`Product`表中，单击**Product Category Name**列中，然后将其拖到`Category`层次结构，然后松开的`Category`名称。  
  
5.  在中`Category`层次结构中，右键单击**Product Category Name**列中，然后单击**重命名**，然后键入`Category`。  
  
    > [!NOTE]  
    >  重命名层次结构中的某列时，不重命名表中的该列。 层次结构中的列只是表中该列的表示形式。  
  
6.  在`Product`表中，右键单击**Product Subcategory Name**列中，然后在上下文菜单中，依次指向**添加到层次结构**，然后单击`Category`。  
  
7.  重命名**Product Subcategory Name**到`Subcategory`。  
  
8.  通过单击和拖动，或通过使用**添加到层次结构**命令的上下文菜单中，添加**模型名称**并**产品名称**（按顺序） 的列并将其下放置**Product Subcategory Name**列。 重命名这些列`Model`和`Product`分别。  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>在 Date 表中创建层次结构  
  
1.  在模型设计器中，右键单击“Date”表，然后单击“创建层次结构”。  
  
2.  将该层次结构重命名为 **Calendar**。  
  
3.  按顺序添加下面各列，然后重命名它们：  
  
    |“列”|重命名为：|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|季度|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  在“Date”表中，重复上述步骤，创建“Fiscal”层次结构，包括以下各列：  
  
    |“列”|重命名为：|  
    |------------|----------------|  
    |Fiscal Year|Year|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|季度|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  最后，在“Date”表中，重复上述步骤，创建“Production Calendar”层次结构，包括以下各列：  
  
    |“列”|重命名为：|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Week Number Of Year|Week|  
    |Day Of Week|Day|  
  
## <a name="next-steps"></a>后续步骤  
 若要继续学习本教程，请转到下一课：[第 11 课：创建分区](lesson-10-create-partitions.md)。  
  
  
