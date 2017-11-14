---
title: "ScriptCacheProcessingMode 元素 (ASSL) |Microsoft 文档"
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
- ScriptCacheProcessingMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ScriptCacheProcessingMode
helpviewer_keywords:
- ScriptCacheProcessingMode element
ms.assetid: 95c0723c-69a4-43e7-b743-f712180a7681
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1982cc5b9266f8d69d0975043c307ec3272d8149
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="scriptcacheprocessingmode-element-assl"></a>ScriptCacheProcessingMode 元素 (ASSL)
  指示服务器在处理期间或处理之后是否生成脚本缓存。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube>  
   ...  
      <ScriptCacheProcessingMode>...</ScriptCacheProcessingMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*正则*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*正则*|服务器在处理过程中生成脚本缓存。|  
|*延迟*|服务器在处理之后生成脚本缓存。|  
  
 对应于的允许值为枚举**ScriptCacheProcessingMode**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ScriptCacheProcessingMode>。  
  
 对应于的父元素**ScriptCacheProcessingMode**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Cube>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

