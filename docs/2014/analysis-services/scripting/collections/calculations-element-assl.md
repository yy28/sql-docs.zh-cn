---
title: 计算元素 (ASSL) |Microsoft 文档
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
- Calculations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Calculations
helpviewer_keywords:
- Calculations element
ms.assetid: 03e5e91c-1f66-4dc7-8aad-4d9876928df0
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 12d1ad22a305c6adb198348a1cd7fe6b858e72cf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016947"
---
# <a name="calculations-element-assl"></a>Calculations 元素 (ASSL)
  包含的集合[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)与关联的元素[透视](../objects/perspective-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Perspective>  
      ...  
   <Calculations>  
      <Calculation xsi:type="PerspectiveCalculation">...</Calculation>  
   </Calculations>  
   ...  
</Perspective>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[透视](../objects/perspective-element-assl.md)|  
|子元素|[计算](../objects/calculation-element-assl.md)类型的[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.PerspectiveCalculationCollection>。  
  
## <a name="see-also"></a>请参阅  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  