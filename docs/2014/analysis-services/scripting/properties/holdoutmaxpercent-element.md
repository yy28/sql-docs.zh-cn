---
title: HoldoutMaxPercent 元素 |Microsoft 文档
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
- HoldoutMaxPercent
helpviewer_keywords:
- HoldoutMaxPercent element
ms.assetid: e375cc51-5f9d-4252-98a1-326ca0dbbf83
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 089ed35d7c900e48da2ba283f8bcf9ee4a29fa7a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016933"
---
# <a name="holdoutmaxpercent-element"></a>HoldoutMaxPercent 元素
  指定数据源中将用于维持部分包含的测试组的事例的最大百分比[MiningStructure](../objects/miningstructure-element-assl.md)元素。 其余事例用于定型。 值为 0 指示对可作为测试集来维持的事例数没有限制。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxPercent>...</ddl100_100:HoldoutMaxPercent>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|0 到 99 之间的整数。|  
|默认值|30|  
|基数|0-1：可出现一次并仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 如果 `HoldoutMaxPercent` 和 `HoldoutMaxCases` 的值都指定，则算法会将测试集限制为这两个值中的较小值。  
  
 如果`HoldoutMaxCases`设置为默认值 0，并且尚未为设置一个值`HoldoutMaxPercent`，该算法使用完整的数据集以进行训练。  
  
 新属性`HoldoutMaxCases`， `HoldoutMaxPercent`， `HoldoutSeed`，或`HoldoutActualSize`仅在可用[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]及更高版本。 因此，必须在这些属性前加上新的命名空间前缀，如语法说明中所示，否则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回错误。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持对挖掘结构使用维持分区。 因此，包含 `HoldoutMaxCases`、`HoldoutMaxPercent`、`HoldoutSeed` 或 `HoldoutActualSize` 维持参数之一的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 语句不能在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中使用。 如果在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中将这些维持参数之一用于 ASSL 语句，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回错误。  
  
 对应于的父元素`HoldoutMaxPercent`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)   
 [HoldoutMaxCases 元素](holdoutmaxcases-element.md)   
 [HoldoutSeed 元素](holdoutseed-element.md)   
 [HoldoutActualSize 元素](holdoutactualsize-element.md)  
  
  