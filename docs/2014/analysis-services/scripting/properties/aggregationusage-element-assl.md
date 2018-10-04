---
title: AggregationUsage 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationUsage Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationUsage
helpviewer_keywords:
- AggregationUsage element
ms.assetid: af0c2e7f-b659-4fbf-9b1a-66128db669a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f2673a9747aee6192ac41d6c6e2c446045c4965f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174237"
---
# <a name="aggregationusage-element-assl"></a>AggregationUsage 元素 (ASSL)
  控件如何聚合设计器中[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]设计聚合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeAttribute>  
   ...  
   <AggregationUsage>...</AggregationUsage>  
   ...  
</CubeAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*默认*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeAttribute](../data-type/cubeattribute-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*Full*|多维数据集的每个聚合都必须包含此属性。|  
|*无*|多维数据集的所有聚合都不应包括此属性。|  
|*不受限制*|聚合设计器不作任何限制。|  
|*默认*|聚合设计器应用默认规则基于属性的类型 (*完整*键，*无限制*为其他人)。|  
  
 与允许的值相对应的枚举`AggregationUsage`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.AggregationUsage>。  
  
## <a name="see-also"></a>请参阅  
 [多维数据集元素&#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
