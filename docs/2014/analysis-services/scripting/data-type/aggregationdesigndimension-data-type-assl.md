---
title: AggregationDesignDimension 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationDesignDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationDesignDimension
helpviewer_keywords:
- AggregationDesignDimension data type
ms.assetid: 06a0d418-014c-4f40-a63a-5cfeee3f6a41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 758fc3a42b2ff1277deda1e7cff566b9eba17a26
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200407"
---
# <a name="aggregationdesigndimension-data-type-assl"></a>AggregationDesignDimension 数据类型 (ASSL)
  定义一个基元数据类型表示多维数据集维度之间的关系，并[AggregationDesign](../objects/aggregationdesign-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationDesignDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Attributes>...</Attributes>  
      <Annotations>...</Annotations>  
</AggregationDesignDimension>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|None|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[批注](../collections/annotations-element-assl.md)，[特性](../collections/attributes-element-assl.md)， [CubeDimensionID](../properties/id-element-assl.md)|  
|派生元素|[维度](../objects/dimension-element-assl.md)([维度](../collections/dimensions-element-assl.md)的集合[AggregationDesign](../objects/aggregationdesign-element-assl.md))|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationDesignDimension>。  
  
## <a name="see-also"></a>请参阅  
 [AggregationDesign 元素&#40;ASSL&#41;](../objects/aggregationdesign-element-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
