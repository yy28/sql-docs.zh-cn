---
title: Aggregation 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Aggregation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Aggregation
helpviewer_keywords:
- Aggregation element
ms.assetid: f37af388-b2b3-4234-a1d6-936ee9b7f2ae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0780a8c81cf80871eed925471fd0ea7e6103e9b6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167797"
---
# <a name="aggregation-element-assl"></a>Aggregation 元素 (ASSL)
  定义的单个聚合[分区](partition-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Aggregations>  
      <Aggregation>  
      <ID>...</ID>  
      <Name>...</Name>  
      <Dimensions>...</Dimensions>  
            <Annotations>...</Annotations>  
      <Description>...</Description>  
   </Aggregation>  
</Aggregations>  
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
|父元素|[聚合](../collections/aggregations-element-assl.md)|  
|子元素|[批注](../collections/annotations-element-assl.md)，[描述](../properties/description-element-assl.md)，[维度](../collections/dimensions-element-assl.md)， [ID](../properties/id-element-assl.md)，[名称](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Aggregation>。  
  
## <a name="see-also"></a>请参阅  
 [分区元素&#40;ASSL&#41;](partition-element-assl.md)   
 [AggregationDesign 元素&#40;ASSL&#41;](aggregationdesign-element-assl.md)   
 [MeasureGroup 元素&#40;ASSL&#41;](group-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
