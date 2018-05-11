---
title: 源元素 （绑定） (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 078f4d9f9e1b7ab1229b754a9d110e172d7c3133
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="source-element-binding-assl"></a>Source 元素（绑定）(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  标识父元素绑定到的数据源。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationInstance> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Source>...</Source>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|请参阅下表。|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
|祖先或父级|数据类型|  
|------------------------|---------------|  
|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|[AggregationInstanceMeasure](../../../analysis-services/scripting/data-type/aggregationinstancemeasure-data-type-assl.md)|[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|  
|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|派生自任何数据类型[绑定](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)，具体的父取决于**DataItem**。 有关详细信息，请参阅“备注”。|  
|[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)， [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[度量值组](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|[MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|[CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|  
|[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)|[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|派生自任何数据类型[ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)，具体使用的父级的处理和通知选项取决于**ProactiveCaching**元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)， [AggregationInstanceMeasure](../../../analysis-services/scripting/data-type/aggregationinstancemeasure-data-type-assl.md)，[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)， [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)，[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)， [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)。|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 在**源**元素、 派生**绑定**中允许的数据类型**DataItem**元素依赖于的父**DataItem**元素。  
  
|DataItem 父级|允许的数据类型|  
|---------------------|------------------------|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [TimeAttributeBinding](../../../analysis-services/scripting/data-type/timeattributebinding-data-type-assl.md) (仅针对[KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md))。|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)。|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
  
 有关详细信息**绑定**类型，包括表的 Analysis Services 脚本语言 (ASSL) 对象**绑定**类型和继承层次结构的**绑定**类型，请参阅[绑定数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)。  
  
 有关在 ASSL 中的数据绑定的详细信息，请参阅[数据源和绑定 & #40;SSAS 多维 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
