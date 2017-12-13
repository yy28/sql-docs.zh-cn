---
title: "KeyColumn 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: KeyColumn Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: KeyColumn
helpviewer_keywords: KeyColumn element
ms.assetid: 7b03eeb3-d478-4c38-822e-8cdfcc485039
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5ab895c6fe2eb527f531faf53aa687fe7e006a98
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="keycolumn-element-assl"></a>KeyColumn 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含，或是特性键的一部分的列的定义。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<KeyColumns>  
   <KeyColumn xsi:type="DataItem">...</KeyColumn>  
<KeyColumns>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|默认值|无|  
|基数|1-n：可多次出现的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关详细信息**DataItem**类型，包括 Analysis Services 脚本语言 (ASSL) 对象和属性表**DataItem**类型，请参阅[DataItem 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 对应的父级的元素**KeyColumns**分析管理对象 (AMO) 对象模型中的集合是<xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>， <xref:Microsoft.AnalysisServices.DimensionAttribute>， <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>，和<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另请参阅  
 [AggregationInstanceAttribute 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md)   
 [AggregationInstanceCubeDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)   
 [DimensionAttribute 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [MeasureGroupAttribute 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)   
 [ScalarMiningStructureColumn 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)   
 [对象 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
