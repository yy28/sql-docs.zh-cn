---
title: DataAggregation 元素 (ASSL) |Microsoft 文档
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
- DataAggregation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataAggregation element
ms.assetid: baf6d2c9-54f6-4a6d-95f7-e1e758be458d
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 795555e24dbdc30a02b0fd3b286e4122323c00f4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015974"
---
# <a name="dataaggregation-element-assl"></a>DataAggregation 元素 (ASSL)
  确定实例是否可以聚合持久化的数据或缓存的数据的[MeasureGroup](../objects/group-element-assl.md)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroup>  
   ...  
   <DataAggregation>...</DataAggregation>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*DataAndCacheAggregatable*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[度量值组](../objects/group-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*无*|不为此度量值组执行聚合。|  
|*DataAggregatable*|为此度量值组聚合持久化数据。|  
|*CacheAggregatable*|为此度量值组聚合缓存数据。|  
|*DataAndCacheAggregatable*|为此度量值组聚合持久化数据和缓存数据。|  
  
 对应于的父元素`DataAggregation`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MeasureGroup>。  
  
## <a name="see-also"></a>请参阅  
 [多维数据集元素&#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [维度元素&#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  