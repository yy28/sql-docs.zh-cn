---
title: RefreshPolicy 元素 (ASSL) |Microsoft Docs
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
- RefreshPolicy Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RefreshPolicy
helpviewer_keywords:
- RefreshPolicy element
ms.assetid: f4c36280-1a39-4f1c-a3ab-fbeb81742d6d
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cf0aa9478a44e7479b20357ae56317b90801f77f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277613"
---
# <a name="refreshpolicy-element-assl"></a>RefreshPolicy 元素 (ASSL)
  何种频率确定维度或度量值组的动态部分 (所指定的[持久性](persistence-element-assl.md)元素) 的更改检查。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <RefreshPolicy>...</RefreshPolicy>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
|祖先或父级|默认值|  
|------------------------|-------------------|  
|[DimensionBinding](../data-type/binding-data-type-assl.md)|*依据查询*|  
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|InclusionThresholdSetting|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionBinding](../data-type/binding-data-type-assl.md)， [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*依据查询*|每个查询都进行检查，以查看数据源是否已更改。|  
|*ByInterval*|检查源数据是仅更改指定的时间间隔[RefreshInterval](refreshinterval-element-assl.md)。|  
  
 与允许的值相对应的枚举`RefreshPolicy`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.RefreshPolicy>。  
  
## <a name="see-also"></a>请参阅  
 [Persistence 元素&#40;ASSL&#41;](persistence-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
