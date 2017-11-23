---
title: "字体名称元素 (ASSL) |Microsoft 文档"
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
ms.openlocfilehash: 7aad7d3dca0d1153bdc7a5235160c348a95354a2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="fontname-element-assl"></a>FontName 元素 (ASSL)
  描述字体相关显示特征[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)或[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)父元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <FontName>...</FontName>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)，[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **字体名称**属性包含的多维表达式 (MDX) 表达式，并将应用于**CalculationProperty**元素具有[CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)的*成员*或*单元格*。  
  
 对应的父级的元素**字体名称**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CalculationProperty>和<xref:Microsoft.AnalysisServices.Measure>。  
  
## <a name="see-also"></a>另请参阅  
 [CalculationProperties 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Mdxscript 被元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
