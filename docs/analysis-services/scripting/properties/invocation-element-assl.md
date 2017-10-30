---
title: "调用元素 (ASSL) |Microsoft 文档"
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
- Invocation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Invocation
helpviewer_keywords:
- Invocation element
ms.assetid: f6bf64ad-ae57-4d46-bf92-1d07a65378bb
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d48dedecabb385ebacd752fff75d6ccec2e1489c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="invocation-element-assl"></a>Invocation 元素 (ASSL)
  指定如何[操作](../../../analysis-services/scripting/objects/action-element-assl.md)应被调用。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action>  
   ...  
   <Invocation>...</Invocation>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*交互式*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 操作的调用取决于客户端应用程序。 **调用**元素如何操作处理方式，并且不表示到的实例提供的建议客户端应用程序到[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]如何调用一个操作。  
  
 此元素的值限定为下表中的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*交互式*|由用户交互调用。|  
|*OnOpen*|当客户端应用程序打开对象时调用。|  
|*批处理*|由批处理命令调用。|  
  
 对应于的允许值为枚举**调用**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

