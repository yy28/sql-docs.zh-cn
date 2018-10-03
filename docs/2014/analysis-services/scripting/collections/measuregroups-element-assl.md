---
title: MeasureGroups 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroups Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroups
helpviewer_keywords:
- MeasureGroups element
ms.assetid: 80e970e9-6ea6-47a9-9e5c-d0f9b01c09c0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee40e848ade9bd151836395be8f34029adef9e85
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153737"
---
# <a name="measuregroups-element-assl"></a>MeasureGroups 元素 (ASSL)
  包含的集合[MeasureGroup](../objects/group-element-assl.md)与父元素关联的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube> <!-- or CubeBinding, Perspective -->  
   ...  
   <MeasureGroups>  
      <MeasureGroup>...</MeasureGroup> <!-- parent: Cube -->  
      <MeasureGroup xsi:type="MeasureGroupBinding">...</MeasureGroup> <!-- parent: CubeBinding -->  
      <MeasureGroup xsi:type="PerspectiveMeasureGroup">...</MeasureGroup> <!-- parent: Perspective -->  
   </MeasureGroups>  
   ...  
</Cube>  
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
|父元素|[多维数据集](../objects/cube-element-assl.md)， [CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md)，[透视](../objects/perspective-element-assl.md)|  
  
|祖先或父级|子元素|  
|------------------------|-------------------|  
|[Cube](../objects/cube-element-assl.md)|[度量值组](../objects/group-element-assl.md)|  
|[CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md)|[MeasureGroup](../objects/group-element-assl.md)类型的[MeasureGroupBinding](../data-type/binding-data-type-assl.md)|  
|[透视](../objects/perspective-element-assl.md)|[MeasureGroup](../objects/group-element-assl.md)类型的[PerspectiveMeasureGroup](../data-type/perspectivemeasuregroup-data-type-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中，对应的元素为 <xref:Microsoft.AnalysisServices.MeasureGroupCollection> 或 <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroupCollection>。  
  
## <a name="see-also"></a>请参阅  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
