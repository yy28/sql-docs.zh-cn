---
title: EventID 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bd00f73399d4eb3711f5783060c26003cfc667c2
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="eventid-element-assl"></a>EventID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  唯一标识[事件](../../../analysis-services/scripting/objects/event-element-assl.md)元素要作为的一部分捕获[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Event>  
  
      <EventID>...</EventID>  
  
</Event>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[事件](../../../analysis-services/scripting/objects/event-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对父级的对应的元素**EventID**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.TraceEvent>。  
  
## <a name="see-also"></a>另请参阅  
 [Events 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
