---
title: MeasureGroupDimension 数据类型 (ASSL) |Microsoft Docs
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
- MeasureGroupDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupDimension
helpviewer_keywords:
- MeasureGroupDimension data type
ms.assetid: 9d1c1c19-31ce-4c42-b2e6-4c1b08875a83
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dcbba7071e1f2efc8ede59259a48a334652de81
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249117"
---
# <a name="measuregroupdimension-data-type-assl"></a>MeasureGroupDimension 数据类型 (ASSL)
  定义一个抽象的基元数据类型，该类型表示某个维度和度量值组之间的关系。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroupDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
      <Annotations>...</Annotations>  
   <Source>...</Source>  
</MeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|[DataMiningMeasureGroupDimension](dimension-data-type-assl.md)， [DegenerateMeasureGroupDimension](measuregroupdimension-data-type-assl.md)， [ManyToManyMeasureGroupDimension](manytomanymeasuregroupdimension-data-type-assl.md)， [ReferenceMeasureGroupDimension](referencemeasuregroupdimension-data-type-assl.md)， [RegularMeasureGroupDimension](regularmeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[批注](../collections/annotations-element-assl.md)， [CubeDimensionID](../properties/id-element-assl.md)，[源](../properties/source-element-binding-assl.md)|  
|派生元素|[维度](../objects/dimension-element-assl.md)([维度](../collections/dimensions-element-assl.md)的集合[MeasureGroup](../objects/group-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 每个 `MeasureGroupDimension` 都是对多维数据集中的一个维度的引用。 它们定义哪些多维数据集维度应用于度量值组。  
  
 提供的属性集确定度量值组中哪个粒度（范围）的度量值为已知。 例如，表示产品销售额的度量值包含在“销售”度量值组中。 这些度量值的信息将按月，而不是按周或天的粒度存储到基础数据源中。 在这种情况下，对描述时间维度和“销售”度量值组之间关系的 `MeasureGroupDimension`，只列出“Month”属性。 在极少数情况下，粒度可能是以一组属性定义的。 例如，给定属性集 {Day, Week, Month, Year}，其中 Day 隐含 Week 和 Month，但 Week 不隐含 Month，“预测”度量值组中包含的度量值可能对 Month 和 Week 来说为已知，但对 Day 来说为未知。  
  
 如果未提供任何属性，则如同只列出维度的键属性（定义最低级别的粒度）。 度量值组的每个分区必须具有相同的粒度。 列出的属性集的各属性间不应包含冗余的关系。 例如，如果 Month 隐含 Year，则粒度应被定义为 Month，而不应为 Month 和 Year。  
  
 仅当 `MeasureGroupDimension` 具有某些特定于层次结构的内容时，才需要包含层次结构来指示特定内容。 （无法选择哪些层次结构应用于特定度量值组）。 同样，它需要包含[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)仅当具有某些特定以指示有关它。  
  
 每个层次结构必须是包含在层次结构的子集[CubeDimension](cubedimension-data-type-assl.md)。 级别无法选择，尽管某些级别会根据度量值组的粒度被自动禁用。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MeasureGroupDimension>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
