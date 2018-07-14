---
title: CustomRollupProperties 元素 (XMLA) |Microsoft Docs
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
- CustomRollupProperties Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.customrollupproperties
- urn:schemas-microsoft-com:xml-analysis#CustomRollupProperties
- http://schemas.microsoft.com/analysisservices/2003/engine#CustomRollupProperties
helpviewer_keywords:
- CustomRollupProperties element
ms.assetid: 4abf0129-e529-4355-b8d5-6f4e6a88e796
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a564296dd022dece7ff20a7187c2c80bba9c6b7f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233697"
---
# <a name="customrollupproperties-element-xmla"></a>CustomRollupProperties 元素 (XMLA)
  包含表示由父特性成员的自定义汇总属性[特性](attribute-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Attribute>  
   ...  
   <CustomRollupProperties>...</CustomRollupProperties>  
   ...  
</Attribute>  
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
|父元素|[Attribute](attribute-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `CustomRollupProperties` 元素包含有一个多维表达式 (MDX)，该多维表达式可定义父级 `Attribute` 元素定义的属性成员的自定义汇总属性。  
  
 有关 MDX 表达式的详细信息，请参阅[表达式&#40;MDX&#41;](/sql/mdx/expressions-mdx)。  
  
## <a name="see-also"></a>请参阅  
 [插入元素&#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Update 元素&#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
