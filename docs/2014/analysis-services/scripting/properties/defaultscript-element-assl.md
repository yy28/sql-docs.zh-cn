---
title: DefaultScript 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DefaultScript Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultScript
helpviewer_keywords:
- DefaultScript element
ms.assetid: 60716e63-2d64-4774-9ac9-253efe612fa5
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b0a26b8b703636aebb6d3701c5c7c99d24a25ade
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138735"
---
# <a name="defaultscript-element-assl"></a>DefaultScript 元素 (ASSL)
  标识默认[MdxScript](../objects/mdxscript-element-assl.md)中的元素[mdxscript 被](../collections/mdxscripts-element-assl.md)集合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MdxScript>  
   ...  
   <DefaultScript>...</DefaultScript>  
   ...  
</MdxScript>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|`True`|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MdxScript](../objects/mdxscript-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 将一个脚本的 `DefaultScript` 值设置为 `True` 将使 `DefaultScript` 集合中所有其他 `False` 元素的 `MdxScript` 值设置为 `MdxScripts`。  
  
 对应于的父元素`DefaultScript`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MdxScript>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  