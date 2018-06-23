---
title: HoldoutActualSize 元素 |Microsoft 文档
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
- HoldoutActualSize
helpviewer_keywords:
- HoldoutActualSize element
ms.assetid: 606a6674-cedb-4cee-82d0-26589f084dd9
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fe781b9e3381a97d9ad75440dac40e281881419f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028659"
---
# <a name="holdoutactualsize-element"></a>HoldoutActualSize 元素
  处理之后，包含的测试集的维持分区指示实际大小， [MiningStructure](../objects/miningstructure-element-assl.md)元素。 数据集中的其余事例用于定型。 该属性为只读。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutActualSize>...</ddl100_100:HoldoutActualSize>  
   ...  
</MiningStructure  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|只读的整数值。|  
|默认值|不适用|  
|基数|0-1：可选元素，只显示一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 值`HoldoutActualSize`取决于源数据，和的值[HoldoutMaxCases](holdoutmaxcases-element.md)， [HoldoutMaxPercent](holdoutmaxpercent-element.md)，和[HoldoutSeed](holdoutseed-element.md)。 因此，只有在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 处理完挖掘结构之后，`HoldoutActualSize` 的值才可用。  
  
 对应于的父元素`HoldoutActualSize`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持对挖掘结构使用维持分区。 因此，包含 `HoldoutMaxCases`、`HoldoutMaxPercent`、`HoldoutSeed` 或 `HoldoutActualSize` 维持参数之一的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 语句不能在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中使用。 如果在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中将这些维持参数之一用于 ASSL 语句，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回错误。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)   
 [HoldoutMaxCases 元素](holdoutmaxcases-element.md)   
 [HoldoutMaxPercent 元素](holdoutmaxpercent-element.md)   
 [HoldoutSeed 元素](holdoutseed-element.md)  
  
  