---
title: AggregationID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- AggregationID element
ms.assetid: 6056da1d-b6b4-4074-84db-45be719df49a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 47d79781ea7f85efa51f48b149a442e7c87ec1f2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087667"
---
# <a name="aggregationid-element-assl"></a>AggregationID 元素 (ASSL)
  标识从的聚合定义[AggregationDesign](../objects/aggregationdesign-element-assl.md)元素用来创建聚合实例。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationInstance>  
   ...  
   <AggregationID>...</AggregationID>  
   ...  
</AggregationInstance>  
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
|父元素|[AggregationInstance](../objects/aggregationinstance-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 如果缺少此元素或将此元素设置为空白字符串，则 `AggregationInstance` 表示一个用户定义的聚合。  
  
 父级对应的元素`AggregationID`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.AggregationInstance>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
