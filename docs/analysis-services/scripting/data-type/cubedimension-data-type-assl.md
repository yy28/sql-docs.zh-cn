---
title: CubeDimension 数据类型 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e7fd3894b7b1d255a8760da4822eff0de1315b72
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="cubedimension-data-type-assl"></a>CubeDimension 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义一个基元数据类型，该类型表示维度和多维数据集之间的关系。  
  
## <a name="syntax"></a>語法  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[AllMemberAggregationUsage](../../../analysis-services/scripting/properties/allmemberaggregationusage-element-assl.md)，[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[属性](../../../analysis-services/scripting/collections/attributes-element-assl.md)， [DimensionID](../../../analysis-services/scripting/properties/dimensionid-element-assl.md)，[层次结构](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)， [HierarchyUniqueNameStyle](../../../analysis-services/scripting/properties/hierarchyuniquenamestyle-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)， [MemberUniqueNameStyle](../../../analysis-services/scripting/properties/memberuniquenamestyle-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)，[可见](../../../analysis-services/scripting/properties/visible-element-assl.md)，[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|派生元素|[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)([维度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)集合[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>注释  
 还有一个**CubeDimension**上每个维度关系**多维数据集**。 **CubeDimension**涵盖所有**MeasureGroups**的多维数据集。  
  
 A **CubeDimension**必须包括[CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)如果维度有某个特定层次结构的看法，包括禁用层次结构 （从而，允许其中的选定内容层次结构将应用到特定维度用法），或使层次结构不可见。  
  
 同样， **CubeDimension**必须包括[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)仅当该维度具有特定于假设该属性有关的内容。 （可使属性不可见，但无法选择哪些属性应用于特定维度用法）。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CubeDimension>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
