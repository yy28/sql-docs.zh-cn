---
title: AggregationType 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- AggregationType element
ms.assetid: c1393bc6-d715-4397-8bc5-82abdb275330
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dad62254c9da3809ae33dcfb035de34fa52a89fc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059617"
---
# <a name="aggregationtype-element-assl"></a>AggregationType 元素 (ASSL)
  定义存储的聚合类型[分区](../objects/partition-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationInstance>  
   ...  
   <AggregationType>...</AggregationType>  
   ...  
</AggregationInstance>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|None|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationInstance](../objects/aggregationinstance-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*IndexedView*|聚合存储在索引视图中。|  
|*表*|聚合存储在表中。|  
|*UserDefined*|聚合是用户定义的。|  
  
 与允许的值相对应的枚举`AggregationType`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.AggregationInstance>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
