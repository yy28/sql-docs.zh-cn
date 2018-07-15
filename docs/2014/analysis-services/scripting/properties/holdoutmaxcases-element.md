---
title: HoldoutMaxCases 元素 |Microsoft Docs
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
- HoldoutMaxCases
helpviewer_keywords:
- HoldoutMaxCases element
ms.assetid: 58d94d10-e11e-4368-b3b8-dff23e1947cd
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6eb53625e7f1fd7f595871bf505481cad4145866
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37314737"
---
# <a name="holdoutmaxcases-element"></a>HoldoutMaxCases 元素
  指定要使用的测试集所在维持分区的数据源中的情况下的最大数目[MiningStructure](../objects/miningstructure-element-assl.md)元素。 数据集中的其余事例用于定型。 值为 0 指示对可作为测试集来维持的事例数没有限制。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxCases>...</ddl100_100:HoldoutMaxCases>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|大于 0 的整数。|  
|默认值|0|  
|基数|0-1：可出现一次并仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 如果 `HoldoutMaxPercent` 和 `HoldoutMaxCases` 的值都指定，则算法会将测试集限制为这两个值中的较小值。  
  
 如果 `HoldoutMaxCases` 设置为默认值 0，并且没有设置 `HoldoutMaxPercent` 的值，则算法会将整个数据集用于定型。  
  
 新属性`HoldoutMaxCases`， `HoldoutMaxPercent`， `HoldoutSeed`，或`HoldoutActualSize`仅适用于[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]及更高版本。 因此，您必须在语法描述中所示前缀这些属性与新的命名空间或[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]将返回错误。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持对挖掘结构使用维持分区。 因此，包含 `HoldoutMaxCases`、`HoldoutMaxPercent`、`HoldoutSeed` 或 `HoldoutActualSize` 维持参数之一的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 语句不能在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中使用。 如果在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中将这些维持参数之一用于 ASSL 语句，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回错误。  
  
 父级对应的元素`HoldoutMaxCases`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)   
 [HoldoutMaxPercent 元素](holdoutmaxpercent-element.md)   
 [HoldoutSeed 元素](holdoutseed-element.md)   
 [HoldoutActualSize 元素](holdoutactualsize-element.md)  
  
  
