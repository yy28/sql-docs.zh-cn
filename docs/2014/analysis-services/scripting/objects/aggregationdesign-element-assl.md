---
title: AggregationDesign 元素 (ASSL) |Microsoft Docs
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
- AggregationDesign Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationDesign
helpviewer_keywords:
- AggregationDesign element
ms.assetid: 80ad98d8-73a8-4353-b5ad-d2a9ac3bc531
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cfebce28ae08d0d76fa851b9d9df3ded8f6c28fc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200087"
---
# <a name="aggregationdesign-element-assl"></a>AggregationDesign 元素 (ASSL)
  定义一组可由数据库中的多个分区共享的聚合定义。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationDesigns>  
   <AggregationDesign>  
      <ID>...</ID>  
      <Name>...</Name>  
            <Description>...</Description>  
      <EstimatedRows>...</EstimatedRows>  
      <Dimensions>...</Dimensions>  
            <Aggregations>...</Aggregation>  
      <EstimatedPerformanceGain>...</EstimatedPerformanceGain>  
      <Annotations>...</Annotations>  
   </AggregationDesign>  
</AggregationDesigns>  
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
|父元素|[AggregationDesigns](../collections/aggregationdesigns-element-assl.md)|  
|子元素|[聚合](../collections/aggregations-element-assl.md)，[批注](../collections/annotations-element-assl.md)，[说明](../properties/description-element-assl.md)，[维度](../collections/dimensions-element-assl.md)， [EstimatedPerformanceGain](../properties/estimatedperformancegain-element-assl.md)， [EstimatedRows](../properties/estimatedrows-element-assl.md)， [ID](../properties/id-element-assl.md)，[名称](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationDesign>。  
  
## <a name="see-also"></a>请参阅  
 [分区元素&#40;ASSL&#41;](partition-element-assl.md)   
 [Aggregation 元素&#40;ASSL&#41;](aggregation-element-assl.md)   
 [Aggregations 元素&#40;ASSL&#41;](../collections/aggregations-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
