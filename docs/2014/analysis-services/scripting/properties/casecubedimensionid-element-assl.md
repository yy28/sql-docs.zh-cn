---
title: CaseCubeDimensionID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CaseCubeDimensionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CaseCubeDimensionID
helpviewer_keywords:
- CaseCubeDimensionID element
ms.assetid: 96720e13-7f9b-4768-ad4b-4def40758707
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8d18fb24a3e2f30dbbc0f8b085bd89096baede81
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082647"
---
# <a name="casecubedimensionid-element-assl"></a>CaseCubeDimensionID 元素 (ASSL)
  包含将数据挖掘维度与度量值组关联的多维数据集维度的标识符 (ID)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataMiningMeasureGroupDimension>  
   ...  
   <CaseCubeDimensionID>...</CaseCubeDimensionID>  
   ...  
</DataMiningMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataMiningMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`CaseCubeDimensionID`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.DataMiningMeasureGroupDimension>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
