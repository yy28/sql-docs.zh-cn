---
title: MeasureGroup 元素 (ASSL) |Microsoft Docs
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
- MeasureGroup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroup
helpviewer_keywords:
- MeasureGroup element
ms.assetid: 7aa099db-5dc7-4cac-b437-f73fc0921b24
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee73b594fde5e3a9e915615d1a343296ce846d52
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163368"
---
# <a name="measuregroup-element-assl"></a>MeasureGroup 元素 (ASSL)
  定义一组属于同一粒度级别的度量值。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroups>  
   <MeasureGroup> <!-- ancestor: Cube -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</<Create  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <LastProcessed>...</LastProcessed>  
      <Translations>...</Translations>  
      <Type>...</Type>  
      <State>...</State>  
      <MeasureQualification>...</MeasureQualification>  
      <Measures>...</Measures>  
      <DataAggregation>...</DataAggregation>  
      <Source>...</Source>  
            <StorageMode>...</StorageMode>  
      <StorageLocation>...</StorageLocation>  
      <IgnoreUnrelatedDimensions>...</IgnoreUnrelatedDimensions>  
            <ProactiveCaching>...</ProactiveCaching>  
      <EstimatedRows>...</EstimatedRows>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <EstimatedSize>...</EstimatedSize>  
      <ProcessingMode>...</ProcessingMode>  
      <Dimensions>...</Dimensions>  
      <Partitions>...</Partitions>  
      <AggregationPrefix>...</AggregationPrefix>  
      <ProcessingPriority>...</ProcessingPriority>  
            <AggregationDesigns>...</AggregationDesigns>  
      <Annotations>...</Annotations>  
   </MeasureGroup>  
   <!-- or  -->  
   <MeasureGroup xsi:type="MeasureGroupBinding">...</MeasureGroup> <!-- ancestor: CubeBinding -->  
   <!-- or  -->  
   <MeasureGroup xsi:type="PerspectiveMeasureGroup">...</MeasureGroup> <!-- ancestor: Perspective -->  
</MeasureGroups>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
|祖先或父级|数据类型|  
|------------------------|---------------|  
|[Cube](cube-element-assl.md)|InclusionThresholdSetting|  
|[CubeBinding](../data-type/binding-data-type-assl.md)|  
|[透视](../data-type/perspectivemeasuregroup-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MeasureGroups](../collections/groups-element-assl.md)|  
|子元素||  
  
|祖先或父级|子元素|  
|------------------------|--------------------|  
|[多维数据集](../collections/aggregationdesigns-element-assl.md)， [AggregationPrefix](../properties/aggregationprefix-element-assl.md)，[批注](../collections/annotations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [DataAggregation](aggregation-element-assl.md)， [描述](../properties/description-element-assl.md)，[维度](../collections/dimensions-element-assl.md)， [ErrorConfiguration](errorconfiguration-element-assl.md)， [EstimatedRows](../properties/estimatedrows-element-assl.md)， [EstimatedSize](../properties/estimatedsize-element-assl.md)，[ID](../properties/id-element-assl.md)， [IgnoreUnrelatedDimensions](../properties/ignoreunrelateddimensions-element-assl.md)， [LastProcessed](../properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [MeasureQualification](../properties/measurequalificaton-element-assl.md)，[度量值](../collections/measures-element-assl.md)，[名称](../properties/name-element-assl.md)，[分区](../collections/partitions-element-assl.md)， [ProactiveCaching](proactivecaching-element-assl.md)， [ProcessingMode](../properties/processingmode-element-assl.md)， [ProcessingPriority](../properties/processingpriority-element-assl.md)，[源](../properties/source-element-measure-assl.md)，[状态](../properties/state-element-assl.md)， [StorageLocation](../properties/storagelocation-element-assl.md)， [StorageMode](../properties/storagemode-element-assl.md)，[翻译](../collections/translations-element-assl.md)，[类型](../properties/type-element-measuregroup-assl.md)|  
|[CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md)|InclusionThresholdSetting|  
|[透视](perspective-element-assl.md)|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 度量值组中的所有度量值都必须源自单个表。 度量值组可定义可为每个分区重写的默认绑定。  
  
 `MeasureGroup` 元素定义常规多维数据集和虚拟多维数据集上的度量值组共有的详细信息。 单独的子类型定义特定于每种类型的详细信息。  
  
 `State` 的 `MeasureGroup` 属性具有以下值：  
  
-   处理了所有分区后，值为*FullyProcessed* 。  
  
-   处理了至少一个分区后，值为*PartiallyProcessed* 。  
  
-   如果未处理任何分区，则值为*Unprocessed* 。  
  
 在 Analysis Management Objects (AMO) 对象模型中，对应的元素为 <xref:Microsoft.AnalysisServices.MeasureGroup> 和 <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
