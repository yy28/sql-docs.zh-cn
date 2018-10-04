---
title: MiningModelID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningModelID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelID
helpviewer_keywords:
- MiningModelID element
ms.assetid: fada8720-1590-44be-bafc-0ab3612b00e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 43cfcff8b238b2502ede1c89038d88be013f639e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067443"
---
# <a name="miningmodelid-element-assl"></a>MiningModelID 元素 (ASSL)
  将挖掘模型与数据挖掘维度关联。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Dimension>  
   ...  
   <MiningModelID>...</MiningModelID>  
   ...  
</Dimension>  
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
|父元素|[Dimension](../objects/dimension-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`MiningModelID`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>请参阅  
 [MiningModel 元素&#40;ASSL&#41;](../objects/miningmodel-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
