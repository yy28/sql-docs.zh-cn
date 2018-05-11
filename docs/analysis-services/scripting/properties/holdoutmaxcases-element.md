---
title: HoldoutMaxCases 元素 |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 156363473a9354041ef4dfa9f9807e7b0d797214
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="holdoutmaxcases-element"></a>HoldoutMaxCases 元素
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定要用于维持部分包含的测试集的数据源中的最大事例数[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)元素。 数据集中的其余事例用于定型。 值为 0 指示对可作为测试集来维持的事例数没有限制。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxCases>...</ddl100_100:HoldoutMaxCases>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|大于 0 的整数。|  
|默认值|0|  
|基数|0-1：可出现一次并仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 如果为两个指定值**HoldoutMaxPercent**和**HoldoutMaxCases**，算法将限制测试设置为较小的两个值。  
  
 如果**HoldoutMaxCases**设置为默认值 0，并且尚未为设置一个值**HoldoutMaxPercent**，算法将整个数据集用于训练。  
  
 新属性**HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，或**HoldoutActualSize**仅在中可用[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]及更高版本。 因此，你必须对语法说明中所示前缀这些属性与新的命名空间或[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]将返回错误。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持对挖掘结构使用维持分区。 因此，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含维持参数之一的脚本语言 (ASSL) 语句**HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，或**HoldoutActualSize**，不能在[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 如果在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中将这些维持参数之一用于 ASSL 语句，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回错误。  
  
 对应于的父元素**HoldoutMaxCases**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>另请参阅  
 [属性&#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [HoldoutMaxPercent 元素](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)   
 [HoldoutSeed 元素](../../../analysis-services/scripting/properties/holdoutseed-element.md)   
 [HoldoutActualSize 元素](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)  
  
  
