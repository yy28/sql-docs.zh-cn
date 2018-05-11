---
title: DataAggregation 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c315e40b15d7bf83cdc317a9498998387fd4d3ee
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="dataaggregation-element-assl"></a>DataAggregation 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  确定实例是否可以聚合持久化的数据或缓存的数据的[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroup>  
   ...  
   <DataAggregation>...</DataAggregation>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*DataAndCacheAggregatable*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[度量值组](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*InclusionThresholdSetting*|不为此度量值组执行聚合。|  
|*DataAggregatable*|为此度量值组聚合持久化数据。|  
|*CacheAggregatable*|为此度量值组聚合缓存数据。|  
|*DataAndCacheAggregatable*|为此度量值组聚合持久化数据和缓存数据。|  
  
 对应于的父元素**DataAggregation**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MeasureGroup>。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [维度元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
