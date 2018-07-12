---
title: QueryNotification 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- QueryNotification Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- QueryNotification element
ms.assetid: 0ee06730-81ff-4913-96e6-f39b6f181650
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7d31cef8ee52964bf9aeb0c7c489f2831f5cb80
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153298"
---
# <a name="querynotification-element-assl"></a>QueryNotification 元素 (ASSL)
  包含确定数据源是否已修改时所执行的查询相关的 [ProactiveCaching](proactivecaching-element-assl.md) 元素信息。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<QueryNotifications>  
   <QueryNotification>  
      <Query>...</Query>  
...</QueryNotification>  
</QueryNotifications>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|1-n：可多次出现的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[QueryNotifications](../collections/querynotifications-element-assl.md)|  
|子元素|[“数据集属性”](../properties/query-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.QueryNotification>。  
  
## <a name="see-also"></a>请参阅  
 [ProactiveCachingQueryBinding 数据类型&#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
