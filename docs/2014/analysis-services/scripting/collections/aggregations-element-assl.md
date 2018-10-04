---
title: Aggregations 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Aggregations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Aggregations
helpviewer_keywords:
- Aggregations element
ms.assetid: 79b7de7a-53b2-4202-bc0f-de1daaf1b179
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2d64819bb59cbd86b2179abfbfd3afb5639577a0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177587"
---
# <a name="aggregations-element-assl"></a>Aggregations 元素 (ASSL)
  包含用于定义聚合的集合[AggregationDesign](../objects/aggregationdesign-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationDesign>  
   ...  
   <Aggregations>  
      <Aggregation>...</Aggregation>  
   </Aggregations>  
   ...  
</AggregationDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|无（集合）|  
|默认值|无（集合）|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationDesign](../objects/aggregationdesign-element-assl.md)|  
|子元素|[聚合](../objects/aggregation-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationCollection>。  
  
## <a name="see-also"></a>请参阅  
 [MeasureGroup 元素&#40;ASSL&#41;](../objects/group-element-assl.md)   
 [分区元素&#40;ASSL&#41;](../objects/partition-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
