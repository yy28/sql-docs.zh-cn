---
title: 替换表或数据源视图 (Analysis Services) 中的命名的查询 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a171eafc35446f588d64c74457792912dcebe75a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services"></a>在数据源视图中替换表或命名查询 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在数据源视图设计器中，可以将数据源视图 (DSV) 中的表、视图或命名查询替换为来自相同数据源或不同数据源的其他表或视图，或者替换为 DSV 中定义的命名查询。 替换表时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的所有其他对象或引用了该表的项目将继续引用该表，因为 DSV 中表的对象 ID 不会发生更改。 任何仍然相关（基于名称和列类型匹配）的关系仍然保留。 与此不同的是，如果删除后再添加表，则将丢失引用和关系，因此必须重新创建引用和关系。  
  
 若要使用其他表替换表，必须在项目模式下与数据源视图设计器中的源数据建立活动连接。  
  
 最常用的替换是使用数据源中的其他表替换该数据源视图中的表。 但是，也可以使用表替换命名查询。 例如，以前使用命名查询替换了一个表，现在想要恢复为表。  
  
> [!IMPORTANT]  
>  如果要重命名数据源中的表，请按以下步骤替换表，并在刷新 DSV 之前，指定重命名后的表作为 DSV 中对应的表的源。 完成替换和重命名处理后，将在 DSV 中保存表、表的引用和表的关系。 否则，在刷新 DSV 时，数据源中重命名后的表将被解释为已删除。 有关详细信息，请参阅[刷新数据源视图中的架构 (Analysis Services)](../../analysis-services/multidimensional-models/refresh-the-schema-in-a-data-source-view-analysis-services.md)。  
  
##  <a name="bkmk_nq"></a> 使用命名查询替换表  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开项目或连接到数据库，此项目或数据库包含要在其中替换表或命名查询的数据源视图。  
  
2.  在解决方案资源管理器中，展开“数据源视图”文件夹，然后双击数据源视图。  
  
3.  将打开 **“创建命名查询”** 对话框。 在“表”或“关系图”窗格中，右键单击要替换的表，指向“替换表”，再单击“使用新建命名查询”。  
  
4.  在 **“创建命名查询”** 对话框中，定义命名查询，再单击 **“确定”**。  
  
5.  保存已修改的数据源视图。  
  
## <a name="replace-a-table-or-named-query-with-a-table"></a>使用表替换表或命名查询  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开项目或连接到数据库，此项目或数据库包含要在其中替换表或命名查询的数据源视图。  
  
2.  在解决方案资源管理器中，展开“数据源视图”文件夹，然后双击数据源视图。  
  
3.  将打开 **“用其他表替换该表”** 对话框。 在“表”或“关系图”窗格中，右键单击要替换的表或命名查询，指向“替换表”，再单击“使用其他表”。  
  
4.  在 **“用其他表替换该表”** 对话框中：  
  
    1.  在“数据源”下拉列表框中，选择所需数据源  
  
    2.  选择要用以替换表或命名查询的表  
  
5.  单击 **“确定”**。  
  
6.  保存已修改的数据源视图。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的数据源视图](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
