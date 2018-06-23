---
title: CubeDimension 数据类型 (ASSL) |Microsoft 文档
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
- CubeDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeDimension
helpviewer_keywords:
- CubeDimension data type
ms.assetid: 128ac790-65a1-4e35-b909-8dba2a61b24c
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4a043895929e09a59d3ae14c5995804c4fa5c7eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014935"
---
# <a name="cubedimension-data-type-assl"></a>CubeDimension 数据类型 (ASSL)
  定义一个基元数据类型，该类型表示维度和多维数据集之间的关系。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeDimension>  
      <ID>...</ID>  
   <Name>...</Name>  
   <Translations>...</Translations>  
   <DimensionID>...</DimensionID>  
   <Visible>...</Visible>  
   <AllMemberAggregationUsage>...</AllMemberAggregationUsage>  
   <HierarchyUniqueNameStyle>...</HierarchyUniqueNameStyle>  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
      <Attributes>...</Attributes>  
   <Hierarchies>...</Hierarchies>  
      <Annotations>...</Annotation>  
</CubeDimension>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[AllMemberAggregationUsage](../properties/aggregationusage-element-assl.md)，[批注](../collections/annotations-element-assl.md)，[属性](../collections/attributes-element-assl.md)， [DimensionID](../properties/id-element-assl.md)，[层次结构](../collections/hierarchies-element-assl.md)， [HierarchyUniqueNameStyle](../properties/hierarchyuniquenamestyle-element-assl.md)， [ID](../properties/id-element-assl.md)， [MemberUniqueNameStyle](../properties/memberuniquenamestyle-element-assl.md)，[名称](../properties/name-element-assl.md)，[可见](../properties/visible-element-assl.md)，[翻译](../collections/translations-element-assl.md)|  
|派生元素|[维度](../objects/dimension-element-assl.md)([维度](../collections/dimensions-element-assl.md)集合[多维数据集](../objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 `CubeDimension` 上的每个维度关系有一个 `Cube`。 `CubeDimension` 涵盖多维数据集的所有 `MeasureGroups`。  
  
 A`CubeDimension`必须包括[CubeHierarchy](hierarchy-data-type-assl.md)如果维度有某个特定层次结构的看法，包括禁用层次结构 （从而，允许种层次结构适用于特定的选择维度用法），或使层次结构不可见。  
  
 同样，`CubeDimension`必须包括[CubeAttribute](cubeattribute-data-type-assl.md)仅当该维度具有特定于假设该属性有关的内容。 （可使属性不可见，但无法选择哪些属性应用于特定维度用法）。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CubeDimension>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  