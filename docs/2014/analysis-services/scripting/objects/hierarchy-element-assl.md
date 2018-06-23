---
title: 层次结构元素 (ASSL) |Microsoft 文档
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
api_name:
- Hierarchy Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy element
ms.assetid: ac54d74a-5e6c-4c24-83bf-766440478f6c
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6c5acacc00f072f50cc0429c345b5a2fedc6afc6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129075"
---
# <a name="hierarchy-element-assl"></a>Hierarchy 元素 (ASSL)
  定义维度中的层次结构。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Hierarchies>  
   <Hierarchy xsi:type="Hierarchy">...</Hierarchy> <!-- ancestor: Dimension -->  
   <!-- or -->  
   <Hierarchy xsi:type="CubeHierarchy">...</Hierarchy> <!-- ancestor: CubeDimension -->  
   <!-- or -->  
   <Hierarchy xsi:type="PerspectiveHierarchy">...</Hierarchy> <!-- ancestor: PerspectiveDimension -->  
   <!-- or -->  
   <Hierarchy xsi:type="MeasureGroupHierarchy">...</Hierarchy> <!-- ancestor: RegularMeasureGroupDimension -->  
</Hierarchies>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度||  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="data-type-and-length"></a>数据类型和长度  
  
|祖先或父级|数据类型|  
|------------------------|---------------|  
|[Dimension](../data-type/hierarchy-data-type-assl.md)|  
|[CubeDimension](../data-type/cubehierarchy-data-type-assl.md)|  
|[PerspectiveDimension](../data-type/perspectivehierarchy-data-type-assl.md)|  
|[RegularMeasureGroupDimension](../data-type/measuregrouphierarchy-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[层次结构](../collections/hierarchies-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中，对应的元素为 <xref:Microsoft.AnalysisServices.Hierarchy>、<xref:Microsoft.AnalysisServices.CubeHierarchy> 和 <xref:Microsoft.AnalysisServices.PerspectiveHierarchy>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  