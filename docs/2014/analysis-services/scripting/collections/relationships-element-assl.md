---
title: Relationships 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: e78882c9-b14e-4044-848e-ea7fddd3b75d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b0a83a2e7722fab119df3a0918ea0ecbe7c24131
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134541"
---
# <a name="relationships-element-assl"></a>Relationships 元素 (ASSL)
  包含关联维度的关系的集合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeDimension> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Attributes>  
      <Attribute>...</Attribute>  
  </Attributes>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeDimension](../data-type/dimension-data-type-assl.md)，[维度](../objects/dimension-element-assl.md)， [PerspectiveDimension](../data-type/perspectivedimension-data-type-assl.md)， [RegularMeasureGroupDimension](../data-type/measuregroupdimension-data-type-assl.md)|  
|子元素|[关系](../data-type/relationship-data-type-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中对应的元素为<xref:Microsoft.AnalysisServices.RelationshipCollection>。  
  
## <a name="see-also"></a>请参阅  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
