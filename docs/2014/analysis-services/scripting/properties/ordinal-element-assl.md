---
title: Ordinal 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Ordinal Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Ordinal
helpviewer_keywords:
- Ordinal element
ms.assetid: 64e68ad5-439c-4c1d-9df4-ee90c56761b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 87957fdfa3adf85081c0a2ca6a6539917b9f9b81
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198737"
---
# <a name="ordinal-element-assl"></a>Ordinal 元素 (ASSL)
  指示要绑定到集合（如键和翻译）中的序号。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributeBinding> <!-- or CubeAttributeBinding -->  
   ...  
   <Ordinal>...</Ordinal>  
   ...  
</AttributeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|`0`|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributeBinding](../data-type/binding-data-type-assl.md)， [CubeAttributeBinding](../data-type/cubeattributebinding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `AttributeBinding` 并`CubeAttributeBinding`中的元素[类型](type-element-binding-assl.md)属性设置为*密钥*或*翻译*可以绑定到某个属性，又绑定到的集合列中数据源视图。 `Ordinal` 元素的值确定该集合中 `AttributeBinding` 或 `CubeAttributeBinding` 所指向的列。  
  
 父级对应的元素`Ordinal`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.AttributeBinding>和<xref:Microsoft.AnalysisServices.CubeAttributeBinding>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
