---
title: "CalculationProperty 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CalculationProperty Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CalculationProperty
helpviewer_keywords:
- CalculationProperty element
ms.assetid: 5f0b4cfc-7d25-4c01-a517-cc2e89859be3
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 499f002694022d737b7711c0d69891a5b08059eb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="calculationproperty-element-assl"></a>CalculationProperty 元素 (ASSL)
  包含集合的计算中使用的用户界面属性[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CalculationProperties](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)|  
|子元素|[AssociatedMeasureGroupID](../../../analysis-services/scripting/properties/associatedmeasuregroupid-element-assl.md)， [BackColor](../../../analysis-services/scripting/properties/backcolor-element-assl.md)， [CalculationReference](../../../analysis-services/scripting/properties/calculationreference-element-assl.md)， [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)，[DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md)， [FontFlags](../../../analysis-services/scripting/properties/fontflags-element-assl.md)，[字体名称](../../../analysis-services/scripting/properties/fontname-element-assl.md)， [FontSize](../../../analysis-services/scripting/properties/fontsize-element-assl.md)， [ForeColor](../../../analysis-services/scripting/properties/forecolor-element-assl.md)，[FormatString](../../../analysis-services/scripting/properties/formatstring-element-assl.md)， [NonEmptyBehavior](../../../analysis-services/scripting/properties/nonemptybehavior-element-assl.md)， [SolveOrder](../../../analysis-services/scripting/properties/solveorder-element-assl.md)，[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)，[可见](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CalculationProperty>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

