---
title: 在数据源视图中定义逻辑关系（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- adding relationships
- relationships [Analysis Services], data source views
- data source views [Analysis Services], relationships
ms.assetid: a20d6dae-e769-4131-8a59-7ef56f174220
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: caa1b9ee8af054f7fcc5f10869553343d50a9c2d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66075622"
---
# <a name="define-logical-relationships-in-a-data-source-view-analysis-services"></a>在数据源视图中定义逻辑关系 (Analysis Services)
  数据源视图向导和数据源视图设计器自动定义添加到数据源视图 (DSV) 的表之间的关系，定义过程基于基础数据库关系或指定的名称匹配条件。  
  
 如果您在使用来自多个数据源的数据，则可能需要在 DSV 中手动定义逻辑关系，以便对自动定义的这些关系进行补充。 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，需要使用关系来标识事实数据表和维度表，以构建用于从基础数据源检索数据和元数据的查询，以及利用高级业务智能功能。  
  
 您可以在数据源视图设计器中定义下列关系类型：  
  
-   同一数据源中的两个表之间的关系。  
  
-   一个表与其本身的关系，就像父子关系一样。  
  
-   某数据源中的一个表与另一个数据源中的另一个表的关系。  
  
> [!NOTE]  
>  在 DSV 中定义的关系是逻辑关系，可能无法反映基础数据源中定义的实际关系。 在数据源视图设计器中，可以创建基础数据源中不存在的关系，也可以从基础数据源的现有外键关系中删除由数据源视图设计器所创建的关系。  
  
 关系是有方向的。 对于源列中的每个值，在目标列中都有一个对应值。 在数据源视图关系图中（如 **“关系图”** 窗格中显示的关系图），两表之间连线上的箭头指示关系的方向。  
  
 本主题包含下列部分：  
  
 [在表、命名查询或视图之间添加关系](#bkmk_addRel)  
  
 [在 "关系图" 窗格中查看或修改关系](#bkmk_diagrampane)  
  
 [在 "表" 窗格中查看或修改关系](#bkmk_tablespane)  
  
##  <a name="to-add-a-relationship-between-tables-named-queries-or-views"></a><a name="bkmk_addRel"></a>添加表、命名查询或视图之间的关系  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开项目或连接到数据库，此项目或数据库包含要在其中添加逻辑关系的数据源视图。  
  
2.  在解决方案资源管理器中，展开“数据源视图”文件夹，然后双击数据源视图以便在“数据源视图设计器”中打开该视图********。  
  
3.  在任一“表”**** 窗格中右键单击要添加关系的表、命名查询或视图，再单击“新建关系”****。  
  
    > [!NOTE]  
    >  若要查找表、视图或命名查询，可以通过单击“数据源视图”菜单或者右键单击“表”或“关系图”窗格的空白区域，以使用“查找表”选项****************。  
  
4.  在 **“指定关系”** 对话框中，执行下列操作：  
  
    1.  在“源(外键)表”**** 列表中选择适当的表、命名查询或视图。  
  
    2.  在“目标(主键)表”**** 列表中选择适当的表、命名查询或视图。  
  
    3.  从 **“源列”** 和 **“目标列”** 列表中选择列，以创建两个表之间的关系。  
  
         如果 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 通过抽样基础表、视图或命名查询中的数据检测到已按错误方向（从主键到外键而不是从外键到主键）定义了关系，则系统将提示反转顺序。 若要快速反转顺序，请单击 **“反转”**。  
  
         如果 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 检测到所选列之间已存在关系，则系统将提示您。 您不能定义重复关系。  
  
    4.  还可以在 **“说明”** 框中键入对该关系的说明。  
  
##  <a name="to-view-or-modify-a-relationship-in-the-diagram-pane"></a><a name="bkmk_diagrampane"></a> 在“关系图”窗格中查看或修改关系  
  
-   在“数据源视图设计器”的“关系图”窗格中，右键单击要查看的关系，再单击“编辑关系”（或者仅双击关系箭头）************。  使用 **“编辑属性关系”** 对话框可修改关系。  
  
##  <a name="to-view-or-modify-a-relationship-in-the-tables-pane"></a><a name="bkmk_tablespane"></a> 在“表”窗格中查看或修改关系  
  
1.  在 **“数据源视图设计器”** 的 **“表”** 窗格中，查找包含要查看或修改的关系的表、视图或命名查询，然后将其展开。  
  
2.  展开 **“关系”** 文件夹。  将显示所选表、视图或命名查询与其他表、视图和命名查询之间的关系，并列出关系列。  
  
3.  右键单击要修改的关系，然后单击“编辑关系”****。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的数据源视图](data-source-views-in-multidimensional-models.md)  
  
  
