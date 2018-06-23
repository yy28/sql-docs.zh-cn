---
title: 类型元素 (MeasureGroupAttribute) (ASSL) |Microsoft 文档
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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0d06b5df3ba99e54ec62de5c6f274874289cbbc4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027755"
---
# <a name="type-element-measuregroupattribute-assl"></a>Type 元素 (MeasureGroupAttribute) (ASSL)
  包含的一种[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)元素。  
  
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
  
 对应于的允许值为枚举`Type`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MeasureGroupAttributeType>。  
  
 对应于的父元素`Type`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MeasureGroupAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [属性元素&#40;ASSL&#41;](../collections/attributes-element-assl.md)   
 [RegularMeasureGroupDimension 数据类型&#40;ASSL&#41;](../data-type/dimension-data-type-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  