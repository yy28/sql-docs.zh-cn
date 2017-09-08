---
title: "RefreshInterval 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- RefreshInterval Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RefreshInterval
helpviewer_keywords:
- RefreshInterval element
ms.assetid: 2761d26a-5fb0-452c-9a89-12f8dc658c33
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7d5d7b519d52d60c042ecb0830a9d36e897ad86c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|XML 持续时间|  
|默认值|祖先或父级时[ProactiveCachingIncrementalProcessingBinding](../../../analysis-services/scripting/data-type/proactivecachingincrementalprocessingbinding-data-type-assl.md)或[ProactiveCachingQueryBinding](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)，默认值是 PT 为 1。 在所有其他情况下，它为 PT1m。|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)， [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)， [ProactiveCachingIncrementalProcessingBinding](../../../analysis-services/scripting/data-type/proactivecachingincrementalprocessingbinding-data-type-assl.md)， [ProactiveCachingQueryBinding](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**RefreshInterval**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.DimensionBinding>， <xref:Microsoft.AnalysisServices.MeasureGroupBinding>， <xref:Microsoft.AnalysisServices.ProactiveCachingIncrementalProcessingBinding>，和<xref:Microsoft.AnalysisServices.ProactiveCachingQueryBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
