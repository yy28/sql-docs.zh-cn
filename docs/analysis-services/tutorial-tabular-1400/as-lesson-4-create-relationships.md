---
title: Analysis Services 教程第 4 课：创建关系 |Microsoft Docs
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a39978dc461bd660d932e13561ed4d00c4041e0e
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52394513"
---
# <a name="create-relationships"></a>创建关系

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，将验证导入数据时自动创建的关系和不同的表之间添加新关系。 关系是在两个表之间建立的连接，用于确立这些表中的数据应该如何相关。 例如，DimProduct 表和 DimProductSubcategory 表基于每个产品属于某个子类别的事实具有某种关系。 若要了解详细信息，请参阅[关系](../tabular-models/relationships-ssas-tabular.md)。
  
学完本课的预计时间：**10 分钟**  
  
## <a name="prerequisites"></a>先决条件  

本文是表格建模教程应按顺序完成的一部分。 执行任务之前在本课程中，您应当已完成上一课：[第 3 课：标记为日期表](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)。 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>查看现有关系并添加新关系  

使用获取数据导入数据，当您从 AdventureWorksDW 数据库有七个表。 通常情况下，当您从关系源导入数据，将自动与数据一起导入现有关系。 为了获取数据在数据模型中自动创建关系，必须有关系数据源的表之间。

在继续创作模型之前，应验证这些表之间的关系已正确创建。 对于本教程，您还可以添加三个新关系。  

  
#### <a name="to-review-existing-relationships"></a>查看现有关系  
  
1.  单击**模型**菜单 >**模型视图** > **关系图视图**。  

    在模型设计器现在将显示在关系图视图以图形格式显示所有表导入了它们之间的行。 表之间的线条指示当您导入数据时自动创建的关系。
    
    ![作为 lesson4 图](../tutorial-tabular-1400/media/as-lesson4-diagram.png)
  
    > [!NOTE]
    > 如果看不到任何表之间的关系，则可能意味着在数据源的这些表之间没有任何关系。

    通过使用模型设计器右下角的 minimap 控件包括尽可能多的尽可能的表。 还可以单击表并将其拖到不同位置，使表之间更接近，或将它们排成特定的顺序。 移动表不会影响表之间的关系。 若要查看特定表中的所有列，请单击并拖动表边缘以展开或使其变小。  
  
2.  单击之间的实线**DimCustomer**表和**DimGeography**表。 这两个表之间的实线显示了此关系处于活动状态，也就是说，当计算 DAX 公式时默认情况下使用。  
  
    请注意**GeographyKey**中的列**DimCustomer**表和**GeographyKey**中的列**DimGeography**现在表同时每个出现在一个框。 在关系中使用这些列。 关系的属性现在也显示在**属性**窗口。  
  
    > [!TIP]  
    > 此外可以使用管理关系对话框以显示表格格式中的所有表之间的关系。 在表格模型资源管理器，右键单击**关系** > **管理关系**。
  
3.  验证时创建以下关系从 AdventureWorksDW 数据库导入每个表：  
  
    |在职|表|相关查找表|  
    |----------|---------|------------------------|  
    |用户帐户控制|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |用户帐户控制|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |用户帐户控制|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |用户帐户控制|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |用户帐户控制|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    如果缺少任意关系，则验证您的模型包括以下各表：DimCustomer、 DimDate、 DimGeography、 DimProduct、 DimProductCategory、 DimProductSubcategory 和 FactInternetSales。 如果在不同时间之间的任何关系相同的数据源连接中的表导入这些表将不会创建，并且必须手动创建。 如果没有关系出现，则表示在数据源没有任何关系。 您可以手动创建这些数据模型中。

### <a name="take-a-closer-look"></a>更详细地介绍

在关系图视图中，请注意一个箭头、 一个星号，以及显示表之间的关系的线条上的数字。

![作为 lesson4 行](../tutorial-tabular-1400/media/as-lesson4-line.png)

箭头显示筛选器方向。 星号显示此表是*许多*端中关系的基数，而是显示此表是*一个*端的关系。 如果您需要编辑关系;例如，更改关系的筛选器方向或基数，双击以打开编辑关系对话框中的关系线。

![作为 lesson4 编辑](../tutorial-tabular-1400/media/as-lesson4-edit.png)

这些功能适用于高级数据建模，并不在本教程的范围。 若要了解详细信息，请参阅[双向交叉筛选器中 Analysis Services 表格模型的](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)。

在某些情况下，您可能需要在模型中的表之间创建其他关系，以支持某些业务逻辑。 对于本教程，需要创建在 FactInternetSales 表和 DimDate 表之间的三个其他关系。  
  
#### <a name="to-add-new-relationships-between-tables"></a>在表之间添加新关系  
  
1.  在模型设计器中，在**FactInternetSales**表，单击并按住**OrderDate**列中，然后光标拖到**日期**中的列**DimDate**表，然后松开。  

    显示一条实线，说明已创建活动之间的关系**OrderDate**中的列**Internet Sales**表中，和**日期**中的列**日期**表。 
  
      ![作为-lesson4-新](../tutorial-tabular-1400/media/as-lesson4-new.png) 
  
    > [!NOTE]  
    > 创建关系时，会自动选择主表与相关的查找表之间的基数和筛选器方向。  
  
2.  在中**FactInternetSales**表中，单击并按住**DueDate**列，然后光标拖到**日期**中的列**DimDate**表，然后松开。  
  
    此时会显示虚线，其中显示已创建非活动的关系之间**DueDate**中的列**FactInternetSales**表，并且**日期**中的列**DimDate**表。 表之间可以具有多个关系，但一次只有一个关系可以处于活动状态。 非活动关系可将激活以在自定义的 DAX 表达式中执行特殊聚合。  
  
3.  最后，创建一个关系。 在中**FactInternetSales**表中，单击并按住**ShipDate**列，然后光标拖到**日期**中的列**DimDate**表，然后松开。  
    
     ![as-lesson4-newinactive](../tutorial-tabular-1400/media/as-lesson4-newinactive.png)
  
## <a name="whats-next"></a>下一步是什么？

[第 5 课：创建计算的列](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)。
  
  
  
