---
title: 分区元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cacc02776c1886caf4a8a46557ac01d2d33257c5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036498"
---
# <a name="partition-element-assl"></a>Partition 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义的分区[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)元素或扩展的行中的分区绑定[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)元素。  
  
## <a name="syntax"></a>語法  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|请参阅下表。|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
|祖先或父级|数据类型|  
|------------------------|---------------|  
|[度量值组](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|无|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[分区](../../../analysis-services/scripting/collections/partitions-element-assl.md)|  
|子元素|请参阅下表。|  
  
|祖先或父级|子元素|  
|------------------------|--------------------|  
|[度量值组](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[AggregationDesignID](../../../analysis-services/scripting/properties/aggregationdesignid-element-assl.md)， [AggregationInstances](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)， [AggregationInstanceSource](../../../analysis-services/scripting/properties/aggregationinstancesource-element-assl.md)， [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md)，[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)， [CurrentStorageMode](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)， [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)， [EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md)， [EstimatedSize](../../../analysis-services/scripting/properties/estimatedsize-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)， [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)， [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)， [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md)， [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md)， [RemoteDatasourceID](../../../analysis-services/scripting/properties/remotedatasourceid-element-assl.md)，[切片](../../../analysis-services/scripting/properties/slice-element-assl.md)，[源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)，[状态](../../../analysis-services/scripting/properties/state-element-assl.md)， [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)， [StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md)，[类型](../../../analysis-services/scripting/properties/type-element-partition-assl.md)|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|無|  
  
## <a name="remarks"></a>注释  
 此元素在 DeploymentMode 值 2（表格服务器模式）下具有以下验证：  
  
-   不支持也不应使用以下子元素：  
  
    -   [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md)  
  
    -   [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md)  
  
    -   [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)  
  
    -   [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md)  
  
    -   [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)  
  
    -   [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)  
  
    -   [RemoteDatasourceID](../../../analysis-services/scripting/properties/remotedatasourceid-element-assl.md)  
  
    -   [切片](../../../analysis-services/scripting/properties/slice-element-assl.md)  
  
    -   [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)  
  
    -   [类型](../../../analysis-services/scripting/properties/type-element-partition-assl.md)  
  
    -   [CurrentStorageMode](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md)  
  
    -   [AggregationDesignID](../../../analysis-services/scripting/properties/aggregationdesignid-element-assl.md)  
  
    -   [AggregationInstances](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)  
  
    -   [AggregationInstanceSource](../../../analysis-services/scripting/properties/aggregationinstancesource-element-assl.md)  
  
     如果使用了任何上述元素，则可能会引发错误。  
  
-   [源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)元素只接受**查询**绑定。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
