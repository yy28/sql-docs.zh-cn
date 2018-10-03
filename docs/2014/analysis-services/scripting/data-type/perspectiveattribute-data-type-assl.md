---
title: PerspectiveAttribute 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PerspectiveAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PerspectiveAttribute
helpviewer_keywords:
- PerspectiveAttribute data type
ms.assetid: bf4d45c1-e48d-4ada-bbab-49c3ac74948d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3d5e6220f4767d7cfb4b49553625426b5a499817
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055177"
---
# <a name="perspectiveattribute-data-type-assl"></a>PerspectiveAttribute 数据类型 (ASSL)
  定义一个基元数据类型，表示有关中的属性的信息[PerspectiveDimension](dimension-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<PerspectiveAttribute>  
      <AttributeID>...</AttributeID>  
   <DefaultMember>...</DefaultMember>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
      <Annotations>...</Annotations>  
</PerspectiveAttribute>  
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
|子元素|[批注](../collections/annotations-element-assl.md)， [AttributeHierarchyVisible](../properties/visible-element-assl.md)， [AttributeID](../properties/id-element-assl.md)， [DefaultMember](../objects/member-element-assl.md)|  
|派生元素|[特性](../objects/attribute-element-assl.md)([特性](../collections/attributes-element-assl.md)的集合[PerspectiveDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.PerspectiveAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
