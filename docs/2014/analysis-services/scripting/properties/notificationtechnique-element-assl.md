---
title: NotificationTechnique 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NotificationTechnique Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- NotificationTechnique element
ms.assetid: 80c43de3-f147-4bf5-bb85-da9d182ce415
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8dc05b03286785e2d06d5595897a263a294ae97e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48139472"
---
# <a name="notificationtechnique-element-assl"></a>NotificationTechnique 元素 (ASSL)
  指定是否[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或外部客户端应用程序处理通知。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProactiveCachingBinding>  
   <NotificationTechnique>...</NotificationTechnique>  
</ProactiveCachingBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*客户端*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ProactiveCachingBinding](../data-type/binding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*客户端*|由外部客户端应用程序处理通知。|  
|*Server*|由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 处理通知。|  
  
 父级对应的元素`NotificationTechnique`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ProactiveCachingBinding>。  
  
 与允许的值相对应的枚举`NotificationTechnique`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.NotificationTechnique>。  
  
## <a name="see-also"></a>请参阅  
 [ProactiveCachingBinding 数据类型&#40;ASSL&#41;](../data-type/binding-data-type-assl.md)  
  
  
