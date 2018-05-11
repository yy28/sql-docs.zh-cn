---
title: 调用元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7bd2f244068919e428bccedc6114e1d7656a5ab3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="invocation-element-assl"></a>Invocation 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定如何[操作](../../../analysis-services/scripting/objects/action-element-assl.md)应被调用。  
  
## <a name="syntax"></a>語法  
  
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
  
## <a name="remarks"></a>備註  
 操作的调用取决于客户端应用程序。 **调用**元素如何操作处理方式，并且不表示到的实例提供的建议客户端应用程序到[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]如何调用一个操作。  
  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*交互式*|由用户交互调用。|  
|*OnOpen*|当客户端应用程序打开对象时调用。|  
|*批处理*|由批处理命令调用。|  
  
 对应于的允许值为枚举**调用**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
