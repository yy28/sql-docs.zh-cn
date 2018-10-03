---
title: AggregationDesignID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationDesignID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationDesignID
helpviewer_keywords:
- AggregationDesignID element
ms.assetid: e7f1f7ae-3169-4c0c-aadb-f7465155d652
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61ca8f81002e28ca60a301ca49c307d9eeb6ef45
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185677"
---
# <a name="aggregationdesignid-element-assl"></a>AggregationDesignID 元素 (ASSL)
  标识[AggregationDesign](../objects/aggregationdesign-element-assl.md)元素与关联[分区](../objects/partition-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Partition>  
      ...  
   <AggregationDesignID>...</AggregationDesignID>  
   ...  
</Partition>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[分区](../objects/partition-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`AggregationDesignID`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Partition>。 另请参阅<xref:Microsoft.AnalysisServices.AggregationDesign>。  
  
## <a name="see-also"></a>请参阅  
 [AggregationDesign 元素&#40;ASSL&#41;](../objects/aggregationdesign-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
