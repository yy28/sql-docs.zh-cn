---
title: AggregationInstance 元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 414284bc1cc0bc1b8d6b99697ace00b770dd7a02
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="aggregationinstance-element-assl"></a>AggregationInstance 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义分区的聚合实例。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationInstances>  
   <AggregationInstance>  
      <AggregationType>...</AggregationType>  
      <AggregationID>...</AggregationID>  
      <Source>...</Source>  
      <Dimensions>...</Dimensions>  
      <Measures>...</Measures>  
      <Annotations>...</Annotations>  
   </AggregationInstance>  
</AggregationInstances>  
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
|父元素|[AggregationInstances](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)|  
|子元素|[AggregationID](../../../analysis-services/scripting/properties/aggregationid-element-assl.md)， [AggregationType](../../../analysis-services/scripting/properties/aggregationtype-element-assl.md)，[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[维度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)，[度量值](../../../analysis-services/scripting/collections/measures-element-assl.md)，[源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>注释  
 当[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)元素使用[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)元素以生成该分区的聚合每个[聚合](../../../analysis-services/scripting/objects/aggregation-element-assl.md)中**AggregationDesign**为该分区实例化。 多个分区可使用同一聚合设计来生成已定义聚合的多个实例。 **AggregationInstance**元素表示的定义聚合的实例。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationInstance>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
