---
title: QueryNotification 元素 (ASSL) |Microsoft 文档
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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3c9bc13772d549d6ade640af4c3f57ac52efbbec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126925"
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
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.QueryNotification>。  
  
## <a name="see-also"></a>请参阅  
 [ProactiveCachingQueryBinding 数据类型&#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  