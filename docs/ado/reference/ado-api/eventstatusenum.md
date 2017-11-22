---
title: "EventStatusEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: EventStatusEnum
helpviewer_keywords: EventStatusEnum enumeration [ADO]
ms.assetid: ebfd4cda-4017-4873-9d28-38b1c7db12a8
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: de4655072b5ce25b3fb35dbb8bc73b6334a9f6c6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="eventstatusenum"></a>EventStatusEnum
指定的事件执行的当前状态。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|请求取消操作导致事件发生。|  
|**adStatusCantDeny**|3|指示该操作无法请求取消挂起操作。|  
|**adStatusErrorsOccurred**|2|指示由于出现错误或错误失败引起该事件的操作。|  
|**adStatusOK**|1|指示引起该事件的操作已成功。|  
|**adStatusUnwantedEvent**|5|在事件方法已完成执行之前，可以防止后续的通知。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.EventStatus.CANCEL|  
|AdoEnums.EventStatus.CANTDENY|  
|AdoEnums.EventStatus.ERRORSOCCURRED|  
|AdoEnums.EventStatus.OK|  
|AdoEnums.EventStatus.UNWANTEDEVENT|  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[BeginTransComplete、 CommitTransComplete 和 RollbackTransComplete 事件 (ADO)](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|[ConnectComplete 和 Disconnect 事件 (ADO)](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|[EndOfRecordset 事件 (ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|  
|[ExecuteComplete 事件 (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)|[FetchComplete 事件 (ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|[InfoMessage 事件 (ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)|  
|[WillChangeField 和 FieldChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|[WillChangeRecord 和 RecordChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[WillConnect 事件 (ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)|[WillExecute 事件 (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|[WillMove 和 MoveComplete 事件 (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|
