---
title: Trend 元素 (ASSL) |Microsoft Docs
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
- Trend Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Trend
helpviewer_keywords:
- Trend element
ms.assetid: d1d92d10-a181-4402-aacb-c0b2adc96bba
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 63bf8353e2ba801fc743fd4d645316c1e8f51eda
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171178"
---
# <a name="trend-element-assl"></a>Trend 元素 (ASSL)
  包含返回的走向指示器的多维表达式 (MDX) 表达式[Kpi](../objects/kpi-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Kpi>  
   ...  
   <Trend>...</Trend>  
   ...  
</Kpi>  
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
|父元素|[Kpi](../objects/kpi-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Trend` 元素包含一个计算结果为 -1 和 1 之间的 MDX 表达式。  
  
 父级对应的元素`Trend`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Kpi>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
