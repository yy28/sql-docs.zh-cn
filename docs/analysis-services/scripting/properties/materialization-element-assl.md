---
title: 具体化元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c620e4fb43246dcd5d761503c0368665ff4a61a4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="materialization-element-assl"></a>Materialization 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*间接*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ReferenceMeasureGroupDimension](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*Regular*|引用维度具有常规关系，如常规维度中的关系。|  
|*间接*|引用维度具有间接关系，如多对多维度中的关系。|  
  
 对应于的父元素**具体化**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension>。  
  
## <a name="see-also"></a>另请参阅  
 [维度元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
