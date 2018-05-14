---
title: AggregationUsage 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2086a274fb76238efd11e4f7c881b07f0b98159f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="aggregationusage-element-assl"></a>AggregationUsage 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  控件如何聚合设计器中[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]设计聚合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeAttribute>  
   ...  
   <AggregationUsage>...</AggregationUsage>  
   ...  
</CubeAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*默认*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*Full*|多维数据集的每个聚合都必须包含此属性。|  
|*InclusionThresholdSetting*|多维数据集的所有聚合都不应包括此属性。|  
|*不受限制*|未设置任何限制聚合设计器上。|  
|*默认*|聚合设计器应用默认规则基于属性的类型 (*完整*有关密钥，*不受限制的*其他人)。|  
  
 对应于的允许值为枚举**AggregationUsage**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AggregationUsage>。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
