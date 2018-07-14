---
title: Type 元素 (MeasureGroupAttribute) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element (MeasureGroupAttribute)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 93740504-297a-4a06-ab3e-b598e466eebb
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 49155b00ca70c613ffec01e898e7c6f071e24c84
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254849"
---
# <a name="type-element-measuregroupattribute-assl"></a>Type 元素 (MeasureGroupAttribute) (ASSL)
  包含的类型[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroupAttribute>  
   ...  
   <Type>...</Type>  
   ...  
</MeasureGroupAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*正则*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*正则*|表示常规特性。|  
|*粒度*|表示粒度属性。|  
  
 与允许的值相对应的枚举`Type`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.MeasureGroupAttributeType>。  
  
 父级对应的元素`Type`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.MeasureGroupAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [Attributes 元素&#40;ASSL&#41;](../collections/attributes-element-assl.md)   
 [RegularMeasureGroupDimension 数据类型&#40;ASSL&#41;](../data-type/dimension-data-type-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
