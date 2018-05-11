---
title: 第 10 课： 创建层次结构 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6241b60197b783710142c4fd2a2b9ebbf3486b30
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-9-create-hierarchies"></a>Lesson 9： 创建层次结构
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课中，您将创建层次结构。 层次结构是按级别排列的列的分组；例如，地理层次结构可能具有针对国家/地区、省/市/自治区、县和市的子级别。 层次结构可独立于报表客户端应用程序字段列表中的其他列出现，使客户端用户可以更方便地在报表中导航和包含数据。 若要了解详细信息，请参阅[层次结构](../analysis-services/tabular-models/hierarchies-ssas-tabular.md)。  
  
若要创建层次结构，你将使用模型设计器中的*图示视图*。 在数据视图中不支持创建和管理层次结构。  
  
学完本课的估计时间： **20 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 之前在本课程中执行任务，你应完成上一课：[课 8： 创建透视](../analysis-services/lesson-8-create-perspectives.md)。  
  
## <a name="create-hierarchies"></a>创建层次结构  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>在中的 DimProduct 表中创建一个类别层次结构  
  
1.  在模型设计器 （图示视图），右键单击**DimProduct**表 >**创建层次结构**。 一个新的层次结构将出现在表窗口的底部。 重命名层次结构**类别**。  
  
2.  单击并拖动**ProductCategoryName**对新的列**类别**层次结构。  
  
3.  在**类别**层次结构中，右键单击**ProductCategoryName** > **重命名**，然后键入**类别**。  
  
    > [!NOTE]  
    > 重命名层次结构中的某列时，不重命名表中的该列。 层次结构中的列只是表中该列的表示形式。  
  
4.  单击并拖动**ProductSubcategoryName**列**类别**层次结构。 将其重命名**子类别**。 
  
5.  右键单击**ModelName**列 >**将添加到层次结构**，然后选择**类别**。 为执行同样**EnglishProductName**。 重命名层次结构中的这些列**模型**和**产品**。  

    ![作为-表格-lesson9-类别](../analysis-services/media/as-tabular-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>若要在 DimDate 表创建层次结构  
  
1.  在**DimDate**表中，创建名为新层次结构**日历**。  
  
3.  添加以下列中的顺序：

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  在**DimDate**表中，创建**会计**层次结构。 包括以下各列：  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  最后，在**DimDate**表中，创建**ProductionCalendar**层次结构。 包括以下各列：  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>下一步是什么？
转到下一课：[课 10： 创建分区](../analysis-services/lesson-10-create-partitions.md)。 
  
  
