---
title: 类型元素 （维度） (ASSL) |Microsoft 文档
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
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 582d5b2052f2681630c5f0cd86facacd5e7cfc91
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024659"
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
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 某些值`Type`，例如*帐户*，确定特定的行为。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*正则*|该维度是一个常规维度。|  
|*Time*|该维度是一个时间维度。 **注意：** 此值指示维度支持特定于时间维度的功能。|  
|*地理位置*|维度包含地域属性。|  
|*组织*|维度包含单位属性。|  
|*物料清单*|维度包含物料清单属性。|  
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
  
 对应于的允许值为枚举`Type`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DimensionType>。  
  
 对应于的父元素`Type`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  