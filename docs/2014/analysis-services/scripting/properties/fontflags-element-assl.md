---
title: FontFlags 元素 (ASSL) |Microsoft 文档
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
- FontFlags Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- FontFlags
helpviewer_keywords:
- FontFlags element
ms.assetid: ea608da9-ab05-42ab-8872-c52cd9f3f546
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 93dfd53940270fb444dd797bfd4d085ab459d200
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028238"
---
# <a name="fontflags-element-assl"></a>FontFlags 元素 (ASSL)
  描述字体相关显示特征[CalculationProperty](../objects/calculationproperty-element-assl.md)或[度量值](../objects/measure-element-assl.md)父元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
      <FontFlags>...</FontFlags>  
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
|父元素|[CalculationProperty](../objects/calculationproperty-element-assl.md)，[度量值](../objects/measure-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `FontFlags`属性包含的多维表达式 (MDX) 表达式，并将应用于`CalculationProperty`元素具有[CalculationType](calculationtype-element-assl.md)的*成员*或*单元格*.  
  
 对应的父级的元素`FontFlags`分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CalculationProperty>和<xref:Microsoft.AnalysisServices.Measure>。  
  
## <a name="see-also"></a>请参阅  
 [CalculationProperties 元素&#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 元素&#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [Mdxscript 被元素&#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  