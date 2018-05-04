---
title: WillChangeRecord 和 RecordChangeComplete 事件 (ADO) |Microsoft 文档
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
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77d02d1a5b5d643c49fcbbd33057d6c709f1949a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord 和 RecordChangeComplete 事件 (ADO)
**WillChangeRecord**事件调用一个或多个记录 （行） 之前[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)更改。 **RecordChangeComplete**事件时调用后一个或多个记录更改。  
  
## <a name="syntax"></a>语法  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，该值指定此事件的原因。 其值可以是**adRsnAddNew**， **adRsnDelete**， **adRsnUpdate**， **adRsnUndoUpdate**， **adRsnUndoAddNew**， **adRsnUndoDelete**，或**adRsnFirstChange**。  
  
 *cRecords*  
 A**长**值，该值指示 （受影响） 的更改的记录数。  
  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述发生错误的值*adStatus*是**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 当**WillChangeRecord**是调用，此参数设置为**adStatusOK**引起该事件的操作是否成功。 设置为**adStatusCantDeny**如果此事件不能请求取消挂起操作。  
  
 当**RecordChangeComplete**是调用，此参数设置为**adStatusOK**引起该事件的操作是否成功，或到**adStatusErrorsOccurred**如果操作失败。  
  
 之前**WillChangeRecord**返回时，将此参数设置为**adStatusCancel**到请求取消操作导致此事件，或将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 之前**RecordChangeComplete**返回时，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pRecordset*  
 A**记录集**对象。 **记录集**此事件发生的。  
  
## <a name="remarks"></a>注释  
 A **WillChangeRecord**或**RecordChangeComplete**事件可能会发生的原因如下行中的第一个已更改字段**记录集**操作： [更新](../../../ado/reference/ado-api/update-method.md)，[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)，[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)， [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，和[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)。 值**记录集**[游标类型](../../../ado/reference/ado-api/cursortype-property-ado.md)确定哪些操作会导致要发生的事件。  
  
 期间**WillChangeRecord**事件，**记录集**[筛选器](../../../ado/reference/ado-api/filter-property.md)属性设置为**adFilterAffectedRecords**。 在处理该事件时，无法更改此属性。  
  
 必须设置**adStatus**参数**adStatusUnwantedEvent**对每个可能**adReason**值完全停用包括任何事件的事件通知**adReason**参数。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
