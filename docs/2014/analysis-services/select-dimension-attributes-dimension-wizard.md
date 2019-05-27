---
title: 选择维度属性 （维度向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionattributes.f1
ms.assetid: f58a3e14-ab27-44d3-8c26-f5c9ee7583b0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84f8612b4d420eed11308472c9c8fabfc56e23c0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069531"
---
# <a name="select-dimension-attributes-dimension-wizard"></a>选择维度属性（维度向导）
  可以使用 **“选择维度属性”** 页选择和修改要创建的维度的属性。  
  
> [!NOTE]  
>  如果您无法读取任何列的值，请将向导窗口最大化并改变每个列标题的宽度直到可以读取这些值。  
  
 **若要打开维度向导**  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的**解决方案资源管理器**中，右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目的“维度”文件夹，然后单击“新建维度”。  
  
## <a name="options"></a>选项  
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
  
 在大多数情况下，将 `AttributeHierarchyEnabled` 属性设置为 `True` 或 `False` 可以使浏览分别为可用或不可用。 但是，在下列三种情况中，向导使用不同的设置。  
  
|情况|设置|  
|----------|--------------|  
|维度包含父子层次结构并且没有选中“启用浏览”|向导将键特性的 `AttributeHierarchyEnabled` 属性设置保留为 `True`，并将 `AttributeHierarchyVisible` 属性设置为 `False`。|  
|维度中的表包含指向维度中没有的表的外键|向导选择该外键作为要包含的属性，但不选中 **“启用浏览”**。 如果保留这些设置，则特性的 `AttributeHiearchyEnabled` 属性将设置为 `True`，而 `AttributeHieararchyVisible` 属性将设置为 `False`。|  
|维度包含通过可为空值的外键列访问的雪花型表<br /><br /> -和-<br /><br /> 对于基于雪花型表键的属性，不选中“启用浏览”|向导将创建 `AttributeHiearchyEnabled` 属性设置为 `True`，`AttributeHieararchyVisible` 属性设置为 `False` 的新特性。|  
  
 **属性类型**  
 （可选）设置属性的类型。 默认值为 **Regular**。 属性类型向客户端应用程序提供属性中可能包含的信息类型的指南。  
  
## <a name="see-also"></a>请参阅  
 [维度向导的 F1 帮助](dimension-wizard-f1-help.md)   
 [维度&#40;Analysis Services-多维数据&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
