---
title: "DefaultValue 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DefaultValue Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DefaultValue
helpviewer_keywords:
- DefaultValue element
ms.assetid: 87e964a3-f317-46c3-98c7-b3621765c77b
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9477af89e608fbf45d10fbdca08e6a5cc8fac769
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="defaultvalue-element-assl"></a>DefaultValue 元素 (ASSL)
  包含关联的只读的默认值[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ServerProperty>  
   ...  
   <DefaultValue>   </DefaultValue>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|任何 simpleType|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素包含的只读安装默认值**ServerProperty**的当前实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 该默认值由当前实例提供，并且通常不能更改。  
  
 对应于的父元素**DefaultValue**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>另请参阅  
 [ServerProperties 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)   
 [服务器元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

