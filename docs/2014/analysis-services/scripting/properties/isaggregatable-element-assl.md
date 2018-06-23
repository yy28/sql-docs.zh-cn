---
title: IsAggregatable 元素 (ASSL) |Microsoft 文档
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
- IsAggregatable Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- IsAggregatable
helpviewer_keywords:
- IsAggregatable element
ms.assetid: ed7dbe89-259c-4c5c-9660-b965c3af1573
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9d167c7c2cf8ce6e1f8092a6378d543ee0ab0d1f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125454"
---
# <a name="isaggregatable-element-assl"></a>IsAggregatable 元素 (ASSL)
  指定是否的值[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)可以聚合元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
      ...  
   <IsAggregatable>...</IsAggregatable>  
  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|True|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对应于的父元素`IsAggregatable`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  