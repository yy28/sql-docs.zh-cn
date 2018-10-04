---
title: TableNotifications 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- TableNotifications Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- TableNotifications element
ms.assetid: 4cecdfea-0d4d-4bd6-bbb3-4d0d2284c665
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d4c48ef76db4a1dd2a96008c108d050ff832fd52
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188827"
---
# <a name="tablenotifications-element-assl"></a>TableNotifications 元素 (ASSL)
  包含的集合[TableNotification](../objects/tablenotification-element-assl.md)提供的信息的元素[ProactiveCaching](../objects/proactivecaching-element-assl.md)有关表或视图的数据源中修改过的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProactiveCachingTablesBinding>  
   <TableNotifications>  
      <TableNotification>...</TableNotification>  
...</TableNotifications>  
</ProactiveCachingTablesBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ProactiveCachingTablesBinding](../data-type/binding-data-type-assl.md)|  
|子元素|[TableNotification](../objects/tablenotification-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.TableNotificationCollection>。  
  
## <a name="see-also"></a>请参阅  
 [ProactiveCachingBinding 数据类型&#40;ASSL&#41;](../data-type/proactivecachingbinding-data-type-assl.md)   
 [ProactiveCachingObjectNotificationBinding 数据类型&#40;ASSL&#41;](../data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
