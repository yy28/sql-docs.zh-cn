---
title: MeasureGroupID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroupID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupID
helpviewer_keywords:
- MeasureGroupID element
ms.assetid: 3b075f86-dbbc-4285-8d2d-61fa722181c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b4eb43414e0fd7da783f4a1ac588c4851e3c9bd9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083627"
---
# <a name="measuregroupid-element-assl"></a>MeasureGroupID 元素 (ASSL)
  将相关联[MeasureGroup](../objects/group-element-assl.md)与父元素、 绑定或外部的绑定。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ManyToManyMeasureGroupDimension> <!-- or MeasureGroupAttributeBinding, MeasureGroupBinding, PerspectiveMeasureGroup -->  
   ...  
   <MeasureGroupID>...</MeasureGroupID>  
   ...  
</ManyToManyMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数||  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md)， [MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)， [MeasureGroupBinding](../data-type/binding-data-type-assl.md)， [PerspectiveMeasureGroup](../data-type/perspectivemeasuregroup-data-type-assl.md)|  
  
|子元素的祖先或父级|基数|  
|------------------------------------------|-----------------|  
|[ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|0-1：可出现一次且仅出现一次的可选元素。|  
|[MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)， [MeasureGroupBinding](../data-type/binding-data-type-assl.md)和[PerspectiveMeasureGroup](../data-type/perspectivemeasuregroup-data-type-assl.md)|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`MeasureGroupID`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.ManyToManyMeasureGroupDimension>， <xref:Microsoft.AnalysisServices.MeasureGroupBinding>，和<xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
