---
title: Materialization 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Materialization Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Materialization element
ms.assetid: a87a95ae-d89c-4005-b22c-47c8991673b7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 149c2bdaa147e129b3d25637c46c10983004c1dc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106447"
---
# <a name="materialization-element-assl"></a>Materialization 元素 (ASSL)
  指示度量值组和引用维度之间的关系类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ReferenceMeasureGroupDimension >  
   ...  
   <Materialization>...</Materialization>  
   ...  
</ReferenceMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*间接*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ReferenceMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*正则*|引用维度具有常规关系，如常规维度中的关系。|  
|*间接*|引用维度具有间接关系，如多对多维度中的关系。|  
  
 父级对应的元素`Materialization`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension>。  
  
## <a name="see-also"></a>请参阅  
 [维度元素&#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
