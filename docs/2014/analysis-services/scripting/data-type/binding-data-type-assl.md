---
title: Binding 数据类型 (ASSL) |Microsoft Docs
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
- Binding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- BINDING
helpviewer_keywords:
- Binding data type
ms.assetid: 0a777219-b885-4961-ac66-b76faeb520db
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a34209ea08d1cdfd0100bd5e2402edc0f592f066
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169538"
---
# <a name="binding-data-type-assl"></a>Binding 数据类型 (ASSL)
  定义一个抽象的基元数据类型，该类型表示两个对象之间的依赖关系：在这两个对象中，一个对象的数据或元数据依赖于绑定对象的数据或元数据。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Binding>...</Binding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|[AttributeBinding](binding-data-type-assl.md)， [ColumnBinding](columnbinding-data-type-assl.md)， [CubeAttributeBinding](cubeattributebinding-data-type-assl.md)， [CubeDimensionBinding](dimensionbinding-data-type-assl.md)， [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)， [DimensionBinding](dimensionbinding-data-type-assl.md)， [InheritedBinding](inheritedbinding-data-type-assl.md)， [MeasureBinding](measurebinding-data-type-assl.md)， [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)， [MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)， [ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md)， [RowBinding](rowbinding-data-type-assl.md)， [TabularBinding](tabularbinding-data-type-assl.md)， [TimeAttributeBinding](timeattributebinding-data-type-assl.md)， [TimeBinding](timebinding-data-type-assl.md)， [UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|InclusionThresholdSetting|  
|派生元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Binding>。  
  
 有关数据绑定的详细信息，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="elements-of-type-binding"></a>Binding 类型的元素  
 下表列出了 `Binding` 类型的元素。  
  
|父元素|`Binding` 类型的元素|注释|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../properties/source-element-binding-assl.md)的[CaptionColumn](../objects/column-element-assl.md) (类型的[DataItem](dataitem-data-type-assl.md))|类型`Binding`必须是[AttributeBinding](binding-data-type-assl.md)或[ColumnBinding](columnbinding-data-type-assl.md)|  
|[Cube](../objects/cube-element-assl.md)|[数据源](../properties/source-element-binding-assl.md)|类型`Binding`必须是[DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding （外部）](../objects/group-element-assl.md)|类型`Binding`必须是[MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[DataItem](dataitem-data-type-assl.md)|[数据源](../properties/source-element-binding-assl.md)|`Binding` 可以是任何类型。|  
|[Dimension](../objects/dimension-element-assl.md)|[数据源](../properties/source-element-binding-assl.md)|类型`Binding`必须是[CubeDimensionBinding](dimensionbinding-data-type-assl.md)， [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)， [DimensionBinding](dimensionbinding-data-type-assl.md)，或[TimeBinding](timebinding-data-type-assl.md)|  
|[DimensionAttribute](dimensionattribute-data-type-assl.md)|[数据源](../properties/source-element-binding-assl.md)|类型`Binding`必须是[AttributeBinding](binding-data-type-assl.md)或[UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](action-data-type-assl.md)|[列](../objects/column-element-assl.md)|类型`Binding`必须是[CubeAttributeBinding](cubeattributebinding-data-type-assl.md)或[MeasureBinding](measurebinding-data-type-assl.md)|  
|[度量值](../objects/measure-element-assl.md)|[源](../properties/source-element-binding-assl.md)(类型的[DataItem](dataitem-data-type-assl.md))|类型`Binding`必须是[ColumnBinding](columnbinding-data-type-assl.md)， [CubeDimensionBinding](dimensionbinding-data-type-assl.md)， [MeasureBinding](measurebinding-data-type-assl.md)，或[RowBinding](rowbinding-data-type-assl.md)|  
|[度量值组](../objects/measuregroup-element-assl.md)|[数据源](../properties/source-element-binding-assl.md)|类型`Binding`必须是[MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)|[源](../properties/source-element-binding-assl.md)的[KeyColumn](../objects/keycolumn-element-assl.md) (类型的[DataItem](dataitem-data-type-assl.md))|类型`Binding`必须是[AttributeBinding](binding-data-type-assl.md)或[ColumnBinding](columnbinding-data-type-assl.md)，或[InheritedBinding](inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding （外部）](measuregroupbinding-data-type-out-of-line-assl.md)|[Dimension](../objects/dimension-element-assl.md)|类型`Binding`必须是[MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding （外部）](measuregroupbinding-data-type-out-of-line-assl.md)|[度量值](../objects/measure-element-assl.md)|类型`Binding`必须是[MeasureBinding](measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding （外部）](../objects/partition-element-assl.md)|类型`Binding`必须是[PartitionBinding](partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding （外部）](measuregroupbinding-data-type-out-of-line-assl.md)|[数据源](../properties/source-element-binding-assl.md)|类型`Binding`必须是[TableBinding](tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](dimension-data-type-assl.md)|[数据源](../properties/source-element-binding-assl.md)|类型`Binding`必须是[MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)|[数据源](../properties/source-element-binding-assl.md)|类型`Binding`必须是[CubeDimensionBinding](dimensionbinding-data-type-assl.md)， [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)，或[DimensionBinding](dimensionbinding-data-type-assl.md)|  
|分区[](../objects/partition-element-assl.md)|[数据源](../properties/source-element-binding-assl.md)|类型`Binding`必须是[TabularBinding](tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|[数据源](../properties/source-element-binding-assl.md)|类型`Binding`必须是[ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[数据源](../properties/source-element-binding-assl.md)|类型`Binding`必须是[AttributeBinding](binding-data-type-assl.md)， [CubeAttributeBinding 数据类型&#40;ASSL&#41;](cubeattributebinding-data-type-assl.md)，或者[MeasureBinding 数据类型&#40;ASSL&#41;](measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../objects/sourcemeasuregroup-element-assl.md)|类型`Binding`必须是[MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
