---
title: "绑定数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Binding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- BINDING
helpviewer_keywords:
- Binding data type
ms.assetid: 0a777219-b885-4961-ac66-b76faeb520db
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d252931193ef06109c1d353ddc8fa42b3e4b6dfb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="binding-data-type-assl"></a>Binding 数据类型 (ASSL)
  定义一个抽象的基元数据类型，该类型表示两个对象之间的依赖关系：在这两个对象中，一个对象的数据或元数据依赖于绑定对象的数据或元数据。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Binding>...</Binding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)， [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)， [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)， [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)， [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)， [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)， [ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)， [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)， [TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)， [TimeAttributeBinding](../../../analysis-services/scripting/data-type/timeattributebinding-data-type-assl.md)， [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)， [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|无|  
|派生元素|无|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Binding>。  
  
 有关数据绑定的详细信息，请参阅[数据源和绑定 &#40;SSAS 多维 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="elements-of-type-binding"></a>Binding 类型的元素  
 下表列出了类型的元素**绑定**。  
  
|父元素|类型的元素**绑定**|注释|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|[源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)的[CaptionColumn](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md) (类型的[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|键入的**绑定**必须[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)或[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|键入的**绑定**必须[DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding （外部）](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|[度量值组](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|键入的**绑定**必须[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|**绑定**可以是任何类型|  
|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|键入的**绑定**必须[CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)，或[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|键入的**绑定**必须[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)或[UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|[列](../../../analysis-services/scripting/objects/column-element-assl.md)|键入的**绑定**必须[CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)或[MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|[源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)(类型的[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|键入的**绑定**必须[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)，或[RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|  
|[度量值组](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|键入的**绑定**必须[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)的[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) (类型的[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|键入的**绑定**必须[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)或[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)，或[InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding （外部）](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|键入的**绑定**必须[MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding （外部）](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|键入的**绑定**必须[MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding （外部）](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)|键入的**绑定**必须[PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding （外部）](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|键入的**绑定**必须[TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|键入的**绑定**必须[MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|键入的**绑定**必须[CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)，或[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|  
|[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|键入的**绑定**必须[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|键入的**绑定**必须[ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|键入的**绑定**必须[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [CubeAttributeBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)，或[MeasureBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[SourceMeasureGroup](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|键入的**绑定**必须[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

