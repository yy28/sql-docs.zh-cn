---
title: HoldoutActualSize 元素 |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9d73c9ba1e3028c3b5622bb27422fdb8774df518
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="holdoutactualsize-element"></a>HoldoutActualSize 元素
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  处理之后，包含的测试集的维持分区指示实际大小， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)元素。 数据集中的其余事例用于定型。 该属性为只读。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutActualSize>...</ddl100_100:HoldoutActualSize>  
   ...  
</MiningStructure  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|只读的整数值。|  
|默认值|不适用|  
|基数|0-1：可选元素，只显示一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 值**HoldoutActualSize**取决于源数据，和的值[HoldoutMaxCases](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)， [HoldoutMaxPercent](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)，和[HoldoutSeed](../../../analysis-services/scripting/properties/holdoutseed-element.md). 因此，值**HoldoutActualSize**将不可用之前[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]处理挖掘结构。  
  
 对应于的父元素**HoldoutActualSize**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持对挖掘结构使用维持分区。 因此，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含维持参数之一的脚本语言 (ASSL) 语句**HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，或**HoldoutActualSize**，不能在[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 如果在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中将这些维持参数之一用于 ASSL 语句，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回错误。  
  
## <a name="see-also"></a>另请参阅  
 [属性&#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [HoldoutMaxCases 元素](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)   
 [HoldoutMaxPercent 元素](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)   
 [HoldoutSeed 元素](../../../analysis-services/scripting/properties/holdoutseed-element.md)  
  
  
