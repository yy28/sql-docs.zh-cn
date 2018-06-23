---
title: KeyColumn 元素 (ASSL) |Microsoft 文档
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
- KeyColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KeyColumn
helpviewer_keywords:
- KeyColumn element
ms.assetid: 7b03eeb3-d478-4c38-822e-8cdfcc485039
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7594a92eb8c2eb4cdb423c7298bc3929dc49dc32
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018718"
---
# <a name="keycolumn-element-assl"></a>KeyColumn 元素 (ASSL)
  包含某个列的定义，该列用作属性键或属性键的一部分。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<KeyColumns>  
   <KeyColumn xsi:type="DataItem">...</KeyColumn>  
<KeyColumns>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|默认值|InclusionThresholdSetting|  
|基数|1-n：可多次出现的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[KeyColumns](../collections/columns-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 有关详细信息`DataItem`类型，包括 Analysis Services 脚本语言 (ASSL) 对象和属性表`DataItem`类型，请参阅[DataItem 数据类型&#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `KeyColumns` 集合的父级对应的元素为 <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>、<xref:Microsoft.AnalysisServices.DimensionAttribute>、<xref:Microsoft.AnalysisServices.MeasureGroupAttribute> 和 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>请参阅  
 [AggregationInstanceAttribute 数据类型&#40;ASSL&#41;](../data-type/aggregationinstanceattribute-data-type-assl.md)   
 [AggregationInstanceCubeDimension 数据类型&#40;ASSL&#41;](../data-type/dimension-data-type-assl.md)   
 [DimensionAttribute 数据类型&#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [MeasureGroupAttribute 数据类型&#40;ASSL&#41;](../data-type/measuregroupattribute-data-type-assl.md)   
 [ScalarMiningStructureColumn 数据类型&#40;ASSL&#41;](../data-type/miningstructurecolumn-data-type-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  