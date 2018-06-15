---
title: WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::RecordsetChangeComplete
- RecordsetChangeComplete
- Recordset::WillChangeRecordset
- WillChangeRecordset
helpviewer_keywords:
- RecordsetChangeComplete event [ADO]
- WillChangeRecordset event [ADO]
ms.assetid: d5d44659-e0d9-46d9-a297-99c43555082f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63962d0ce3c8c4a5bf5aa0274a4084a9f8d84a5f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282796"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)
**WillChangeRecordset**挂起的操作更改之前，将调用事件[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。 **RecordsetChangeComplete**事件后，会调用**记录集**已更改。  
  
## <a name="syntax"></a>语法  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，该值指定此事件的原因。 其值可以是**adRsnRequery**， **adRsnResynch**， **adRsnClose**， **adRsnOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 当**WillChangeRecordset**是调用，此参数设置为**adStatusOK**引起该事件的操作是否成功。 设置为**adStatusCantDeny**如果此事件不能请求取消挂起操作。  
  
 当**RecordsetChangeComplete**是调用，此参数设置为**adStatusOK**引起该事件的操作是否成功， **adStatusErrorsOccurred**如果操作失败，或**adStatusCancel**如果该操作与以前接受**WillChangeRecordset**事件已被取消。  
  
 之前**WillChangeRecordset**返回时，将此参数设置为**adStatusCancel**若要请求取消挂起操作或将此参数设置为 adStatusUnwantedEvent 以防止后续发送通知。  
  
 之前**WillChangeRecordset**或**RecordsetChangeComplete**返回时，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述发生错误的值*adStatus*是**adStatusErrorsOccurred**; 不会设置。  
  
 *pRecordset*  
 A**记录集**对象。 **记录集**此事件发生的。  
  
## <a name="remarks"></a>Remarks  
 A **WillChangeRecordset**或**RecordsetChangeComplete**事件可能会发生由于**记录集** [Requery](../../../ado/reference/ado-api/requery-method.md)或[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法。  
  
 如果提供程序不支持书签， **RecordsetChange**新行从提供程序检索每次发生的事件通知。 此事件的频率取决于**RecordsetCacheSize**属性。  
  
 必须设置**adStatus**参数**adStatusUnwantedEvent**对每个可能**adReason**值完全停用包括任何事件的事件通知**adReason**参数。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
