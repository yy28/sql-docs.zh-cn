---
title: Action 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Action Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Action
helpviewer_keywords:
- Action element
ms.assetid: aaee06a2-91c6-4007-b787-79cb08d63c77
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 48a07020a2c4b8bb2fbc79c5c3d67697a30760d7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166437"
---
# <a name="action-element-assl"></a>Action 元素 (ASSL)
  包含有关中提供的操作的信息[多维数据集](cube-element-assl.md)元素或[角度来看](perspective-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Actions>  
   <Action xsi:type="DrillThroughAction">...</Action> <!-- ancestor: Cube -->  
   <Action xsi:type="ReportAction">...</Action> <!-- ancestor: Cube -->  
   <Action xsi:type="StandardAction">...</Action> <!-- ancestor: Cube -->  
   <!-- or -->  
   <Action xsi:type="PerspectiveAction">...</Action> <!-- ancestor: Perspective -->  
</Actions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
|祖先或父级|数据类型|  
|------------------------|---------------|  
|[多维数据集](../data-type/action-data-type-assl.md)， [ReportAction](../data-type/reportaction-data-type-assl.md)， [StandardAction](../data-type/standardaction-data-type-assl.md)|  
|[透视](../data-type/perspectiveaction-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../collections/actions-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>请参阅  
 [多维数据集元素&#40;ASSL&#41;](cube-element-assl.md)   
 [Perspective 元素&#40;ASSL&#41;](perspective-element-assl.md)   
 [PerspectiveAction 数据类型&#40;ASSL&#41;](../data-type/perspectiveaction-data-type-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
