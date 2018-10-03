---
title: Event 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Event Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EVENT
helpviewer_keywords:
- Event element
ms.assetid: c7911bcd-e601-4a96-a6d8-20b7c7375ff2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 417035dadf738cd6f1302da6a543bf46e9c4b8c9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067610"
---
# <a name="event-element-assl"></a>Event 元素 (ASSL)
  定义`Event`作为的一部分捕获[跟踪](trace-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Events>  
   <Event>  
      <EventID>...</EventID>  
      <Columns>...</Columns>  
   </Event>  
</Events>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|1-n：可多次出现的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[事件](../collections/events-element-assl.md)|  
|子元素|[列](../collections/columns-element-assl.md)， [EventID](../properties/id-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.TraceEvent>。  
  
## <a name="see-also"></a>请参阅  
 [跟踪元素&#40;ASSL&#41;](trace-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
