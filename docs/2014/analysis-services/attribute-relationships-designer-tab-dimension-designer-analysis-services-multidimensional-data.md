---
title: 属性关系 （属性关系设计器选项卡，维度设计器） (Analysis Services-多维数据) |Microsoft 文档
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
- sql12.asvs.dimensiondesigner.ardesigner.attributerelationships.f1
ms.assetid: abc8af00-5389-456d-b0f1-ec3e7403d4f9
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ea9c91e9584f2b5e7f561e9982ef1427340c470d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125478"
---
# <a name="attribute-relationships-attribute-relationship-designer-tab-dimension-designer-analysis-services---multidimensional-data"></a>属性关系（“属性关系”设计器选项卡，维度设计器）（Analysis Services - 多维数据）
  可以使用 **“属性关系”** 列表，查找属性关系图中的特定属性关系以及管理此关系。 此窗格紧位于包含属性关系图的窗格之下。  
  
 **若要查看属性关系窗格**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的解决方案资源管理器中，双击维度以打开维度设计器，然后单击“属性关系”选项卡。  
  
2.  在工具栏上，单击 **“显示列表视图”** 图标。  
  
## <a name="using-the-attribute-relationships-list"></a>使用“属性关系”列表  
 **“属性关系”** 列表显示维度中的所有属性关系。  
  
 若要查找属性关系图中的特定属性关系，可在列表中双击该属性。 该属性（又称特性）关系将在属性关系图中突出显示，其属性将显示在“属性”窗口中。  
  
> [!NOTE]  
>  您可以在列表中选择多个属性关系并进行更改。  
  
 如果属性关系不正确，则在连接两个属性的箭头上会出现一个图标。 若要确定此关系不正确的原因，可将鼠标指针置于图标上，然后读取工具提示中提供的说明。  
  
 若要管理属性关系，请右键单击属性关系，然后单击快捷菜单中相应的命令。  
  
### <a name="shortcut-menu-options"></a>快捷菜单选项  
 **编辑属性关系**  
 打开“编辑属性关系”对话框，可以在其中修改属性关系。  
  
 有关详细信息，请参阅[“创建属性关系”和“编辑属性关系”对话框（“属性关系设计器”选项卡，维度设计器）（Analysis Services - 多维数据）](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md)和[定义属性关系](multidimensional-models/attribute-relationships-define.md)。  
  
 **关系类型**  
 将关系类型设置为“柔性”或“刚性”。 在柔性关系中，成员之间的关系会随时间而变化。 在刚性关系中，成员之间的关系不随时间而变化。  
  
 **删除**  
 删除所选属性关系。  
  
 **属性**  
 在“属性”窗口中显示特性的属性。  
  
## <a name="see-also"></a>请参阅  
 [属性关系&#40;维度设计器&#41; &#40;Analysis Services-多维数据&#41;](attribute-relationships-dimension-designer-analysis-services-multidimensional-data.md)   
 [工具栏&#40;属性关系设计器选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-attribute-relationship-dimension-designer-analysis-services-multidimensional-data.md)   
 [属性&#40;属性关系设计器选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](attributes-designer-tab-dimension-designer-analysis-services-multidimensional-data.md)   
 [属性关系图&#40;属性关系设计器选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](attribute-relationship-diagram-analysis-services-multidimensional-data.md)  
  
  