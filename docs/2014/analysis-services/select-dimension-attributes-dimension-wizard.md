---
title: 选择维度属性 （维度向导） |Microsoft 文档
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
- sql12.asvs.dimensionwizard.dimensionattributes.f1
ms.assetid: f58a3e14-ab27-44d3-8c26-f5c9ee7583b0
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6af0f81a3b356427d4279bfcdcb88f1c7b14ba57
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026420"
---
# <a name="select-dimension-attributes-dimension-wizard"></a>选择维度属性（维度向导）
  可以使用 **“选择维度属性”** 页选择和修改要创建的维度的属性。  
  
> [!NOTE]  
>  如果您无法读取任何列的值，请将向导窗口最大化并改变每个列标题的宽度直到可以读取这些值。  
  
 **若要打开维度向导**  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的**解决方案资源管理器**中，右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目的“维度”文件夹，然后单击“新建维度”。  
  
## <a name="options"></a>“常规”  
 (带复选框的列)  
 选择此项将包括维度中的属性。  
  
 若要包含特定属性，请选中该属性的复选框。  
  
 若要包含所有属性，请选中列标题中的复选框。  
  
> [!NOTE]  
>  键属性的复选框不能清除。  
  
 **属性名称**  
 列出可用属性。  
  
 若要更改属性的名称，请单击属性名称并键入该属性的新名称。  
  
 **启用浏览**  
 选中此项可使最终用户能够浏览并筛选属性。 对于键属性，必须选中 **“启用浏览”** 。 对于非键属性，默认未选中“启用浏览”，这将导致非键属性只显示为成员属性。  
  
 在大多数情况下，该属性由可用或不可用于通过设置浏览`AttributeHierarchyEnabled`属性`True`或`False`分别。 但是，在下列三种情况中，向导使用不同的设置。  
  
|情况|“设置”|  
|----------|--------------|  
|维度包含父子层次结构并且没有选中“启用浏览”|向导将保持`AttributeHierarchyEnabled`属性设置为`True`，并将设置`AttributeHierarchyVisible`属性设为`False`的键属性。|  
|维度中的表包含指向维度中没有的表的外键|向导选择该外键作为要包含的属性，但不选中 **“启用浏览”**。 如果保留这些设置，则特性的 `AttributeHiearchyEnabled` 属性将设置为 `True`，而 `AttributeHieararchyVisible` 属性将设置为 `False`。|  
|维度包含通过可为空值的外键列访问的雪花型表<br /><br /> —并且—<br /><br /> 对于基于雪花型表键的属性，不选中“启用浏览”|向导将创建新属性，其`AttributeHiearchyEnabled`属性设置为`True`，和`AttributeHieararchyVisible`属性设置为`False`。|  
  
 **特性类型**  
 （可选）设置属性的类型。 默认值为 **Regular**。 属性类型向客户端应用程序提供属性中可能包含的信息类型的指南。  
  
## <a name="see-also"></a>请参阅  
 [维度向导的 F1 帮助](dimension-wizard-f1-help.md)   
 [维度&#40;Analysis Services-多维数据&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  