---
title: "OrderBy 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- OrderBy Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- OrderBy
helpviewer_keywords:
- OrderBy element
ms.assetid: d7a0564b-430e-44eb-913a-fe1f98917d0f
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 35479ebb898200c9082a7e08369a3ae5d4c57ac3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="orderby-element-assl"></a>OrderBy 元素 (ASSL)
  说明如何对属性中包含的成员进行排序。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderBy>...</OrderBy>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*名称*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*名称*|按成员名称进行排序。|  
|*Key*|按成员键进行排序。|  
|*AttributeKey*|Order by 中指定的属性的成员键[OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md)元素**DimensionAttribute**。|  
|*AttributeName*|Order by 中指定的属性的成员名称**OrderByAttributeID**元素**DimensionAttribute**。|  
  
 对应于的允许值为枚举**OrderBy**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.OrderBy>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

