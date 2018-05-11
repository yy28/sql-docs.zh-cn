---
title: 源元素 (ComAssembly) (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1d90d4e6a521c4a8adf70f97b0edc1a35b7cd75d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="source-element-comassembly-assl"></a>Source 元素 (ComAssembly) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ComAssembly](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**源**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ComAssembly>。  
  
## <a name="see-also"></a>另请参阅  
 [Assembly 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [ClrAssembly 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [数据库元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [服务器元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
