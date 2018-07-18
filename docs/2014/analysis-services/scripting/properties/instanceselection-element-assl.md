---
title: InstanceSelection 元素 (ASSL) |Microsoft Docs
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
- InstanceSelection Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- InstanceSelection element
ms.assetid: 908a2da9-274c-40d2-87dc-4641cb8d77e6
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e9babb9e5066d00b8a396d52dfb2dbdfc2f0b4cf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279763"
---
# <a name="instanceselection-element-assl"></a>InstanceSelection 元素 (ASSL)
  提供了应显示提示客户端应用程序建议如何的项的列表，根据预期的列表中的项目数。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <InstanceSelection>...</InstanceSelection>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下列字符串之一：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*无*|不显示选择列表。 允许用户直接输入值。|  
|*下拉列表中*|项数很少，足以在下拉列表中显示。|  
|*列表*|项数太多，不能在下拉列表中显示，但不需要进行筛选。|  
|*FilteredList*|项数太多，需要用户进行筛选才能显示。|  
|*MandatoryFilter*|项数太多，必须一直使用筛选才能显示。|  
  
 与允许的值相对应的枚举`InstanceSelection`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.InstanceSelection>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
