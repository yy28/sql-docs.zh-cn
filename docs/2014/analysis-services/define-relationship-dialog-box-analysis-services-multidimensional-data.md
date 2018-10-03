---
title: 定义关系对话框 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.f1
helpviewer_keywords:
- Define Relationship dialog box
ms.assetid: 0fcee7f1-f138-4c2e-ae8c-245395ee0fe8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bc1ab86373fc7c3b4b32cdfdbc87f5d5dd4acf8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196297"
---
# <a name="define-relationship-dialog-box-analysis-services---multidimensional-data"></a>“定义关系”对话框（Analysis Services - 多维数据）
  使用 **“定义关系”** 对话框，可以定义多维数据集设计器中的多维数据集维度与度量值组之间的关系。 在多维数据集设计器的 **“维度用法”** 选项卡上，单击 **“网格”** 窗格中单元上的 **...** ，可以显示 **“定义关系”** 对话框。  
  
## <a name="options"></a>选项  
 **选择关系类型**  
 选择要在多维数据集维度与度量值组之间创建的维度关系的类型。 选择维度关系类型可以更改 **“详细信息”** 窗格的内容。  
  
 如果选择 **“无关系”** ，将不会创建维度关系。  
  
 Detail  
 显示“选择关系类型”中所选维度关系类型可用的选项。  
  
## <a name="detail-pane-options"></a>详细信息窗格选项  
 下面列出了 **“详细信息”** 窗格中显示的选项（根据 **“选择关系类型”** 中所选关系类型的不同，所显示的选项也有所不同）：  
  
|关系类型|Description|选项|  
|-----------------------|-----------------|------------|  
|**任何关系**|没有定义任何关系，并且 **“详细信息”** 窗格中也不显示任何选项。||  
|**Regular**|指定常规维度关系。 **“详细信息”** 窗格中显示以下选项：|**粒度属性**: <br />                      选择定义与维度有关的度量值组粒度的属性。 此属性通常为维度的键属性。|  
|||**维度表**：显示维度的主表。|  
|||**度量值组表**：显示度量值组的事实数据表。|  
|||“关系”：显示关系所基于的维度列和度量值组列的网格。 该网格包含以下列：<br /><br /> **维度列**：显示与所选粒度属性相关联的列。 注意：如果尚未生成维度，则此选项将设置为“生成” 。<br />**度量值组列**：<br />                              选择度量值组中与维度列相关的列。|  
|||**高级**：<br />                      单击此项可显示“度量值组绑定”对话框，并可以编辑特性和度量值组列之间的关系的高级属性，如空值处理。 有关“度量值组绑定”对话框的详细信息，请参阅[“度量值组绑定”对话框（Analysis Services - 多维数据）](measure-group-bindings-dialog-box-analysis-services-multidimensional-data.md)。|  
|**这一事实**|指定事实维度关系。 **“详细信息”** 窗格中显示以下选项：|**粒度属性**：选择定义与维度有关的度量值组粒度的属性。 此属性通常为维度的键属性。|  
|||**维度表**：显示主维度表。|  
|||**度量值组表**： <br />                      显示度量值组所基于的表。|  
|**引用**|指定引用的维度关系。 **“详细信息”** 窗格中显示以下选项：|**引用维度**: <br />                      显示所选维度。|  
|||**中间维度**： <br />                      选择中间维度。|  
|||**引用维度属性**： <br />                      选择引用维度中与“中间维度属性”中指定的中间维度属性相关的属性。|  
|||**中间维度属性**： <br />                      选择中间维度中与“引用维度”中指定的引用维度属性相关的属性。|  
|||**具体化**： <br />                      选择以存储中间维度中将引用维度中的属性链接到 MOLAP 结构中的事实数据表的属性成员。 使关系具体化是用于最大程度地提高查询性能的默认行为，但这同时会增加处理时间和存储空间。|  
|**多对多**|指定多对多维度关系。 **“详细信息”** 窗格中显示以下选项：|“维度” ：显示所选维度。|  
|||**中间度量值组**： <br />                      选择相关联的中间度量值组。<br /><br /> 注意：中间度量值组必须至少有一个与所选度量值组共享的维度。 此外，中间度量值组与共同维度之间关系的粒度必须大于或等于共同维度与所选度量值组之间的粒度。|  
|**数据挖掘**|指定数据挖掘维度关系。 **“详细信息”** 窗格中显示以下选项：|“目标维度”：显示所选数据挖掘维度。<br /><br /> 注意：若要创建数据挖掘维度关系，则必须选择数据挖掘维度。|  
|||**源维度**：选择数据挖掘维度提供预测分析所处的维度。|  
  
## <a name="see-also"></a>请参阅  
 [维度关系](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [维度用法&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)   
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
