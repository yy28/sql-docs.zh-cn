---
title: Analysis Services 教程第 9 课： 创建层次结构 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
ms.openlocfilehash: df99d05373d4d3087ef1d5fa5324ec645bf000b6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37973016"
---
# <a name="create-hierarchies"></a>创建层次结构

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，将创建层次结构。 层次结构是按级别排列的列组。 例如，地理层次结构可包含子级别的国家/地区、 状态、 县和城市。 层次结构可独立于报表客户端应用程序字段列表中的其他列出现，使客户端用户可以更方便地在报表中导航和包含数据。 若要了解详细信息，请参阅[层次结构](../tabular-models/hierarchies-ssas-tabular.md)
  
若要创建层次结构，使用模型设计器中的*关系图视图*。 在数据视图中不支持创建和管理层次结构。  
  
学完本课的估计时间： **20 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文是表格建模教程应按顺序完成的一部分。 在之前在本课程中执行的任务，您应已完成上一课：[第 8 课： 创建透视](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)。  
  
## <a name="create-hierarchies"></a>创建层次结构  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>在 DimProduct 表中创建类别层次结构  
  
1.  在模型设计器 （关系图视图） 中右键单击**DimProduct**表 >**创建层次结构**。 一个新的层次结构将出现在表窗口的底部。 重命名层次结构**类别**。  
  
2.  单击并拖动**ProductCategoryName**对新的列**类别**层次结构。  
  
3.  在中**类别**层次结构中，右键单击**ProductCategoryName** > **重命名**，然后键入**类别**。  
  
    > [!NOTE]  
    > 重命名层次结构中的某列时，不重命名表中的该列。 层次结构中的列只是表中该列的表示形式。  
  
4.  单击并拖动**ProductSubcategoryName**列与**类别**层次结构。 将其重命名**Subcategory**。 
  
5.  右键单击**ModelName**列 >**添加到层次结构**，然后选择**类别**。 将其重命名**模型**。

6.  最后，添加**EnglishProductName**到类别层次结构。 将其重命名**产品**。  

    ![as-lesson9-category](../tutorial-tabular-1400/media/as-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>在 DimDate 表中创建层次结构  
  
1.  在中**DimDate**表中，创建名为的层次结构**日历**。  
  
3.  以下列按顺序添加：

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  在中**DimDate**表中，创建**会计**层次结构。 包括以下列中的顺序：  
  
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
  
  
