---
title: MeasureGroupAttribute 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroupAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupAttribute
helpviewer_keywords:
- MeasureGroupAttribute data type
ms.assetid: dc7f71e6-3755-4d99-9fcd-5830e10eb653
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 996fdfbec8996d925c67f55f4dd6ad3cf423d0b6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177797"
---
# <a name="measuregroupattribute-data-type-assl"></a>MeasureGroupAttribute 数据类型 (ASSL)
  定义一个基元数据类型，该类型表示属性和度量值组之间的关系。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroupAttribute>  
   <AttributeID>...</AttributeID>  
      <KeyColumns>...</KeyColumns>  
   <Type>...</Type>  
   <Annotations>...</Annotations>  
</MeasureGroupAttribute>  
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
|子元素|[批注](../collections/annotations-element-assl.md)， [AttributeID](../properties/id-element-assl.md)， [KeyColumns](../collections/columns-element-assl.md)，[类型](../properties/type-element-measuregroupattribute-assl.md)|  
|派生元素|[特性](../objects/attribute-element-assl.md)([特性](../collections/attributes-element-assl.md)的集合[RegularMeasureGroupDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MeasureGroupAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
