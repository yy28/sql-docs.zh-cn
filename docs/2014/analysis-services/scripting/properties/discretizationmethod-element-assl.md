---
title: DiscretizationMethod 元素 (ASSL) |Microsoft Docs
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
- DiscretizationMethod Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DiscretizationMethod
helpviewer_keywords:
- DiscretizationMethod element
ms.assetid: 4cfe015f-ad6c-47e1-8aff-c9c7677867b1
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6347db0e5d964b10112516b4c607a5185f247b65
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252999"
---
# <a name="discretizationmethod-element-assl"></a>DiscretizationMethod 元素 (ASSL)
  定义用于离散化的方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationMethod>...</DiscretizationMethod>  
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
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `DiscretizationMethod` 元素的值可确定如何离散化 `DimensionAttribute` 或 `ScalarMiningStructureColumn` 的值，或如何将其组织到特定的组集中。 有关离散化方法的详细信息，请参阅[离散化方法&#40;数据挖掘&#41;](../../data-mining/discretization-methods-data-mining.md)。  
  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*自动*|等效于用于挖掘结构列的 AUTOMATIC 离散化方法。|  
|*EqualAreas*|等效于用于挖掘结构列的 EQUAL_AREAS 离散化方法。|  
|*群集*|等效于用于挖掘结构列的 CLUSTERS 离散化方法。|  
|*Thresholds*|等效于用于挖掘结构列的 THRESHOLDS 离散化方法。|  
|*EqualRanges*|等效于用于挖掘结构列的 EQUAL_RANGES 离散化方法。|  
  
 对应的允许值的枚举`DiscretizationMethod`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.DiscretizationMethod>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
