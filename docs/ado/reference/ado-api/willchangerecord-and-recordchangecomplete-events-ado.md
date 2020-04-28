---
title: WillChangeRecord 和 RecordChangeComplete 事件（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e632db34fbbacbee61cd943067052af27a8cfe8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938677"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord 和 RecordChangeComplete 事件 (ADO)
在[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)的一个或多个记录（行）更改之前调用**WillChangeRecord**事件。 在一个或多个记录发生更改后调用**RecordChangeComplete**事件。  
  
## <a name="syntax"></a>语法  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>参数  
 *adReason*  
 一个[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，该值指定此事件的原因。 其值可以是**adRsnAddNew**、 **adRsnDelete**、 **adRsnUpdate**、 **adRsnUndoUpdate**、 **adRsnUndoAddNew**、 **adRsnUndoDelete**或**adRsnFirstChange**。  
  
 *cRecords*  
 **长整型**值，指示更改（受影响）的记录数。  
  
 *pError*  
 一个[错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述了*adStatus*的值为**adStatusErrorsOccurred**时所发生的错误;否则，不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 调用**WillChangeRecord**时，如果导致事件的操作成功，则将此参数设置为**adStatusOK** 。 如果此事件无法请求取消挂起操作，则将其设置为**adStatusCantDeny** 。  
  
 调用**RecordChangeComplete**时，如果导致事件的操作成功，则此参数设置为**adStatusOK** ; 如果操作失败，则设置为**adStatusErrorsOccurred** 。  
  
 在**WillChangeRecord**返回之前，将此参数设置为**adStatusCancel** ，以请求取消引发此事件的操作，或将此参数设置为**adStatusUnwantedEvent**以阻止后续通知。  
  
 在**RecordChangeComplete**返回之前，将此参数设置为**adStatusUnwantedEvent** ，以防止后续通知。  
  
 *pRecordset*  
 **记录集**对象。 发生此事件的**记录集**。  
  
## <a name="remarks"></a>备注  
 由于以下**记录集**操作，行中第一个已更改的字段可能发生**WillChangeRecord**或**RecordChangeComplete**事件： [Update](../../../ado/reference/ado-api/update-method.md)、 [Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)、 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)、 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)和[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)。 **记录集** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)的值确定导致事件发生的操作。  
  
 在**WillChangeRecord**事件期间，"**记录集**[筛选器](../../../ado/reference/ado-api/filter-property.md)" 属性设置为 " **adFilterAffectedRecords**"。 在处理事件时，不能更改此属性。  
  
 必须为每个可能的**adReason**值将**adStatus**参数设置为**adStatusUnwantedEvent** ，以完全停止包含**adReason**参数的任何事件的事件通知。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
