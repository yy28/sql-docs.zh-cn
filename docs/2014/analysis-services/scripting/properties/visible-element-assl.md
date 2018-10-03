---
title: Visible 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a28fa446eb1753ce85458a19b849729f57c67a7a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166657"
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
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `Visible` 元素可确定用户界面组件是否应显示父元素。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `Visible` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.CalculationProperty>、<xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.CubeDimension>、<xref:Microsoft.AnalysisServices.CubeHierarchy>、<xref:Microsoft.AnalysisServices.Database> 和 <xref:Microsoft.AnalysisServices.Measure>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
