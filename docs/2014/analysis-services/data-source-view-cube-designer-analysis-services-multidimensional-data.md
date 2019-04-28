---
title: 数据源视图 （多维数据集结构选项卡，多维数据集设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.cubebuilder.datasourcepane.f1
ms.assetid: 1e39c910-5c10-4624-be27-ca02a461b46b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fd3d21c2371878c44accc4d7e9f501f47ce64646
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732658"
---
# <a name="data-source-view-cube-structure-tab-cube-designer-analysis-services---multidimensional-data"></a>数据源视图（“多维数据集结构”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用 **“数据源视图”** 窗格，查看与所选多维数据集关联的数据源视图中的表和列。 此窗格用于创建度量值组和度量值，方法是将列从 **“数据源视图”** 窗格拖动到 **“度量值”** 窗格中。  
  
## <a name="options"></a>选项  
 **数据源视图**  
 显示与所选多维数据集关联的数据源视图。  
  
 **（移动视点）**  
 单击窗格右下角滚动条之间的位置，即可选择要查看的“数据源视图”窗格区域。  
  
## <a name="diagram-context-menu"></a>关系图上下文菜单  
 右键单击“数据源视图”窗格的关系图背景后显示的上下文菜单中包含下列选项：  
  
 **显示表**  
 显示“显示表”对话框。 有关“显示表”对话框的详细信息，请参阅[“显示表”对话框（Analysis Services - 多维数据）](show-table-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **显示所有表**  
 在窗格中显示与多维数据集相关联的数据源视图中包含的所有表。  
  
 **仅显示已用表**  
 在窗格中仅显示关联的数据源视图中多维数据集所使用的那些表。  
  
 **显示的友好名称**  
 选择此选项可以显示窗格中对象的友好名称。  
  
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
 显示与对象关联的数据源视图的数据源视图设计器。 有关数据源视图设计器的详细信息，请参阅[数据源视图设计器（Analysis Services - 多维数据）](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **数据源视图中显示**  
 通过选择下列选项之一，可以在“数据源视图”窗格的以下查看模式之间切换：  
  
-   关系图  
  
     显示与当前多维数据集关联的表和列的关系图。  
  
-   树  
  
     显示包含与当前多维数据集关联的表和列的树视图。  
  
 **关系图复制源**  
 选择与多维数据集关联的数据源视图所包含的一个关系图，可以在“数据源视图”窗格中显示该关系图。  
  
 **缩放**  
 选择可用的缩放选项。  
  
 **属性**  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，显示与多维数据集关联的数据源视图的“属性”窗口。  
  
## <a name="table-context-menu"></a>表上下文菜单  
 右键单击“数据源视图”窗格中表或视图的名称后显示的上下文菜单中包含下列选项：  
  
 **显示相关的表**  
 在窗格中显示与数据源视图中的所选表相关的表。  
  
 **隐藏表**  
 从窗格中删除相应的表。  
  
 **浏览数据**  
 显示所选表的“浏览数据”对话框。  
  
 **编辑数据源视图**  
 显示包含所选表的数据源视图的数据源视图设计器。 有关数据源视图设计器的详细信息，请参阅[数据源视图设计器（Analysis Services - 多维数据）](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **从表新建度量值组**  
 基于所选表在“度量值”窗格中定义新的度量值组。  
  
> [!NOTE]  
>  只有当“度量值”窗格中的度量值组尚未引用该表时，才会启用此选项。  
  
 **属性**  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中显示所选表的“属性”窗口。  
  
## <a name="column-context-menu"></a>列上下文菜单  
 右键单击“数据源视图”窗格内表或视图中的列名称后显示的上下文菜单中包含下列选项：  
  
 **从列新建度量值**  
 基于所选列在“度量值”窗格中定义新的度量值。  
  
 **浏览数据**  
 显示包含所选列的表的“浏览数据”对话框。  
  
 **编辑数据源视图**  
 显示包含所选列的数据源视图的数据源视图设计器。 有关数据源视图设计器的详细信息，请参阅[数据源视图设计器（Analysis Services - 多维数据）](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **属性**  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中显示所选列的“属性”窗口。  
  
## <a name="relationship-context-menu"></a>关系上下文菜单  
 右键单击“数据源视图”窗格中的关系后显示的上下文菜单中包含下列选项：  
  
 **编辑数据源视图**  
 显示包含所选关系的数据源视图的数据源视图设计器。 有关数据源视图设计器的详细信息，请参阅[数据源视图设计器（Analysis Services - 多维数据）](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **属性**  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中显示所选关系的“属性”窗口。  
  
## <a name="see-also"></a>请参阅  
 [工具栏&#40;多维数据集结构选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [度量值&#40;多维数据集结构选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](measures-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [维度&#40;多维数据集结构选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](dimensions-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [多维数据集结构&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](cube-structure-cube-designer-analysis-services-multidimensional-data.md)  
  
  
