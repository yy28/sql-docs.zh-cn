---
title: Analysis Services 教程 lesson 9： 创建层次结构 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
ms.openlocfilehash: 2f6d539153aabd8cb87c4ec2c28deff330505b0d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="create-hierarchies"></a>创建层次结构

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，你可以创建层次结构。 层次结构是排列级别中的列组。 例如，Geography 层次结构对于国家/地区、 状态、 县和城市可能有子级别。 层次结构可独立于报表客户端应用程序字段列表中的其他列出现，使客户端用户可以更方便地在报表中导航和包含数据。 若要了解详细信息，请参阅[层次结构](../tabular-models/hierarchies-ssas-tabular.md)
  
若要创建层次结构，使用模型设计器中的*图示视图*。 在数据视图中不支持创建和管理层次结构。  
  
学完本课的估计时间： **20 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文摘自表格建模教程中，应按顺序完成。 之前在本课程中执行任务，你应完成上一课：[课 8： 创建透视](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)。  
  
## <a name="create-hierarchies"></a>创建层次结构  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>在中的 DimProduct 表中创建一个类别层次结构  
  
1.  在模型设计器 （图示视图），右键单击**DimProduct**表 >**创建层次结构**。 一个新的层次结构将出现在表窗口的底部。 重命名层次结构**类别**。  
  
2.  单击并拖动**ProductCategoryName**对新的列**类别**层次结构。  
  
3.  在**类别**层次结构中，右键单击**ProductCategoryName** > **重命名**，然后键入**类别**。  
  
    > [!NOTE]  
    > 重命名层次结构中的某列时，不重命名表中的该列。 层次结构中的列只是表中该列的表示形式。  
  
4.  单击并拖动**ProductSubcategoryName**列**类别**层次结构。 将其重命名**子类别**。 
  
5.  右键单击**ModelName**列 >**将添加到层次结构**，然后选择**类别**。 将其重命名**模型**。

6.  最后，添加**EnglishProductName**到类别层次结构。 将其重命名**产品**。  

    ![as-lesson9-category](../tutorial-tabular-1400/media/as-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>若要在 DimDate 表创建层次结构  
  
1.  在**DimDate**表中，创建名为层次结构**日历**。  
  
3.  添加以下列中的顺序：

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  在**DimDate**表中，创建**会计**层次结构。 包括以下列中的顺序：  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  最后，在**DimDate**表中，创建**ProductionCalendar**层次结构。 包括以下列中的顺序：  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>下一步是什么？

[第 10 课： 创建分区](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)。 
  
  
