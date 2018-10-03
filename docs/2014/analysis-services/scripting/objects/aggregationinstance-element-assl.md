---
title: AggregationInstance 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationInstance Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- AggregationInstance element
ms.assetid: 2e77e9e1-9f2c-4df4-9aa6-5b7b911016a3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aef7afde2cf93d18ad0a567f5a5e1071b7e42ebf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177897"
---
# <a name="aggregationinstance-element-assl"></a>AggregationInstance 元素 (ASSL)
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationInstances](../collections/aggregationinstances-element-assl.md)|  
|子元素|[AggregationID](../properties/id-element-assl.md)， [AggregationType](../properties/aggregationtype-element-assl.md)，[批注](../collections/annotations-element-assl.md)，[维度](../collections/dimensions-element-assl.md)，[度量值](../collections/measures-element-assl.md)，[源](../properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>备注  
 当[分区](partition-element-assl.md)元素使用[AggregationDesign](aggregationdesign-element-assl.md)元素生成该分区的聚合每个[聚合](aggregation-element-assl.md)中`AggregationDesign`是为该分区实例化。 多个分区可使用同一聚合设计来生成已定义聚合的多个实例。 `AggregationInstance` 元素表示已定义聚合的一个实例。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationInstance>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
