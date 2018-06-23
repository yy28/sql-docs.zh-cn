---
title: EstimatedRows 元素 (ASSL) |Microsoft 文档
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
- EstimatedRows Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EstimatedRows
helpviewer_keywords:
- EstimatedRows element
ms.assetid: 08a66481-6479-4a93-aa7e-15e8b1f854f2
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0348e39cf3528c34028677a22c2bf7ec25697705
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123911"
---
# <a name="estimatedrows-element-assl"></a>EstimatedRows 元素 (ASSL)
  包含由父元素表示的估计行数。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationDesign> <!-- or Cube, MeasureGroup, MeasureGroupBinding, Partition -->  
   ...  
   <EstimatedRows>...</EstimatedRows>  
   ...  
</AggregationDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Long|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationDesign](../objects/aggregationdesign-element-assl.md)，[多维数据集](../objects/cube-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)， [MeasureGroupBinding](../data-type/binding-data-type-assl.md)，[分区](../objects/partition-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中，与 `EstimatedRows` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.AggregationDesign>、<xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.MeasureGroup>、<xref:Microsoft.AnalysisServices.MeasureGroupBinding> 和 <xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  