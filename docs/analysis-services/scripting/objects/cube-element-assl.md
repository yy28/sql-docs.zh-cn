---
title: "多维数据集元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Cube Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Cube
helpviewer_keywords:
- Cube element
ms.assetid: 2d801066-6cca-4a99-bbd8-56a38d762108
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bd8bd9f2f76070f697b9fdabe6c488b2f51838b0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="cube-element-assl"></a>Cube 元素 (ASSL)
  定义正则、 虚拟的或链接的多维数据集在[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../../../analysis-services/scripting/collections/cubes-element-assl.md)|  
|子元素|[操作](../../../analysis-services/scripting/collections/actions-element-assl.md)， [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md)，[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[排序规则](../../../analysis-services/scripting/properties/collation-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)， [CubePermissions](../../../analysis-services/scripting/collections/cubepermissions-element-assl.md)， [DefaultMeasure](../../../analysis-services/scripting/properties/defaultmeasure-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)，[维度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)， [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)[EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)， [Kpi](../../../analysis-services/scripting/collections/kpis-element-assl.md)，[语言](../../../analysis-services/scripting/properties/language-element-assl.md)， [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)， [mdxscript 被](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)， [MeasureGroups](../../../analysis-services/scripting/collections/measuregroups-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)，[透视](../../../analysis-services/scripting/collections/perspectives-element-assl.md)， [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)， [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md)， [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md)， [ScriptCacheProcessingMode](../../../analysis-services/scripting/properties/scriptcacheprocessingmode-element-assl.md)，[状态](../../../analysis-services/scripting/properties/state-element-assl.md)， [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)， [StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md)，[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)，[可见](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Cube>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

