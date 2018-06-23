---
title: 筛选元素 （跟踪） (ASSL) |Microsoft 文档
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
- Filter Element (Trace)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- filter
helpviewer_keywords:
- Filter element
ms.assetid: 411a598e-3bb1-487b-9f37-cce4b57a67b4
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8997c652883a70572fa83351be51b3381a6fdb7f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123489"
---
# <a name="filter-element-trace-assl"></a>Filter 元素 (Trace) (ASSL)
  包含 XML 文档片段描述[跟踪](../objects/trace-element-assl.md)筛选器。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Trace>  
   ...  
   <Filter>...</Filter>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Trace](../objects/trace-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对应于的父元素`Filter`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)   
 [跟踪元素&#40;ASSL&#41;](../collections/traces-element-assl.md)  
  
  