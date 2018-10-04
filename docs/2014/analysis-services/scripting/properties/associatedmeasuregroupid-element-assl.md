---
title: AssociatedMeasureGroupID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AssociatedMeasureGroupID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AssociatedMeasureGroupID
helpviewer_keywords:
- AssociatedMeasureGroupID element
ms.assetid: a18ff25b-00a2-4ddf-abcc-ef4d52c8a462
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 753f79f6f0536db7d5ae4c7af77805294c45af21
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054607"
---
# <a name="associatedmeasuregroupid-element-assl"></a>AssociatedMeasureGroupID 元素 (ASSL)
  包含的 ID [MeasureGroup](../objects/group-element-assl.md)元素与关联[CalculationProperty](../objects/calculationproperty-element-assl.md)元素或[Kpi](../objects/kpi-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CalculationProperty> <!-- or Kpi -->  
   ...  
   <AssociatedMeasureGroupID>...</AssociatedMeasureGroupID>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../objects/calculationproperty-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 当应用于`CalculationProperty`元素，`AssociatedMeasureGroupID`属性将应用于元素具有[CalculationType](calculationtype-element-assl.md)的*成员*。  
  
 父级对应的元素`AssociatedMeasureGroupID`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.CalculationProperty>和<xref:Microsoft.AnalysisServices.Kpi>。  
  
## <a name="see-also"></a>请参阅  
 [CalculationProperties 元素&#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 元素&#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [MdxScripts 元素&#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
