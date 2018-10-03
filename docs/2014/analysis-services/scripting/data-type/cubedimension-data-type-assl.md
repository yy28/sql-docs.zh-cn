---
title: CubeDimension 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c3ea688681749a2b22f8c457fb9a5eb8ee39d8eb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059507"
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
|基本数据类型|None|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[AllMemberAggregationUsage](../properties/aggregationusage-element-assl.md)，[批注](../collections/annotations-element-assl.md)，[特性](../collections/attributes-element-assl.md)， [DimensionID](../properties/id-element-assl.md)，[层次结构](../collections/hierarchies-element-assl.md)， [HierarchyUniqueNameStyle](../properties/hierarchyuniquenamestyle-element-assl.md)， [ID](../properties/id-element-assl.md)， [MemberUniqueNameStyle](../properties/memberuniquenamestyle-element-assl.md)，[名称](../properties/name-element-assl.md)，[可见](../properties/visible-element-assl.md)，[翻译](../collections/translations-element-assl.md)|  
|派生元素|[维度](../objects/dimension-element-assl.md)([维度](../collections/dimensions-element-assl.md)的集合[多维数据集](../objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>备注  
 `CubeDimension` 上的每个维度关系有一个 `Cube`。 `CubeDimension` 涵盖多维数据集的所有 `MeasureGroups`。  
  
 一个`CubeDimension`必须包含[CubeHierarchy](hierarchy-data-type-assl.md)如果维度有某些特定于对层次结构，包括禁用层次结构 （从而允许这些层次结构应用于特定的选择维度用法），或使层次结构不可见。  
  
 同样，`CubeDimension`必须包含[CubeAttribute](cubeattribute-data-type-assl.md)仅当维度有某些特定于对属性。 （可使属性不可见，但无法选择哪些属性应用于特定维度用法）。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CubeDimension>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
