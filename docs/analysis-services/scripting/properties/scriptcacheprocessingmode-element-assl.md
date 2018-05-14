---
title: ScriptCacheProcessingMode 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c6d355029964905071bcef03ac8721e5df2208f9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="scriptcacheprocessingmode-element-assl"></a>ScriptCacheProcessingMode 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|默认值|*Regular*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*Regular*|服务器在处理过程中生成脚本缓存。|  
|*延迟*|服务器在处理之后生成脚本缓存。|  
  
 对应于的允许值为枚举**ScriptCacheProcessingMode**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ScriptCacheProcessingMode>。  
  
 对应于的父元素**ScriptCacheProcessingMode**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Cube>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
