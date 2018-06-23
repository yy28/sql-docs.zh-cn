---
title: AggregationDesignAttribute 数据类型 (ASSL) |Microsoft 文档
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
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a6d65f5cbd6173218b4d33448ec442002290aad6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138524"
---
# <a name="aggregationdesignattribute-data-type-assl"></a>AggregationDesignAttribute 数据类型 (ASSL)
  定义表示属性之间的关联的基元数据类型和[AggregationDesignDimension](dimension-data-type-assl.md)元素。  
  
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
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[AttributeID](../properties/id-element-assl.md)， [EstimatedCount](../properties/estimatedcount-element-assl.md)|  
|派生元素|[属性](../objects/attribute-element-assl.md)([属性](../collections/attributes-element-assl.md)集合[AggregationDesignDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AggregationDesignAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [AggregationDesignDimension 数据类型&#40;ASSL&#41;](dimension-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  