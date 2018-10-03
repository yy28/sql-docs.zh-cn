---
title: AggregationDesign 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 430035dd83cf137cb80a5db5d159da027014e6c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075287"
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
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationDesigns](../collections/aggregationdesigns-element-assl.md)|  
|子元素|[聚合](../collections/aggregations-element-assl.md)，[批注](../collections/annotations-element-assl.md)，[说明](../properties/description-element-assl.md)，[维度](../collections/dimensions-element-assl.md)， [EstimatedPerformanceGain](../properties/estimatedperformancegain-element-assl.md)， [EstimatedRows](../properties/estimatedrows-element-assl.md)， [ID](../properties/id-element-assl.md)，[名称](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationDesign>。  
  
## <a name="see-also"></a>请参阅  
 [分区元素&#40;ASSL&#41;](partition-element-assl.md)   
 [Aggregation 元素&#40;ASSL&#41;](aggregation-element-assl.md)   
 [Aggregations 元素&#40;ASSL&#41;](../collections/aggregations-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
