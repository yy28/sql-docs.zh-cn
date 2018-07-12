---
title: DimensionID 元素 (ASSL) |Microsoft Docs
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
- DimensionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DimensionID
helpviewer_keywords:
- DimensionID element
ms.assetid: 00262781-4216-4a19-8bdc-d46647f42165
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5c211ed3b218a89bf02e29793573fe0915191641
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259483"
---
# <a name="dimensionid-element-assl"></a>DimensionID 元素 (ASSL)
  包含维度的标识符 (ID)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeDimension> <!-- or DimensionBinding, DimensionAttributeBinding -- >  
   ...  
   <DimensionID>...</DimensionID>  
      ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeDimension](../data-type/dimension-data-type-assl.md)， [DimensionBinding](../data-type/binding-data-type-assl.md)， [DimensionAttributeBinding](../data-type/dimensionattributebinding-data-type-out-of-line-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 父级对应的元素`DimensionID`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.CubeDimension>和<xref:Microsoft.AnalysisServices.DimensionBinding>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
