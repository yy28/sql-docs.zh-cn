---
title: 聚合元素 (ASSL) |Microsoft 文档
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
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 59f33b45653f614702b1472e57fe4464cf172b73
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123488"
---
# <a name="aggregation-element-assl"></a>Aggregation 元素 (ASSL)
  定义为单个聚合[分区](partition-element-assl.md)元素。  
  
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
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[聚合](../collections/aggregations-element-assl.md)|  
|子元素|[批注](../collections/annotations-element-assl.md)，[说明](../properties/description-element-assl.md)，[维度](../collections/dimensions-element-assl.md)， [ID](../properties/id-element-assl.md)，[名称](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Aggregation>。  
  
## <a name="see-also"></a>请参阅  
 [分区元素&#40;ASSL&#41;](partition-element-assl.md)   
 [AggregationDesign 元素&#40;ASSL&#41;](aggregationdesign-element-assl.md)   
 [MeasureGroup 元素&#40;ASSL&#41;](group-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  