---
title: RefreshInterval 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RefreshInterval Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RefreshInterval
helpviewer_keywords:
- RefreshInterval element
ms.assetid: 2761d26a-5fb0-452c-9a89-12f8dc658c33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 76651edd1818204fed5c2ab9f8d8d787f4501d6a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48175837"
---
# <a name="refreshinterval-element-assl"></a>RefreshInterval 元素 (ASSL)
  指定与父元素关联的绑定数据的刷新时间间隔。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding, ProactiveCachingIncrementalProcessingBinding, ProactiveCachingQueryBinding -->  
   ...  
   <RefreshInterval>...</RefreshInterval>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|XML 持续时间|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
|默认值|[ProactiveCachingIncrementalProcessingBinding](../data-type/binding-data-type-assl.md)或[ProactiveCachingQueryBinding](../data-type/querybinding-data-type-assl.md) = PT 1 s|  
|默认值|所有其他 = PT1m|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)， [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)， [ProactiveCachingIncrementalProcessingBinding](../data-type/binding-data-type-assl.md)， [ProactiveCachingQueryBinding](../data-type/querybinding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中，与 `RefreshInterval` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.DimensionBinding>、<xref:Microsoft.AnalysisServices.MeasureGroupBinding>、<xref:Microsoft.AnalysisServices.ProactiveCachingIncrementalProcessingBinding> 和 <xref:Microsoft.AnalysisServices.ProactiveCachingQueryBinding>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
