---
title: TableNotification 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TableNotification Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- TableNotification element
ms.assetid: 3afd075a-74f9-428c-b527-ee497cbe71e7
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 12dec839000f56e8d82a3f5b0e6398f20ccfb35f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126403"
---
# <a name="tablenotification-element-assl"></a>TableNotification 元素 (ASSL)
  包含信息[ProactiveCaching](proactivecaching-element-assl.md)有关的表或视图已修改的数据源中的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<TableNotifications>  
   <TableNotification>  
      <DbTableName>...</DbTableName>  
      <DbSchemaName>...</DbSchemaName>  
...</TableNotification>  
</TableNotifications>  
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
|父元素|[TableNotifications](../collections/tablenotifications-element-assl.md)|  
|子元素|[DbSchemaName](../properties/name-element-assl.md)， [DbTableName](../properties/dbtablename-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.TableNotification>。  
  
## <a name="see-also"></a>请参阅  
 [ProactiveCachingTablesBinding 数据类型&#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [ProactiveCachingObjectNotificationBinding 数据类型&#40;ASSL&#41;](../data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)   
 [ProactiveCachingBinding 数据类型&#40;ASSL&#41;](../data-type/proactivecachingbinding-data-type-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  