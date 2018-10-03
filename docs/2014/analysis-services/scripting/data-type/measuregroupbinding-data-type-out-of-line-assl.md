---
title: MeasureGroupBinding 数据类型 （的外部） (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroupBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupBinding
helpviewer_keywords:
- MeasureGroupBinding data type
ms.assetid: e6c65597-89ac-457e-a0e5-01d85449a1b7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a31e1d49636fc74f28639d898b18f26838ff389
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180137"
---
# <a name="measuregroupbinding-data-type-out-of-line-assl"></a>MeasureGroupBinding 数据类型（外部）(ASSL)
  定义一个基元数据类型，该类型表示与度量值组的绑定。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroupBinding>  
   <ID>...</ID>  
   <Source>...</Source>  
   <EstimatedRows>...</EstimatedRows>  
   <Dimensions>...</Dimensions>  
   <Measures>...</Measures>  
      <Partitions>...</Partitions>  
</MeasureGroupBinding>  
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
|子元素|[维度](../collections/dimensions-element-assl.md)， [EstimatedRows](../properties/estimatedrows-element-assl.md)， [ID](../properties/id-element-assl.md)，[度量值](../collections/measures-element-assl.md)，[分区](../collections/partitions-element-assl.md)，[源](../properties/source-element-binding-assl.md)|  
|派生元素|请参阅[绑定](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>备注  
 详细信息，请参阅部分中，带外部绑定中，在[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
