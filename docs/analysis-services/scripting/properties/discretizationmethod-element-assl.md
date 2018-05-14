---
title: DiscretizationMethod 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 81064689788574061f103b973a5435beb3e83893
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="discretizationmethod-element-assl"></a>DiscretizationMethod 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 值**DiscretizationMethod**元素确定如何值**DimensionAttribute**或**ScalarMiningStructureColumn** discretized、 或组织到一组特定的组。 有关离散化方法的详细信息，请参阅[离散化方法&#40;数据挖掘&#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md)。  
  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|*自动*|等效于用于挖掘结构列的 AUTOMATIC 离散化方法。|  
|*EqualAreas*|等效于用于挖掘结构列的 EQUAL_AREAS 离散化方法。|  
|*Clusters*|等效于用于挖掘结构列的 CLUSTERS 离散化方法。|  
|*Thresholds*|等效于用于挖掘结构列的 THRESHOLDS 离散化方法。|  
|*EqualRanges*|等效于用于挖掘结构列的 EQUAL_RANGES 离散化方法。|  
  
 对应的允许值为枚举**DiscretizationMethod**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DiscretizationMethod>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
