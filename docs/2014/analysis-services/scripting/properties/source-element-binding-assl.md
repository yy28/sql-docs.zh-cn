---
title: 源元素 （绑定） (ASSL) |Microsoft 文档
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
- Source Element (Binding)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 1032558c-7546-4ca7-888d-8139df23cb62
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 58bacab7c84d1432a57d16c709b08c8c79ac143d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127602"
---
# <a name="source-element-binding-assl"></a>Source 元素（绑定）(ASSL)
  标识父元素绑定到的数据源。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationInstance> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Source>...</Source>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|下，请参阅数据类型表|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
 **数据类型和长度**  
  
|||  
|-|-|  
|祖先或父级|数据类型|  
|[AggregationInstance](../data-type/binding-data-type-assl.md)|  
|[AggregationInstanceMeasure](../data-type/columnbinding-data-type-assl.md)|  
|[Cube](../data-type/datasourceviewbinding-data-type-assl.md)|  
|[DataItem](../data-type/dataitem-data-type-assl.md)|派生自任何数据类型[绑定](../data-type/binding-data-type-assl.md)，具体的父取决于`DataItem`。 有关详细信息，请参阅“备注”。|  
|[维度](../data-type/dimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)， [TimeBinding](../data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../data-type/attributebinding-data-type-assl.md)， [UserDefinedGroupBinding](../data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[度量值组](../data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupDimension](../data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)|[CubeDimensionBinding](../data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)|  
|分区[](../data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|派生自任何数据类型[ProactiveCachingBinding](../data-type/proactivecachingbinding-data-type-assl.md)，具体使用的父级的处理和通知选项取决于`ProactiveCaching`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationInstance](../objects/aggregationinstance-element-assl.md)， [AggregationInstanceMeasure](../data-type/aggregationinstancemeasure-data-type-assl.md)，[多维数据集](../objects/cube-element-assl.md)， [DataItem](../data-type/dataitem-data-type-assl.md)，[维度](../objects/dimension-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)， [MeasureGroup](../objects/group-element-assl.md)， [MeasureGroupDimension](../data-type/dimension-data-type-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)，[分区](../objects/partition-element-assl.md)， [ProactiveCaching](../objects/proactivecaching-element-assl.md)。|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 在 `Source` 元素中，`Binding` 元素允许的派生的 `DataItem` 数据类型取决于 `DataItem` 元素的父级。  
  
|DataItem 父级|允许的数据类型|  
|---------------------|------------------------|  
|[DimensionAttribute](../data-type/attributebinding-data-type-assl.md)， [ColumnBinding](../data-type/columnbinding-data-type-assl.md)， [TimeAttributeBinding](../data-type/timeattributebinding-data-type-assl.md) (仅针对[KeyColumns](../collections/columns-element-assl.md))。|  
|[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)|[AttributeBinding](../data-type/attributebinding-data-type-assl.md)， [ColumnBinding](../data-type/columnbinding-data-type-assl.md)， [InheritedBinding](../data-type/inheritedbinding-data-type-assl.md)。|  
|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[ColumnBinding](../data-type/columnbinding-data-type-assl.md)|  
  
 有关详细信息`Binding`类型，包括表的 Analysis Services 脚本语言 (ASSL) 对象`Binding`类型和继承层次结构的`Binding`类型，请参阅[绑定数据类型&#40;ASSL&#41;](../data-type/binding-data-type-assl.md).  
  
 有关在 ASSL 中的数据绑定的详细信息，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  