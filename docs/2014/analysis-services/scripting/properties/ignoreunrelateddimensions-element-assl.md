---
title: IgnoreUnrelatedDimensions 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- IgnoreUnrelatedDimensions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- IgnoreUnrelatedDimensions
helpviewer_keywords:
- IgnoreUnrelatedDimensions element
ms.assetid: c7d7a1cd-a8e0-4ae7-9464-a1d2a55a86ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 400a1ef9f55d5696e2bbaeabbdd4a109c7a13587
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099337"
---
# <a name="ignoreunrelateddimensions-element-assl"></a>IgnoreUnrelatedDimensions 元素 (ASSL)
  确定当查询中包括与度量值组无关的维度的成员时，是否将无关维度强制为顶级。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroup>  
   ...  
   <IgnoreUnrelatedDimensions>...</IgnoreUnrelatedDimensions>  
   ...  
</MeasureGroup>  
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
|父元素|[度量值组](../objects/group-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 当 `IgnoreUnrelatedDimensions` 为 `true` 时，无关的维度会被强制为顶级；当其值为 `false` 时，维度不会被强制为顶级。 此属性是为多维表达式 (MDX) 类似[ValidMeasure](/sql/mdx/validmeasure-mdx)函数。  
  
 父级对应的元素`IgnoreUnrelatedDimensions`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.MeasureGroup>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
