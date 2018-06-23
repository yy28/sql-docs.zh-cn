---
title: SolveOrder 元素 (ASSL) |Microsoft 文档
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
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ed5092f93494162179dc2ee142a6769eddd5d6da
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129071"
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
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../objects/calculationproperty-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `SolveOrder`属性适用于`CalculationProperty`元素[CalculationType](calculationtype-element-assl.md)的*成员*或*单元格*。  
  
 对应于的父元素`SolveOrder`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.CalculationProperty>。  
  
## <a name="see-also"></a>请参阅  
 [CalculationProperties 元素&#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 元素&#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [Mdxscript 被元素&#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  