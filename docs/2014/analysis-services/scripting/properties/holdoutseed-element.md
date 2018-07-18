---
title: HoldoutSeed 元素 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
f1_keywords:
- HoldoutSeed
helpviewer_keywords:
- HoldoutSeed element
ms.assetid: 6b608bb3-c075-4744-9722-f5fb9fa1cc7e
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b5ba2d0d5d3cb355a4d0d6a372b41207ddce1d6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185224"
---
# <a name="holdoutseed-element"></a>HoldoutSeed 元素
  指定的测试集所在的可重复的维持分区的种子[MiningStructure](../objects/miningstructure-element-assl.md)元素。 此种子可确保模型内容在处理过程中保持不变。 如果未指定或设置为 0，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]上的挖掘结构名称使用哈希算法创建种子。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutSeed>...</ddl100_100:HoldoutSeed>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Long|  
|默认值|0|  
|基数|0-1：可出现一次并仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 首次创建挖掘结构时，ID 和名称是相同的。 但是，您可以更改挖掘结构的名称。 因此，若要确保分区可重复使用，则不应依赖基于名称创建的种子，而应对种子进行显式设置。  
  
 此外，当您创建挖掘结构的副本通过使用`EXPORT`语句，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]将保留新挖掘结构的名称，但会自动生成新的 id。 因此，两个挖掘结构可以共享相同的名称但具有不同的 ID。 任何两个名称相同的挖掘结构都将具有相同的种子。 但是，由于数据的分区还依赖于源数据，因此每个结构中分区的实际内容可能不同。  
  
 新属性`HoldoutMaxCases`， `HoldoutMaxPercent`， `HoldoutSeed`，或`HoldoutActualSize`仅适用于[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]及更高版本。 因此，您必须在语法描述中所示前缀这些属性与新的命名空间或[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]将返回错误。  
  
 **请注意**中[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]不支持对挖掘结构使用维持分区。 因此，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含维持参数的脚本语言 (ASSL) 语句`HoldoutMaxCases`， `HoldoutMaxPercent`， `HoldoutSeed`，或`HoldoutActualSize`不能用于[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 如果在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中将这些维持参数之一用于 ASSL 语句，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回错误。  
  
 父级对应的元素`HoldoutSeed`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)   
 [HoldoutActualSize 元素](holdoutactualsize-element.md)   
 [HoldoutMaxPercent 元素](holdoutmaxpercent-element.md)   
 [HoldoutMaxCases 元素](holdoutmaxcases-element.md)  
  
  
