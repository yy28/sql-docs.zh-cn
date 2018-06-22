---
title: 可见元素 (ASSL) |Microsoft 文档
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
- Visible Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Visible
helpviewer_keywords:
- Visible element
ms.assetid: 3e9baf1b-351f-4ebf-b57d-13d561f72d6f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 90a6ddadf0bc6654fb0c30c02f22b78a88655daa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016206"
---
# <a name="visible-element-assl"></a>Visible 元素 (ASSL)
  确定父元素的可见性。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CalculationProperty> <!-- or one of the elements listed below in the Element Relationships table -->  
  
   <Visible >...</Visible >  
  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|True|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../objects/calculationproperty-element-assl.md)，[多维数据集](../objects/cube-element-assl.md)， [CubeDimension](../data-type/dimension-data-type-assl.md)， [CubeHierarchy](../data-type/hierarchy-data-type-assl.md)，[数据库](../objects/database-element-assl.md)，[度量值](../objects/measure-element-assl.md)， [MemberProperty](../objects/attributerelationship-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Visible` 元素可确定用户界面组件是否应显示父元素。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `Visible` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.CalculationProperty>、<xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.CubeDimension>、<xref:Microsoft.AnalysisServices.CubeHierarchy>、<xref:Microsoft.AnalysisServices.Database> 和 <xref:Microsoft.AnalysisServices.Measure>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  