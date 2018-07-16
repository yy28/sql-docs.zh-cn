---
title: Aggregations 元素 (ASSL) |Microsoft Docs
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
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c94129a76064bbbc98f300a855e77826ec57794
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189194"
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
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationCollection>。  
  
## <a name="see-also"></a>请参阅  
 [MeasureGroup 元素&#40;ASSL&#41;](../objects/group-element-assl.md)   
 [分区元素&#40;ASSL&#41;](../objects/partition-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
