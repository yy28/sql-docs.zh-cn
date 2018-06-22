---
title: 数据源视图 （维度结构选项卡，维度设计器） (Analysis Services-多维数据) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.datasourcepane.f1
ms.assetid: c4bd3c5e-8986-448f-b9db-3551f50f0696
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c960a5c08f3d95ee6ef0813db67f8d9a33a6a683
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016983"
---
# <a name="data-source-view-dimension-structure-tab-dimension-designer-analysis-services---multidimensional-data"></a>数据源视图（“维度结构”选项卡，维度设计器）（Analysis Services - 多维数据）
  可以使用 **“数据源视图”** 窗格，查看与所选维度关联的数据源视图中的表和列。 使用此窗格，可以通过将列从 **“数据源视图”** 窗格中拖动到 **“属性”** 窗格或 **“层次结构和级别”** 窗格中，来创建特性、成员属性、层次结构和级别。  
  
## <a name="options"></a>“常规”  
 **数据源视图**  
 显示与所选维度相关联的数据源视图。  
  
 **（移动角度来看）**  
 单击窗格右下角滚动条之间的位置，即可选择要查看的“数据源视图”窗格区域。  
  
## <a name="diagram-context-menu"></a>关系图上下文菜单  
 右键单击“数据源视图”窗格的关系图背景后，显示的上下文菜单中包含下表中所列的选项：  
  
 **显示表**  
 显示“显示表”对话框。 有关“显示表”对话框的详细信息，请参阅[“显示表”对话框（Analysis Services - 多维数据）](show-table-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **显示所有表**  
 在窗格中显示与维度相关联的数据源视图中包含的所有表。  
  
 **仅显示已用表**  
 在窗格中仅显示关联的数据源视图中维度所使用的表。  
  
 **显示的友好名称**  
 选择此选项可以在窗格中显示对象的友好名称。  
  
 **全选**  
 选择窗格中的所有对象。  
  
 **查找表**  
 显示“查找表”对话框。 有关“查找表”对话框的详细信息，请参阅[“查找表”对话框（Analysis Services - 多维数据）](find-table-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **排列表**  
 根据通过选择“切换到对角线布局”或“切换到矩形布局”指定的布局，排列窗格中的对象。  
  
 **切换到对角线布局**  
 选择此项将按对角线模式排列对象。  
  
> [!NOTE]  
>  只有在选择了“切换到矩形布局”时，才会显示此选项。  
  
 **切换到矩形布局**  
 选择此项将按矩形模式排列对象。  
  
> [!NOTE]  
>  只有在选择了“切换到对角线布局”时，才会显示此选项。  
  
 **编辑数据源视图**  
 显示与维度关联的数据源视图的**数据源视图设计器**。 有关**数据源视图设计器**的详细信息，请参阅[数据源视图设计器（Analysis Services - 多维数据）](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **显示在数据源视图**  
 通过选择下列选项之一，可以在“数据源视图”窗格的以下查看模式之间切换：  
  
-   关系图  
  
     显示与当前维度相关联的表和列的关系图。  
  
-   trEE  
  
     显示树视图，其中包含与当前维度相关联的表和列。  
  
 **关系图复制源**  
 选择与维度关联的数据源视图中包含的一个关系图，以在“数据源视图”窗格中显示该关系图。  
  
 **缩放**  
 选择可用的缩放选项。  
  
 **属性**  
 在“SQL Server Data Tools”中显示与维度关联的数据源视图的“属性”窗口。  
  
## <a name="table-context-menu"></a>表上下文菜单  
 右键单击“数据源视图”窗格中表或视图的名称后，显示的上下文菜单中提供下表中所列的选项：  
  
 **显示相关的表**  
 在窗格中显示与数据源视图中的所选表相关的表。  
  
 **隐藏表**  
 从窗格中删除相应的表。  
  
 **浏览数据**  
 显示所选表的“浏览数据”对话框。  
  
 **编辑数据源视图**  
 显示包含所选表的数据源视图的**数据源视图设计器**。 有关**数据源视图设计器**的详细信息，请参阅[数据源视图设计器（Analysis Services - 多维数据）](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **属性**  
 在“SQL Server Data Tools”中显示所选表的“属性”窗口。  
  
## <a name="column-context-menu"></a>列上下文菜单  
 右键单击“数据源视图”窗格中表或视图中的列的名称后，显示的上下文菜单中提供下表中所列的选项：  
  
 **从列新建属性**  
 在窗格中显示与数据源视图中的所选表相关的表。  
  
 **浏览数据**  
 显示包含所选列的表的“浏览数据”对话框。  
  
 **编辑数据源视图**  
 显示包含所选列的数据源视图的**数据源视图设计器**。 有关**数据源视图设计器**的详细信息，请参阅[数据源视图设计器（Analysis Services - 多维数据）](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **属性**  
 在“SQL Server Data Tools”中显示所选列的“属性”窗口。  
  
## <a name="relationship-context-menu"></a>关系上下文菜单  
 右键单击“数据源视图”窗格中的关系后，显示的上下文菜单中提供下表中所列的选项：  
  
 **编辑数据源视图**  
 显示包含所选关系的数据源视图的**数据源视图设计器**。 有关**数据源视图设计器**的详细信息，请参阅[数据源视图设计器（Analysis Services - 多维数据）](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **属性**  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中显示所选关系的“属性”窗口。  
  
## <a name="see-also"></a>请参阅  
 [维度结构&#40;维度设计器&#41; &#40;Analysis Services-多维数据&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md)   
 [工具栏&#40;维度结构选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-dimension-structure-designer-analysis-services-multidimensional-data.md)   
 [属性&#40;维度结构选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](attributes-dimension-designer-analysis-services-multidimensional-data.md)   
 [层次结构&#40;维度结构选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)  
  
  