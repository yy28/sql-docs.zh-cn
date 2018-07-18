---
title: DiscretizationMethod 元素 (ASSL) |Microsoft Docs
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
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38002199"
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 值**DiscretizationMethod**元素可确定如何为值**DimensionAttribute**或**ScalarMiningStructureColumn**离散化，或组织到一组特定的组。 有关离散化方法的详细信息，请参阅[离散化方法&#40;数据挖掘&#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md)。  
  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*自动*|等效于用于挖掘结构列的 AUTOMATIC 离散化方法。|  
|*EqualAreas*|等效于用于挖掘结构列的 EQUAL_AREAS 离散化方法。|  
|*群集*|等效于用于挖掘结构列的 CLUSTERS 离散化方法。|  
|*Thresholds*|等效于用于挖掘结构列的 THRESHOLDS 离散化方法。|  
|*EqualRanges*|等效于用于挖掘结构列的 EQUAL_RANGES 离散化方法。|  
  
 对应的允许值的枚举**DiscretizationMethod**在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.DiscretizationMethod>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
