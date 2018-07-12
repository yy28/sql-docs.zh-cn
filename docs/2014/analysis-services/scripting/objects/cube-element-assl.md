---
title: 多维数据集元素 (ASSL) |Microsoft Docs
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
- Cube Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Cube
helpviewer_keywords:
- Cube element
ms.assetid: 2d801066-6cca-4a99-bbd8-56a38d762108
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eab8cc56de346540491664a60c644ef868b02a25
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165258"
---
# <a name="cube-element-assl"></a>Cube 元素 (ASSL)
  定义的常规、 虚拟或链接多维数据集中[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [数据库](database-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cubes>  
   <Cube>  
            <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
            <Description>...</Description>  
            <Language>...</Language>  
            <Collation>...</Collation>  
            <Translations>...</Translations>  
      <Dimensions>...</Dimensions>  
            <CubePermissions>...</CubePermissions>  
      <MdxScripts>...</MdxScripts>  
      <Perspectives>...</Perspectives>  
      <State>...</State>  
      <DefaultMeasure>...</DefaultMeasure>  
      <Visible>...</Visible>  
      <MeasureGroups>...</MeasureGroups>  
      <DataSourceView >...</Source>  
      <AggregationPrefix>...</AggregationPrefix>  
      <ProcessingPriority>...</ProcessingPriority>  
            <StorageMode>...</StorageMode>  
      <ProcessingMode>...</ProcessingMode>  
      <ScriptCacheProcessingMode>...</ScriptCacheProcessingMode>  
      <ProactiveCaching>...</ProactiveCaching>  
            <Kpis>...</Kpis>  
            <ErrorConfiguration>...</ErrorConfiguration>  
            <Actions>...</Actions>  
      <StorageLocation>...</StorageLocation>  
      <EstimatedRows>...</EstimatedRows>  
      <LastProcessed>...</LastProcessed>  
      <Annotations>...</Annotations>  
   </Cube>  
</Cubes>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../collections/cubes-element-assl.md)|  
|子元素|[操作](../collections/actions-element-assl.md)， [AggregationPrefix](../properties/aggregationprefix-element-assl.md)，[批注](../collections/annotations-element-assl.md)，[排序规则](../properties/collation-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [CubePermissions](../collections/cubepermissions-element-assl.md)， [DefaultMeasure](measure-element-assl.md)，[说明](../properties/description-element-assl.md)，[维度](../collections/dimensions-element-assl.md)， [ErrorConfiguration](errorconfiguration-element-assl.md)[EstimatedRows](../properties/estimatedrows-element-assl.md)， [ID](../properties/id-element-assl.md)， [Kpi](../collections/kpis-element-assl.md)，[语言](../properties/language-element-assl.md)， [LastProcessed](../properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [MdxScripts](../collections/mdxscripts-element-assl.md)， [MeasureGroups](../collections/groups-element-assl.md)，[名称](../properties/name-element-assl.md)，[透视](../collections/perspectives-element-assl.md)， [ProactiveCaching](proactivecaching-element-assl.md)， [ProcessingMode](../properties/processingmode-element-assl.md)， [ProcessingPriority](../properties/processingpriority-element-assl.md)， [ScriptCacheProcessingMode](../properties/scriptcacheprocessingmode-element-assl.md)，[状态](../properties/state-element-assl.md)， [StorageLocation](../properties/storagelocation-element-assl.md)， [StorageMode](../properties/storagemode-element-assl.md)，[翻译](../collections/translations-element-assl.md)，[可见](../properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Cube>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
