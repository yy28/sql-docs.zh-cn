---
title: Source 元素 (ComAssembly) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Source Element (ComAssembly)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 5c9209e8-ace6-4688-a64d-4987a7648ab9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7c6259d5bec6c2c1e371df5d9412ccdbc5489a1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106507"
---
# <a name="source-element-comassembly-assl"></a>Source 元素 (ComAssembly) (ASSL)
  包含组件对象模型 (COM) 组件的文件名或编程标识符 (ProgID)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ComAssembly>  
   ...  
   <Source>...</Source>  
   ...  
</ComAssembly>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ComAssembly](../data-type/assembly-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`Source`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ComAssembly>。  
  
## <a name="see-also"></a>请参阅  
 [Assembly 元素&#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [ClrAssembly 数据类型&#40;ASSL&#41;](../data-type/clrassembly-data-type-assl.md)   
 [程序集元素&#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [数据库元素&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [服务器元素&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
