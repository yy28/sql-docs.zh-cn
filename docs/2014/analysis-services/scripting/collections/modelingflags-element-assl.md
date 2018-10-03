---
title: ModelingFlags 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ModelingFlags Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ModelingFlags
helpviewer_keywords:
- ModelingFlags element
ms.assetid: 83968c1e-aae8-4657-aa53-d971de0dc834
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 369af68b69c25d70ea80096947a0ecda4488418a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063254"
---
# <a name="modelingflags-element-assl"></a>ModelingFlags 元素 (ASSL)
  包含的集合[ModelingFlag](../objects/modelingflag-element-assl.md)元素中的列[MiningStructure](../objects/miningstructure-element-assl.md)或[MiningModel](../objects/miningmodel-element-assl.md)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModelColumn> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <ModelingFlags>  
      <ModelingFlag xsi:type="MiningModelingFlag">...</ModelingFlag>  
   </ModelingFlags>  
   ...  
</MiningModelColumn>  
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
|父元素|[MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)， [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|[ModelingFlag](../objects/modelingflag-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MiningModelingFlags>。  
  
## <a name="see-also"></a>请参阅  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
