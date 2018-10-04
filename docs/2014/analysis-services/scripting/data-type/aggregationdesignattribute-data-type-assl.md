---
title: AggregationDesignAttribute 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationDesignAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationDesignAttribute
helpviewer_keywords:
- AggregationDesignAttribute data type
ms.assetid: 03d29d76-e4bd-4035-92cc-35149d83fbf9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c20be714c6a302f7ba913cacc67b86f70c5379f0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48163298"
---
# <a name="aggregationdesignattribute-data-type-assl"></a>AggregationDesignAttribute 数据类型 (ASSL)
  定义一个基元数据类型，表示属性之间的关联和一个[AggregationDesignDimension](dimension-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationDesignAttribute>  
   <AttributeID>...</AttributeID>  
      <EstimatedCount>...</EstimatedCount>  
</AggregationDesignAttribute>  
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
|子元素|[AttributeID](../properties/id-element-assl.md)， [EstimatedCount](../properties/estimatedcount-element-assl.md)|  
|派生元素|[特性](../objects/attribute-element-assl.md)([特性](../collections/attributes-element-assl.md)的集合[AggregationDesignDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationDesignAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [AggregationDesignDimension 数据类型&#40;ASSL&#41;](dimension-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
