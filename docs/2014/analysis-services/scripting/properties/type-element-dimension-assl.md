---
title: Type 元素 (Dimension) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Type Element (Dimension)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 6a2798b1-26c7-49d8-b556-e681c69d9574
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab2d68ab78b31373e08185c3ee816241fe82bbd1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117617"
---
# <a name="type-element-dimension-assl"></a>Type 元素 (Dimension) (ASSL)
  提供有关维度内容的信息。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Dimension>  
      ...  
   <Type>...</Type>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*正则*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Dimension](../objects/dimension-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 某些值`Type`，例如*帐户*，确定特定行为。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*正则*|该维度是一个常规维度。|  
|*Time*|该维度是一个时间维度。 **注意：** 此值指示维度支持特定于时间维度的功能。|  
|*地理位置*|维度包含地域属性。|  
|*组织*|维度包含单位属性。|  
|*BillOfMaterials*|维度包含物料清单属性。|  
|*帐户*|维度包含帐户相关属性。 **注意：** 此值指示维度支持特定于帐户维度的功能。|  
|*客户*|维度包含客户相关属性。|  
|*产品*|维度包含产品相关属性。|  
|*方案*|维度包含方案相关属性。|  
|*定量*|维度包含定量属性。|  
|*实用工具*|维度包含效用属性。|  
|*货币*|维度包含货币属性。|  
|*费率*|维度包含汇率属性。|  
|*Channel*|维度包含渠道属性。|  
|*升级*|维度包含促销相关属性。|  
  
 与允许的值相对应的枚举`Type`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.DimensionType>。  
  
 父级对应的元素`Type`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
