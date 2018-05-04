---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11e7151dea1e522b1c265313043f840c2cced8a4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
为 RDS[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，指定检索数据的异步线程的执行优先级。  
  
 使用与这些常量**记录集**"**后台线程优先级**"动态属性，用于进行中的 ADO OLE DB 动态属性索引引用并记录在[用于 OLE DB 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)文档。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|设置之间正常和最高的优先级。|  
|**adPriorityBelowNormal**|2|最低和普通之间设置优先级。|  
|**adPriorityHighest**|5|设置到的最大可能的优先级。|  
|**AdPriorityLowest**|1|设置尽可能低的优先级。|  
|**adPriorityNormal**|3|将优先级设置为正常。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|
