---
title: "第 5 课： 创建关系 |Microsoft 文档"
ms.custom: 
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 53cfcc73f8bca771607425ac69eff021b8e6a00c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="lesson-4-create-relationships"></a>第 4 课： 创建关系
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课程将验证导入数据时自动创建的关系，并添加新不同的表之间的关系。 关系是在两个表之间建立的连接，用于确立这些表中的数据应该如何相关。 例如，DimProduct 表和 DimProductSubcategory 表基于每个产品属于某个子类别的事实具有某种关系。 若要了解详细信息，请参阅[关系](../analysis-services/tabular-models/relationships-ssas-tabular.md)。
  
学完本课的估计时间： **10 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 之前在本课程中执行任务，你应完成上一课：[第 3 课： 标记为日期表](../analysis-services/lesson-3-mark-as-date-table.md)。 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>查看现有关系并添加新关系  
当使用表导入向导导入数据时，你将从 AdventureWorksDW 数据库中获取七个表。 通常情况下，当你将数据从关系数据源时，现有关系是与数据一起自动导入。 但是，在继续创作模型之前，您应验证正确创建了表之间的这些关系。 对于本教程，您还会添加三个新关系。  
  
#### <a name="to-review-existing-relationships"></a>查看现有关系  
  
1.  单击**模型**菜单 >**模型视图** > **图示视图**。  

    模型设计器现在出现在“关系图视图”中，这是一种图形格式，可显示您导入的所有表以及表之间的线条。 表之间的线条指示当您导入数据时自动创建的关系。
    
    ![作为-表格-lesson4-关系图](../analysis-services/media/as-tabular-lesson4-diagram.png)
  
    使用模型设计器右下角的 minimap 控件可调整此视图，以包括尽可能多的表。 还可以单击表并将其拖到不同位置，使表之间更接近，或将它们排成特定的顺序。 移动表不会影响表之间已存在的关系。 若要查看特定表中的所有列，请单击并拖动表边缘以展开或使其变小。  
  
2.  单击之间实线**DimCustomer**表和**DimGeography**表。 这两个表之间的实线表明此关系处于活动状态，也即，当计算 DAX 公式时，默认情况下将使用此关系。  
  
    请注意**GeographyKey**中的列**DimCustomer**表和**GeographyKey**中的列**DimGeography**表现在这两项每出现一个框内。 这表明关系中使用的是这些列。 关系的属性现在也显示在“属性”窗口中。  
  
    > [!TIP]  
    > 除了在关系图视图中使用模型设计器中，你还可以使用管理关系对话框中以显示表格格式中的所有表之间的关系。 右键单击**关系**在表格模型资源管理器，然后单击**管理关系**。 管理关系对话框中显示导入数据时自动创建的关系。  
  
3.  使用模型设计器在图示视图或管理关系对话框中，若要验证以下关系已创建时每个表已导入从 AdventureWorksDW 数据库：  
  
    |在职|表|相关查找表|  
    |----------|---------|------------------------|  
    |是|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |是|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |是|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |是|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |是|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    如果缺少任何上述表中的关系，则验证您的模型包含下表： DimCustomer、 DimDate、 DimGeography、 DimProduct、 DimProductCategory、 DimProductSubcategory 和 FactInternetSales。 如果在不同的时间从相同的数据源连接导入了表，则在这些表之间不会创建任何关系，而必须手动创建。  

### <a name="take-a-closer-look"></a>要进一步查看
在关系图视图中，你会注意到一个箭头，星号和显示表之间的关系的行号。

![作为表格-lesson4-行](../analysis-services/media/as-tabular-lesson4-line.png)

箭头显示筛选器方向，星号演示了此表是在关系的基数中的许多端而 1 显示了此表是关系的一方。 如果你需要编辑关系;例如，更改关系的筛选器方向或基数，双击要打开编辑关系对话框中的关系图视图中的关系行。

![作为表格-lesson4-编辑](../analysis-services/media/as-tabular-lesson4-edit.png)

最有可能，你将永远不会需要编辑关系。 这些功能用于建模的高级数据，并在本教程中的范围以外。 若要了解详细信息，请参阅[双向交叉筛选器的 SQL Server 2016 Analysis Services 中的表格模型](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)。

在某些情况下，您可能需要在模型中的表之间创建其他关系，以支持某些业务逻辑。 对于本教程中，你需要创建 FactInternetSales 表和 DimDate 表之间的三个其他关系。  
  
#### <a name="to-add-new-relationships-between-tables"></a>在表之间添加新关系  
  
1.  在模型设计器中，在**FactInternetSales**表，单击并按住**OrderDate**列，然后拖动光标所在位置到**日期**中的列**DimDate**表，，然后释放。  

    一条实线显示显示你已创建一个活动关系之间**OrderDate**中的列**Internet Sales**表和**日期**中列**日期**表。 
  
      ![作为-表格-lesson4-新建](../analysis-services/media/as-tabular-lesson4-new.png) 
  
    > [!NOTE]  
    > 在创建关系时，会自动选择主表和相关的查找表之间的基数和筛选器方向。  
  
2.  在**FactInternetSales**表，单击并按住**DueDate**列，然后拖动光标所在位置到**日期**中的列**DimDate**表，，然后释放。  
  
    虚线显示显示你已创建之间的非活动关系**DueDate**中的列**FactInternetSales**表和**日期**中的列**DimDate**表。 表之间可以具有多个关系，但一次只有一个关系可以处于活动状态。  
  
3.  最后，创建一个更多的关系;在**FactInternetSales**表，单击并按住**ShipDate**列，然后拖动光标所在位置到**日期**中的列**DimDate**表，然后松开。  
    
     ![作为-表格-lesson4-newinactive](../analysis-services/media/as-tabular-lesson4-newinactive.png)
  
## <a name="whats-next"></a>下一步是什么？
转到下一课：[第 5 课： 创建计算列](../analysis-services/lesson-5-create-calculated-columns.md)。
  
  
  
