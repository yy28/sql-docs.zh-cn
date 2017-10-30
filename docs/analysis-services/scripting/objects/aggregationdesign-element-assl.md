---
title: "AggregationDesign 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AggregationDesign Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationDesign
helpviewer_keywords:
- AggregationDesign element
ms.assetid: 80ad98d8-73a8-4353-b5ad-d2a9ac3bc531
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 37820498904def60b0bdbd35afddeccf461cdb34
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationDesigns](../../../analysis-services/scripting/collections/aggregationdesigns-element-assl.md)|  
|子元素|[聚合](../../../analysis-services/scripting/collections/aggregations-element-assl.md)，[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)，[维度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)， [EstimatedPerformanceGain](../../../analysis-services/scripting/properties/estimatedperformancegain-element-assl.md)， [EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationDesign>。  
  
## <a name="see-also"></a>另请参阅  
 [分区元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)   
 [聚合元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)   
 [聚合元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/aggregations-element-assl.md)   
 [对象 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

