---
title: CalculationProperty 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CalculationProperty Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CalculationProperty
helpviewer_keywords:
- CalculationProperty element
ms.assetid: 5f0b4cfc-7d25-4c01-a517-cc2e89859be3
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 251cd4bd439fad70fd64e1c5ebf4be2965cf983d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37308397"
---
# <a name="calculationproperty-element-assl"></a>CalculationProperty 元素 (ASSL)
  包含用户界面中使用的计算的属性的集合[MdxScript](mdxscript-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CalculationProperties>  
   <CalculationProperty>  
      <CalculationReference>...</CalculationReference>  
      <CalculationType>...</CalculationType>  
      <Translations>...</Translations>  
      <Description>...</Description>  
      <Visible>...</Visible>  
      <SolveOrder>...</SolveOrder>  
      <FormatString>...</FormatString>  
      <ForeColor>...</ForeColor>  
      <BackColor>...</BackColor>  
            <FontName>...</FontName>  
            <FontSize>...</FontSize>  
            <FontFlags>...</FontFlags>  
            <NonEmptyBehavior>...</NonEmptyBehavior>  
      <AssociatedMeasureGroupID>...</AssociatedMeasureGroupID>  
      <DisplayFolder>...</DisplayFolder>  
   </CalculationProperty>  
</CalculationProperties>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CalculationProperties](../collections/calculationproperties-element-assl.md)|  
|子元素|[AssociatedMeasureGroupID](../properties/id-element-assl.md)， [BackColor](../properties/backcolor-element-assl.md)， [CalculationReference](../properties/calculationreference-element-assl.md)， [CalculationType](../properties/calculationtype-element-assl.md)，[说明](../properties/description-element-assl.md)，[DisplayFolder](../properties/displayfolder-element-assl.md)， [FontFlags](../properties/fontflags-element-assl.md)， [FontName](../properties/name-element-assl.md)， [FontSize](../properties/fontsize-element-assl.md)， [ForeColor](../properties/forecolor-element-assl.md)，[FormatString](../properties/formatstring-element-assl.md)， [NonEmptyBehavior](../properties/nonemptybehavior-element-assl.md)， [SolveOrder](../properties/solveorder-element-assl.md)，[翻译](../collections/translations-element-assl.md)，[可见](../properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CalculationProperty>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
