---
title: RefreshPolicy 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6322c725a0c4b339425b9cc9e10aa6596c9fc34c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144427"
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
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|None|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionBinding](../data-type/binding-data-type-assl.md)， [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*依据查询*|每个查询都进行检查，以查看数据源是否已更改。|  
|*ByInterval*|检查源数据是仅更改指定的时间间隔[RefreshInterval](refreshinterval-element-assl.md)。|  
  
 与允许的值相对应的枚举`RefreshPolicy`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.RefreshPolicy>。  
  
## <a name="see-also"></a>请参阅  
 [Persistence 元素&#40;ASSL&#41;](persistence-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
