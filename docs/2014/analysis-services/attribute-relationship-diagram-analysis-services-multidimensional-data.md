---
title: 属性关系图 （属性关系设计器选项卡，维度设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.ardesigner.ardiagram.f1
ms.assetid: 320989ad-bd95-43f4-a2e7-b262d66dbda7
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e4467e0ca268edd9d9e38ca4d915c489c5f65014
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208117"
---
# <a name="attribute-relationship-diagram-attribute-relationship-designer-tab-dimension-designer-analysis-services---multidimensional-data"></a>属性关系图（“属性关系”设计器选项卡，维度设计器）（Analysis Services - 多维数据）
  可以使用 **“属性关系”** 选项卡上的工具栏紧下方的窗格查看属性关系图，以及创建、修改和删除属性关系。  
  
 **若要查看包含属性关系图窗格**  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的解决方案资源管理器中，双击维度以打开维度设计器，然后单击“属性关系”选项卡。  
  
## <a name="using-the-attribute-relationship-diagram"></a>使用属性关系图  
 使用属性关系图可以创建、编辑或删除属性关系。 属性关系图还将突出显示有问题的属性关系并在工具提示中显示该问题的说明。  
  
 关系图中有三个独立的快捷菜单：关系图快捷菜单、属性快捷菜单和关系快捷菜单。  
  
### <a name="diagram-shortcut-menu"></a>关系图快捷菜单  
 若要打开属性关系图的快捷菜单，请右键单击关系图的背景。 关系图快捷菜单包含以下命令：  
  
 **新建属性关系**  
 打开“创建属性关系”对话框，可以在其中定义新的属性关系。  
  
 有关详细信息，请参阅[“创建属性关系”和“编辑属性关系”对话框（“属性关系设计器”选项卡，维度设计器）（Analysis Services - 多维数据）](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md)和[定义属性关系](multidimensional-models/attribute-relationships-define.md)。  
  
 **排列形状**  
 根据维度设计器使用的布局算法排列形状。  
  
 **自动排列形状**  
 根据维度设计器使用的布局算法，自动排列关系图中的形状。 默认情况下，启用 **“自动排列形状”** 。  
  
 **显示列表视图**  
 显示或隐藏“属性”和“属性关系”列表。 这些列表立即出现在包含属性关系图的窗格下的自己的窗格中。  
  
 **展开所有形状**  
 显示与顶级属性相关联的分组属性。 分组属性仅在展开属性关系图中的形状时可见。  
  
> [!NOTE]  
>  如果单击此属性，维度设计器会将属性关系图中的形状返回到该设计器使用的默认布局中。  
  
 **折叠所有形状**  
 隐藏与顶级属性相关联的分组属性。  
  
> [!NOTE]  
>  如果单击此属性，维度设计器会将属性关系图中的形状返回到该设计器使用的默认布局中。  
  
 **缩放**  
 显示可用的缩放选项列表。  
  
### <a name="attribute-shortcut-menu"></a>属性快捷菜单  
 若要打开属性快捷菜单，请右键单击属性关系图中的属性。 属性快捷菜单包含以下命令：  
  
 **新建属性关系**  
 打开“创建属性关系”对话框，可以在其中定义新的属性关系。  
  
 有关详细信息，请参阅[“创建属性关系”和“编辑属性关系”对话框（“属性关系设计器”选项卡，维度设计器）（Analysis Services - 多维数据）](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md)和[定义属性关系](multidimensional-models/attribute-relationships-define.md)。  
  
 **属性**  
 在“属性”窗口中显示特性的属性。  
  
### <a name="relationship-shortcut-menu"></a>关系快捷菜单  
 若要打开关系快捷菜单，请右键单击标识两个属性之间关系的箭头。 关系快捷菜单包含以下命令：  
  
 **编辑属性关系**  
 打开“编辑属性关系”对话框，可以在其中修改属性关系。  
  
 有关详细信息，请参阅[“创建属性关系”和“编辑属性关系”对话框（“属性关系设计器”选项卡，维度设计器）（Analysis Services - 多维数据）](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md)和[定义属性关系](multidimensional-models/attribute-relationships-define.md)。  
  
 **关系类型**  
 将关系类型设置为“柔性”或“刚性”。 在柔性关系中，成员之间的关系会随时间而变化。 在刚性关系中，成员之间的关系不随时间而变化。  
  
 **删除**  
 删除属性关系。  
  
 **属性**  
 在“属性”窗口中显示关系的属性。  
  
## <a name="see-also"></a>请参阅  
 [属性关系&#40;维度设计器&#41; &#40;Analysis Services-多维数据&#41;](attribute-relationships-dimension-designer-analysis-services-multidimensional-data.md)   
 [工具栏&#40;属性关系设计器选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-attribute-relationship-dimension-designer-analysis-services-multidimensional-data.md)   
 [属性&#40;属性关系设计器选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](attributes-designer-tab-dimension-designer-analysis-services-multidimensional-data.md)   
 [属性关系&#40;属性关系设计器选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](attribute-relationships-designer-tab-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
