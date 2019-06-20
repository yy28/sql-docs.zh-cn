---
title: 第 5 课：创建关系 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a80f607c3187e967404ce018b7eed00497d9c01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078583"
---
# <a name="lesson-5-create-relationships"></a>第 5 课：创建关系
  在本课中，将验证导入数据时自动创建的关系并在不同表之间添加新关系。 关系是在两个表之间建立的连接，用于确立这些表中的数据应该如何相关。 例如，Product 表和 Product Subcategory 表基于每个产品属于某个子类别的事实具有某种关系。 有关详细信息，请参阅[关系（SSAS 表格）](tabular-models/relationships-ssas-tabular.md)  
  
 估计的时间才能完成本课程中：**10 分钟**  
  
## <a name="prerequisites"></a>先决条件  
 本主题是表格建模教程的一部分，该教程应按顺序学习。 执行任务之前在本课程中，您应当已完成上一课：[第 3 课：重命名列](rename-columns.md)。  
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>查看现有关系并添加新关系  
 当您使用“表导入向导”导入数据时，从 AdventureWorksDW 数据库导入了七个表。 通常，如果您从关系源中导入数据，则将自动导入现有关系以及数据。 但是，在继续创作模型之前，您应验证正确创建了表之间的这些关系。 对于本教程，您还会添加三个新关系。  
  
#### <a name="to-review-existing-relationships"></a>查看现有关系  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“模型”  菜单，然后指向“模型视图”  ，再单击“关系图视图”  。  
  
     模型设计器现在出现在“关系图视图”中，这是一种图形格式，可显示您导入的所有表以及表之间的线条。 表之间的线条指示当您导入数据时自动创建的关系。  
  
     使用模型设计器右上角的 minimap 控件可调整此视图，以包括尽可能多的表。 还可以单击表并将其拖到不同位置，使表之间更接近，或将它们排成特定的顺序。 移动表不会影响表之间已存在的关系。 若要查看特定表中的所有列，请单击并拖动表边缘以展开或使其变小。  
  
2.  单击 **Customer** 表与 **Geography** 表之间的实线。 这两个表之间的实线表明此关系处于活动状态，也即，当计算 DAX 公式时，默认情况下将使用此关系。  
  
     请注意， **Customer** 表中的 **Geography Id** 列和 **Geography** 表中的 **Geography Id** 列现在同时出现在一个框中。 这表明关系中使用的是这些列。 关系的属性现在也显示在**属性**窗口。  
  
    > [!TIP]  
    >  除了使用关系图视图中的模型设计器之外，还可以使用“管理关系”  对话框以表格式显示所有表之间的关系。 单击“表”  菜单，然后单击“管理关系”  。 “管理关系”  对话框显示导入数据时自动创建的关系。  
  
3.  使用关系图视图中的模型设计器或“管理关系”  对话框，验证在从 AdventureWorksDW 数据库中导入每个表时创建的以下关系：  
  
    |在职|表|相关查找表|  
    |------------|-----------|--------------------------|  
    |是|**客户 [Geography Id]**|**Geography [Geography Id]**|  
    |是|**Product [Product Subcategory Id]**|**Product Subcategory [Product Subcategory Id]**|  
    |是|**产品子类别 [产品类别 Id]**|**Product Category [Product Category Id]**|  
    |是|**Internet Sales [Customer Id]**|**客户 [Customer Id]**|  
    |是|**Internet Sales [Product Id]**|**Product [Product Id]**|  
  
 如果缺少任何上表中的关系，则验证您的模型包括以下各表：客户、 日期、 地理位置、 产品、 产品类别、 产品子类别和 Internet 销售。 如果在不同的时间从相同的数据源连接导入了表，则在这些表之间不会创建任何关系，而必须手动创建。  
  
 在某些情况下，您可能需要在模型中的表之间创建其他关系，以支持某些业务逻辑。 对于本教程，您需要在 Internet Sales 表与 Date 表之间创建三个其他关系。  
  
#### <a name="to-add-new-relationships-between-tables"></a>在表之间添加新关系  
  
1.  在模型设计器中，在 **Internet Sales** 表中单击并按住 **Order Date** 列，将光标拖到 **Date** 表中的 **Date** 列，然后松开。  
  
     将显示一条实线，说明已在 **Internet Sales** 表的 **Order Date** 列与 **Date** 表的 **Date** 列之间创建了活动的关系。  
  
    > [!NOTE]  
    >  当创建关系时，将自动正确地排列主表与相关查找表之间的顺序。  
  
2.  在 **Internet Sales** 表中单击并按住 **Due Date** 列，将光标拖到 **Date** 表中的 **Date** 列，然后松开。  
  
     将显示一条点划线，说明已在 **Internet Sales** 表的 **Due Date** 列与 **Date** 表的 **Date** 列之间创建了非活动的关系。 表之间可以具有多个关系，但一次只有一个关系可以处于活动状态。  
  
3.  最后，再创建一个关系；在 **Internet Sales** 表中单击并按住 **Ship Date** 列，将光标拖到 **Date** 表中的 **Date** 列，然后松开。  
  
     将显示一条点划线，说明已在 **Internet Sales** 表的 **Ship Date** 列与 **Date** 表的 **Date** 列之间创建了非活动的关系。  
  
## <a name="next-step"></a>下一步  
 若要继续学习本课程，请转到下一课：[第 6 课：创建计算的列](lesson-5-create-calculated-columns.md)。  
  
  
