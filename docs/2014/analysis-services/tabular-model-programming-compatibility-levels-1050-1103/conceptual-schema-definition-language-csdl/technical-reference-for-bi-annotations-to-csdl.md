---
title: 商业智能的 CSDL 注释技术参考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 63b3e069-6ba5-474e-b769-47b7cc87b7dd
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 78300a412d7db986edd76172c7cf49e6c86aaec9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192374"
---
# <a name="technical-reference-for-bi-annotations-to-csdl"></a>用于商业智能的 CSDL 注释技术参考
  本部分列出了 CSDL 中用于表示 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 表格模型的元素、特性和属性。 某些元素是新增的：其他属性已添加批注或扩展，以支持商业智能建模。  
  
 有关表格模型和在 CSDL 中如何表示实体、 关系和公式的概述，请参阅[用于商业智能的 CSDL 批注&#40;CSDLBI&#41;](../csdl-annotations-for-business-intelligence-csdlbi.md)。  
  
## <a name="extended-csdl-elements-complex-types"></a>扩展的 CSDL 元素：复杂类型  
 已添加或扩展以下 CSDL 元素，以支持商业智能数据模型（表格和多维）。  
  
-   [AssociationSet 元素&#40;CSDLBI&#41;](associationset-element-csdlbi.md)  
  
-   [BaseProperty 元素&#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [DefaultDetails 元素&#40;CSDLBI&#41;](defaultdetails-element-csdlbi.md)  
  
-   [DisplayKey 元素&#40;CSDLBI&#41;](displaykey-element-csdlbi.md)  
  
-   [EntityContainer 元素&#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)  
  
-   [EntitySet 元素&#40;CSDLBI&#41;](entityset-element-csdlbi.md)  
  
-   [EntityType 元素&#40;CSDLBI&#41;](entitytype-element-csdlbi.md)  
  
-   [Hierarchy 元素&#40;CSDLBI&#41;](hierarchy-element-csdlbi.md)  
  
-   [KPI 元素&#40;CSDLBI&#41;](kpi-element-csdlbi.md)  
  
-   [KpiGoal 元素&#40;CSDLBI&#41;](kpigoal-element-csdlbi.md)  
  
-   [KpiStatus 元素&#40;CSDLBI&#41;](kpistatus-element-csdlbi.md)  
  
-   [Level 元素&#40;CSDLBI&#41;](level-element-csdlbi.md)  
  
-   [度量值元素&#40;CSDLBI&#41;](measure-element-csdlbi.md)  
  
-   [Member 元素&#40;CSDLBI&#41;](member-element-csdlbi.md)  
  
-   [MemberRef 元素&#40;CSDLBI&#41;](memberref-element-csdlbi.md)  
  
-   [NavigationProperty 元素&#40;CSDLBI&#41;](navigationproperty-element-csdlbi.md)  
  
-   [属性元素&#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [PropertyRef 元素&#40;CSDLBI&#41;](propertyref-element-csdlbi.md)  
  
## <a name="simple-type-and-subtypes"></a>简单类型和子类型  
 下表列出了包括在上面所列的复杂类型定义中的一些简单类型和一些次要复杂类型。 右侧列中列出的父元素中将提供在左侧列中列出的每个简单类型或子类型的文档。  
  
|简单类型|可在以下主题中找到|  
|-----------------|--------------------|  
|Alignment|[BaseProperty 元素&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|CompareOptions|[EntityContainer 元素&#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|目录|[EntityType 元素&#40;CSDLBI&#41;](entitytype-element-csdlbi.md)|  
|ContextualNameRule|[Member 元素&#40;CSDLBI&#41;](member-element-csdlbi.md)|  
|DefaultAggregationFunction|[属性元素&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|DirectQueryMode|[EntityContainer 元素&#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|GroupingBehavior|[属性元素&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|MemberRefs|[MemberRef 元素&#40;CSDLBI&#41;](memberref-element-csdlbi.md)|  
|PropertyRefs|[PropertyRef 元素&#40;CSDLBI&#41;](propertyref-element-csdlbi.md)|  
|SortDirection|[BaseProperty 元素&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|State|[AssociationSet 元素&#40;CSDLBI&#41;](associationset-element-csdlbi.md)|  
|稳定性|[属性元素&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|SortDirection|[BaseProperty 元素&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
  
## <a name="see-also"></a>请参阅  
 [CSDLBI 概念](../csdlbi-concepts.md)  
  
  
