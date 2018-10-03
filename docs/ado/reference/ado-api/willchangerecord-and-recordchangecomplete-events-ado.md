---
title: WillChangeRecord 和 RecordChangeComplete 事件 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: dd31a75a45bd38bda04655bbb47daca09714803c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822006"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord 和 RecordChangeComplete 事件 (ADO)
**WillChangeRecord**事件之前，将调用一个或多个记录 （行）[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)更改。 **RecordChangeComplete**后调用事件或更多的记录更改。  
  
## <a name="syntax"></a>语法  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，该值指定此事件的原因。 其值可以是**adRsnAddNew**， **adRsnDelete**， **adRsnUpdate**， **adRsnUndoUpdate**， **adRsnUndoAddNew**， **adRsnUndoDelete**，或**adRsnFirstChange**。  
  
 *cRecords*  
 一个**长**值，该值指示 （受影响） 的更改的记录数。  
  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述了如果发生的错误的值*adStatus*是**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 当**WillChangeRecord**是调用，此参数设置为**adStatusOK**引发该事件的操作是否成功。 设置为**adStatusCantDeny**如果此事件不能请求取消的挂起的操作。  
  
 当**RecordChangeComplete**是调用，此参数设置为**adStatusOK**引发该事件的操作是否成功，或向**adStatusErrorsOccurred**如果操作失败。  
  
 之前**WillChangeRecord**返回时，将此参数设置为**adStatusCancel**请求取消操作的操作导致此事件或将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 之前**RecordChangeComplete**返回时，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pRecordset*  
 一个**记录集**对象。 **记录集**有关发生此事件。  
  
## <a name="remarks"></a>备注  
 一个**WillChangeRecord**或**RecordChangeComplete**事件可能是由于以下行中的第一个已更改字段**记录集**operations: [更新](../../../ado/reference/ado-api/update-method.md)，[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)， [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)， [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，和[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)。 值**记录集** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)确定哪些操作会导致要发生的事件。  
  
 期间**WillChangeRecord**事件，**记录集**[筛选器](../../../ado/reference/ado-api/filter-property.md)属性设置为**adFilterAffectedRecords**。 处理该事件时，不能更改此属性。  
  
 必须设置**adStatus**参数**adStatusUnwantedEvent**对每个可能**adReason**值完全停用的任何事件，其中包括事件通知**adReason**参数。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
