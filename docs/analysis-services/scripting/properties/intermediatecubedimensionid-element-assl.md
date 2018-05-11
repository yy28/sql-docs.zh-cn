---
title: IntermediateCubeDimensionID 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2f0396d3863c981e673e946ce03555b623c12129
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="intermediatecubedimensionid-element-assl"></a>IntermediateCubeDimensionID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含将引用维度与度量值组关联的维度的标识符 (ID)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ReferenceMeasureGroupDimension>  
   ...  
   <IntermediateCubeDimensionID>...</IntermediateCubeDimensionID>  
   ...  
</ReferenceMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ReferenceMeasureGroupDimension](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**IntermediateCubeDimensionID**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
