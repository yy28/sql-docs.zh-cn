---
title: 属性元素 (ASSL) |Microsoft Docs
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
- Attribute Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Attribute
helpviewer_keywords:
- Attribute element
ms.assetid: 079ec9f8-a314-4e3c-821a-b42c65cc7363
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e94fcb4fdffacfad0bbf735bfc2fe3c7b19b798
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171458"
---
# <a name="attribute-element-assl"></a>Attribute 元素 (ASSL)
  包含对属性的说明。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Attributes>  
   <Attribute xsi:type="AggregationAttribute">...</Attribute> <!-- ancestor: AggregationDimension -->  
   <!-- or -->  
   <Attribute xsi:type="AggregationDesignAttribute">...</Attribute> <!-- ancestor: AggregationDesignDimension -->  
   <!-- or -->  
   <Attribute xsi:type="AggregationInstanceAttribute">...</Attribute> <!-- ancestor: AggregationInstanceCubeDimension -->  
   <!-- or -->  
   <Attribute xsi:type="CubeAttribute">...</Attribute> <!--ancestor:  CubeDimension -->  
   <!-- or -->  
   <Attribute xsi:type="DimensionAttribute">...</Attribute> <!-- ancestor: Dimension -->  
   <!-- or -->  
   <Attribute xsi:type="MeasureGroupAttribute">...</Attribute> <!-- ancestor: RegularMeasureGroupDimension -->  
   <!-- or -->  
   <Attribute xsi:type="PerspectiveAttribute">...</Attribute> <!-- ancestor: PerspectiveDimension -->  
   <!-- or -->  
   <Attribute>  
      <AttributeID>...</AttributeID>  
   </Attribute> <!-- ancestor: RelationshipEnd -->  
</Attributes>  
```  
  
## <a name="element-characteristics"></a>元素特征  
 默认值： 无  
  
 基数： 0-1： 可出现一次且仅一次出现的可选元素。  
  
|祖先或父级|数据类型|  
|------------------------|---------------|  
|[AggregationDesignDimension](../data-type/aggregationdesignattribute-data-type-assl.md)|  
|[AggregationDimension](../data-type/aggregationattribute-data-type-assl.md)|  
|[AggregationInstanceCubeDimension](../data-type/aggregationinstanceattribute-data-type-assl.md)|  
|[CubeDimension](../data-type/cubeattribute-data-type-assl.md)|  
|[Dimension](../data-type/dimensionattribute-data-type-assl.md)|  
|[RegularMeasureGroupDimension](../data-type/measuregroupattribute-data-type-assl.md)|  
|[PerspectiveDimension](../data-type/perspectiveattribute-data-type-assl.md)|  
|[RelationshipEnd](../data-type/relationshipend-data-type-assl.md)|\<属性 ><br />      \<[AttributeID](../properties/id-element-assl.md)>...\</AttributeID > \< /属性 >|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[属性](../collections/attributes-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationDesignAttribute>， <xref:Microsoft.AnalysisServices.AggregationAttribute>， <xref:Microsoft.AnalysisServices.CubeAttribute>， <xref:Microsoft.AnalysisServices.DimensionAttribute>， <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>，并<xref:Microsoft.AnalysisServices.PerspectiveAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
