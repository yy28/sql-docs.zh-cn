---
title: AggregationInstances 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationInstances Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- AggregationInstances element
ms.assetid: e8321aa8-361b-4d8a-bd89-a596eeb814b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e0ed44484d1c8a27eae1495a188843040e28ba4b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050697"
---
# <a name="aggregationinstances-element-assl"></a>AggregationInstances 元素 (ASSL)
  包含在中定义的聚合实例的集合[分区](../objects/partition-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Partition>  
   ...  
   <AggregationInstances>  
      <AggregationInstance>...</AggregationInstance>  
   </AggregationInstances>  
   ...  
</Partition>  
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
|父元素|[分区](../objects/partition-element-assl.md)|  
|子元素|[AggregationInstance](../objects/aggregationinstance-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationInstanceCollection>。  
  
## <a name="see-also"></a>请参阅  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
