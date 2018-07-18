---
title: 分区元素 (ASSL) |Microsoft Docs
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
- Partition Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PARTITION
helpviewer_keywords:
- Partition element
ms.assetid: 40020840-1bb7-478f-9017-1a30342ac4c6
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c298ec80f1bb1f17d97e36f2ce93b6efbf924508
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209967"
---
# <a name="partition-element-assl"></a>Partition 元素 (ASSL)
  定义的分区[MeasureGroup](group-element-assl.md)元素或掉的行中的一个分区绑定[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Partitions>  
      <Partition> <!-- ancestor: MeasureGroup -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Source>...</Source>  
      <ProcessingPriority>...</ProcessingPriority>  
      <AggregationPrefix>...</AggregationPrefix>  
      <StorageMode>...</StorageMode>  
      <ProcessingMode>...</ProcessingMode>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <StorageLocation>...</StorageLocation>  
      <RemoteDatasourceID>...</RemoteDatasourceID>  
      <Slice>...</Slice>  
      <ProactiveCaching>...</ProactiveCaching>  
      <Type>...</Type>  
      <EstimatedSize>...</EstimatedSize>  
      <EstimatedRows>...</EstimatedRows>  
      <CurrentStorageMode>...</CurrentStorageMode>  
      <AggregationDesignID>...</AggregationDesignID>  
      <AggregationInstances>...</AggregationInstances>  
      <AggregationInstanceSource>...</AggregationInstanceSource>  
      <LastProcessed>...</LastProcessed>  
      <State>...</State>  
      <Annotations>.../Annotations>  
   </Partition>  
   <!-- or -->  
   <Partition xsi:type="PartitionBinding"> <!-- ancestor: MeasureGroupBinding -->  
   </Partition>  
</Partitions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
|祖先或父级|数据类型|  
|------------------------|---------------|  
|[度量值组](group-element-assl.md)|InclusionThresholdSetting|  
|[MeasureGroupBinding](../data-type/binding-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[分区](../collections/partitions-element-assl.md)|  
  
|祖先或父级|子元素|  
|------------------------|--------------------|  
|[MeasureGroup](../properties/id-element-assl.md)， [AggregationInstances](../collections/aggregationinstances-element-assl.md)， [AggregationInstanceSource](../properties/aggregationinstancesource-element-assl.md)， [AggregationPrefix](../properties/aggregationprefix-element-assl.md)，[批注](../collections/annotations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [CurrentStorageMode](../properties/storagemode-element-assl.md)，[说明](../properties/description-element-assl.md)， [ErrorConfiguration](errorconfiguration-element-assl.md)， [EstimatedRows](../properties/estimatedrows-element-assl.md)， [EstimatedSize](../properties/estimatedsize-element-assl.md)， [ID](../properties/id-element-assl.md)， [LastProcessed](../properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[名称](../properties/name-element-assl.md)， [ProactiveCaching](proactivecaching-element-assl.md)， [ProcessingMode](../properties/processingmode-element-assl.md)， [ProcessingPriority](../properties/processingpriority-element-assl.md)， [RemoteDatasourceID](../properties/datasourceid-element-assl.md)，[切片](../properties/slice-element-assl.md)，[源](../properties/source-element-binding-assl.md)，[状态](../properties/state-element-assl.md)， [StorageLocation](../properties/storagelocation-element-assl.md)， [StorageMode](../properties/storagemode-element-assl.md)，[类型](../properties/type-element-partition-assl.md)|  
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素在 DeploymentMode 值 2（表格服务器模式）下具有以下验证：  
  
-   不支持也不应使用以下子元素：  
  
    -   [ProcessingPriority](../properties/processingpriority-element-assl.md)  
  
    -   [AggregationPrefix](../properties/aggregationprefix-element-assl.md)  
  
    -   [StorageLocation](../properties/storagelocation-element-assl.md)  
  
    -   [ProcessingMode](../properties/processingmode-element-assl.md)  
  
    -   [ErrorConfiguration](errorconfiguration-element-assl.md)  
  
    -   [StorageLocation](../properties/storagelocation-element-assl.md)  
  
    -   [RemoteDatasourceID](../properties/datasourceid-element-assl.md)  
  
    -   [切片](../properties/slice-element-assl.md)  
  
    -   [ProactiveCaching](proactivecaching-element-assl.md)  
  
    -   [类型](../properties/type-element-partition-assl.md)  
  
    -   [CurrentStorageMode](../properties/storagemode-element-assl.md)  
  
    -   [AggregationDesignID](../properties/aggregationdesignid-element-assl.md)  
  
    -   [AggregationInstances](../collections/aggregationinstances-element-assl.md)  
  
    -   [AggregationInstanceSource](../properties/aggregationinstancesource-element-assl.md)  
  
     如果使用了任何上述元素，则可能会引发错误。  
  
-   [源](../properties/source-element-binding-assl.md)元素只接受**查询**绑定。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
