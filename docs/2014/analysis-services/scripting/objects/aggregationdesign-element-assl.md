---
title: AggregationDesign 元素 (ASSL) |Microsoft 文档
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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c8b02460500a79d1ff98dfac84a07782c388ef10
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018030"
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
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationDesign>。  
  
## <a name="see-also"></a>请参阅  
 [分区元素&#40;ASSL&#41;](partition-element-assl.md)   
 [聚合元素&#40;ASSL&#41;](aggregation-element-assl.md)   
 [聚合元素&#40;ASSL&#41;](../collections/aggregations-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  