---
title: DiscretizationBucketCount 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 99329b8d3c635ecbd6d4ffcfd6139fd5056539b9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="discretizationbucketcount-element-assl"></a>DiscretizationBucketCount 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含以其进行离散化的存储桶数。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 值**DiscretizationBucketCount**元素确定多少组或"存储桶"时，会创建值**DimensionAttribute**或**ScalarMiningStructureColumn**离散化，或组织成一组特定的组。 如果未指定元素，或如果为该元素的值指定零[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]创建适当数量的组，具体取决于离散化方法。 有关离散化方法的详细信息，请参阅[离散化方法&#40;数据挖掘&#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md)。  
  
 对应的父级的元素**DiscretizationBucketCount**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.DimensionAttribute>和<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另请参阅  
 [DiscretizationMethod 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
