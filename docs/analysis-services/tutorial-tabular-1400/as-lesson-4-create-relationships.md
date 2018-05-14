---
title: Analysis Services 教程第 4 课： 创建关系 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 564126e1de4a8019778e33718b48462f633ae232
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="create-relationships"></a>创建关系

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，你将验证导入数据时自动创建的关系，并添加不同的表之间的新关系。 关系是在两个表之间建立的连接，用于确立这些表中的数据应该如何相关。 例如，DimProduct 表和 DimProductSubcategory 表基于每个产品属于某个子类别的事实具有某种关系。 若要了解详细信息，请参阅[关系](../tabular-models/relationships-ssas-tabular.md)。
  
学完本课的估计时间：**10 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文摘自表格建模教程中，应按顺序完成。 之前在本课程中执行任务，你应完成上一课：[第 3 课： 标记为日期表](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)。 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>查看现有关系并添加新关系  

当使用获取数据导入数据时，你将从 AdventureWorksDW 数据库中获取七个表。 通常情况下，当你将数据从关系数据源时，现有关系是与数据一起自动导入。 为了获取要在数据模型中自动创建关系的数据，必须有关系数据源中的表之间。

在继续进行创作您的模型之前，你应验证这些表之间的关系正确创建。 对于本教程，你还可以添加三个新的关系。  

  
#### <a name="to-review-existing-relationships"></a>查看现有关系  
  
1.  单击**模型**菜单 >**模型视图** > **图示视图**。  

    模型设计器现在将显示在关系图视图以图形格式显示所有表你使用导入它们之间的界限。 表之间的线条指示当您导入数据时自动创建的关系。
    
    ![作为 lesson4 图](../tutorial-tabular-1400/media/as-lesson4-diagram.png)
  
    > [!NOTE]
    > 如果看不到任何表之间的关系，但很可能意味着在数据源的这些表之间没有任何关系。

    通过使用模型设计器的右下角中的最小映射控件包含任意多个尽可能表。 还可以单击表并将其拖到不同位置，使表之间更接近，或将它们排成特定的顺序。 移动表不会影响表之间的关系。 若要查看特定表中的所有列，请单击并拖动以展开或使更小的一个表边缘上的。  
  
2.  单击之间实线**DimCustomer**表和**DimGeography**表。 这两个表之间实线显示这种关系是处于活动状态，也就是说，在计算 DAX 公式时默认情况下使用。  
  
    请注意**GeographyKey**中的列**DimCustomer**表和**GeographyKey**中的列**DimGeography**表现在这两项每出现一个框内。 在关系中使用这些列。 关系的属性现在也显示在“属性”窗口中。  
  
    > [!TIP]  
    > 你可以使用管理关系对话框中以显示表格格式中的所有表之间的关系。 在表格模型资源管理器，右键单击**关系** > **管理关系**。
  
3.  验证以下关系已创建时每个表已从 AdventureWorksDW 数据库导入：  
  
    |在职|表|相关查找表|  
    |----------|---------|------------------------|  
    |是|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |是|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |是|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |是|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |是|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    如果缺少任何关系，则验证您的模型包含下表： DimCustomer、 DimDate、 DimGeography、 DimProduct、 DimProductCategory、 DimProductSubcategory 和 FactInternetSales。 如果时间之间的任何关系的单独导入表从相同的数据源连接这些表将不会创建，并且必须手动创建。 如果没有关系出现，这意味着在数据源没有任何关系。 你可以手动在中创建它们的数据模型。

### <a name="take-a-closer-look"></a>要进一步查看

在关系图视图中，请注意箭头、 星号和显示表之间的关系的行数。

![作为 lesson4 行](../tutorial-tabular-1400/media/as-lesson4-line.png)

箭头显示的筛选器方向。 星号显示此表是*许多*端中的关系的基数和一个显示此表是*一个*侧的关系。 如果你需要编辑关系;例如，更改关系的筛选器方向或基数，双击该关系连线以打开编辑关系对话框。

![作为 lesson4 编辑](../tutorial-tabular-1400/media/as-lesson4-edit.png)

这些功能用于建模的高级数据，并在本教程中的范围以外。 若要了解详细信息，请参阅[双向交叉筛选器的 Analysis Services 中的表格模型](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)。

在某些情况下，您可能需要在模型中的表之间创建其他关系，以支持某些业务逻辑。 对于本教程中，你需要创建 FactInternetSales 表和 DimDate 表之间的三个其他关系。  
  
#### <a name="to-add-new-relationships-between-tables"></a>在表之间添加新关系  
  
1.  在模型设计器中，在**FactInternetSales**表，单击并按住上**OrderDate**列，然后拖动光标所在位置到**日期**中的列**DimDate**表，，然后释放。  

    一条实线显示显示你已创建一个活动关系之间**OrderDate**中的列**Internet Sales**表，与**日期**中的列**日期**表。 
  
      ![作为-lesson4-新建](../tutorial-tabular-1400/media/as-lesson4-new.png) 
  
    > [!NOTE]  
    > 在创建关系时，会自动选择主表和相关的查找表之间的基数和筛选器方向。  
  
2.  在**FactInternetSales**表，单击并按住**DueDate**列，然后拖动光标所在位置到**日期**中的列**DimDate**表，，然后释放。  
  
    虚线显示显示你已创建之间的非活动关系**DueDate**中的列**FactInternetSales**表，与**日期**中的列**DimDate**表。 表之间可以具有多个关系，但一次只有一个关系可以处于活动状态。 非活动关系可以将活动状态，以在自定义的 DAX 表达式中执行特殊的聚合。  
  
3.  最后，创建一个更多的关系。 在**FactInternetSales**表，单击并按住**ShipDate**列，然后拖动光标所在位置到**日期**中的列**DimDate**表，，然后释放。  
    
     ![as-lesson4-newinactive](../tutorial-tabular-1400/media/as-lesson4-newinactive.png)
  
## <a name="whats-next"></a>下一步是什么？

[第 5 课： 创建计算的列](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)。
  
  
  
