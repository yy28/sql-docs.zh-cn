---
title: MeasureID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureID
helpviewer_keywords:
- MeasureID element
ms.assetid: 8457aebc-8fdd-4683-8640-baaf9d89b2a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 87f79713090454e2426212eeecf56630eac7fe2c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197539"
---
# <a name="measureid-element-assl"></a>MeasureID 元素 (ASSL)
  将相关联[度量值](../objects/measure-element-assl.md)元素与父元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureBinding> <!-- or AggregationInstanceMeasure, PerspectiveMeasure -->  
   ...  
   <MeasureID>...</MeasureID>  
   ...  
</MeasureBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationInstanceMeasure](../data-type/aggregationinstancemeasure-data-type-assl.md)， [MeasureBinding](../data-type/binding-data-type-assl.md)， [PerspectiveMeasure](../data-type/perspectivemeasure-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`MeasureID`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.AggregationInstanceMeasure>， <xref:Microsoft.AnalysisServices.MeasureBinding>，和<xref:Microsoft.AnalysisServices.PerspectiveMeasure>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
