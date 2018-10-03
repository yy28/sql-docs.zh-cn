---
title: SolveOrder 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- SolveOrder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SolveOrder
helpviewer_keywords:
- SolveOrder element
ms.assetid: ec43e055-97dd-4f2a-9a7c-2df2e1119e56
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4fbd4132a0dc27d9055956d4b49a1ad02bc5dff5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219507"
---
# <a name="solveorder-element-assl"></a>SolveOrder 元素 (ASSL)
  指示在其中的求解次序[CalculationProperty](../objects/calculationproperty-element-assl.md)元素应用于计算的成员或计算的单元定义。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CalculationProperty>  
   ...  
   <SolveOrder>...</SolveOrder>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../objects/calculationproperty-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `SolveOrder`属性适用于`CalculationProperty`元素[CalculationType](calculationtype-element-assl.md)的*成员*或者*单元格*。  
  
 父级对应的元素`SolveOrder`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.CalculationProperty>。  
  
## <a name="see-also"></a>请参阅  
 [CalculationProperties 元素&#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 元素&#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [MdxScripts 元素&#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
