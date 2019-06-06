---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 18ffebe5cbf781212b6b8962f9f48d61281c7d30
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703986"
---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Rds[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，指定异步检索数据的线程的执行优先级。  
  
 使用与这些常量**记录集**"**后台线程优先级**"动态属性，它是在 ADO OLE DB 动态属性索引中引用和中所述[用于 OLE DB 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)文档。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|设置之间正常和最高的优先级。|  
|**adPriorityBelowNormal**|2|设置最低和正常之间的优先级。|  
|**adPriorityHighest**|5|优先级设置为的最大可能。|  
|**AdPriorityLowest**|1|设置尽可能低的优先级。|  
|**adPriorityNormal**|3|优先级设置为 normal。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|
