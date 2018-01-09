---
title: "字体名称元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: FontName Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: FontName
helpviewer_keywords: FontName element
ms.assetid: 5560a852-9745-4abb-93d8-9cebe8a9897c
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 77be8f2a2eeb89338f15dc21bf10ab424f650f73
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="fontname-element-assl"></a>FontName 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]描述字体相关显示特征[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)或[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)父元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <FontName>...</FontName>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)，[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **字体名称**属性包含的多维表达式 (MDX) 表达式，并将应用于**CalculationProperty**元素具有[CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)的*成员*或*单元格*。  
  
 对应的父级的元素**字体名称**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CalculationProperty>和<xref:Microsoft.AnalysisServices.Measure>。  
  
## <a name="see-also"></a>另请参阅  
 [CalculationProperties 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Mdxscript 被元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
