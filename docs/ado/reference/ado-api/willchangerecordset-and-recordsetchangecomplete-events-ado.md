---
title: WillChangeRecordset 和 RecordsetChangeComplete 事件（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd4e2f1485c18ce1fecc76d4eb23aa4132d85329
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938686"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)
在挂起的操作更改[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)之前调用**WillChangeRecordset**事件。 更改**记录集**后，将调用**RecordsetChangeComplete**事件。  
  
## <a name="syntax"></a>语法  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>parameters  
 *adReason*  
 一个[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，该值指定此事件的原因。 其值可以是**adRsnRequery**、 **adRsnResynch**、 **adRsnClose**、 **adRsnOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 调用**WillChangeRecordset**时，如果导致事件的操作成功，则将此参数设置为**adStatusOK** 。 如果此事件无法请求取消挂起操作，则将其设置为**adStatusCantDeny** 。  
  
 调用**RecordsetChangeComplete**时，如果导致事件的操作成功，则将此参数设置为**adStatusOK** ; 如果操作失败，则设置为**adStatusErrorsOccurred** ; 如果已取消与先前接受的**WillChangeRecordset**事件关联的操作，则设置为**adStatusCancel** 。  
  
 在**WillChangeRecordset**返回之前，将此参数设置为**adStatusCancel** ，以请求取消挂起的操作或将此参数设置为 adStatusUnwantedEvent，以防止后续通知。  
  
 在**WillChangeRecordset**或**RecordsetChangeComplete**返回之前，将此参数设置为**adStatusUnwantedEvent** ，以防止后续通知。  
  
 *pError*  
 一个[错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述了*adStatus*的值为**adStatusErrorsOccurred**时所发生的错误;否则，不会设置。  
  
 *pRecordset*  
 **记录集**对象。 发生此事件的**记录集**。  
  
## <a name="remarks"></a>备注  
 **WillChangeRecordset**或**RecordsetChangeComplete**事件可能是由**记录集** [Requery](../../../ado/reference/ado-api/requery-method.md)或[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法导致的。  
  
 如果提供程序不支持书签，则每次从提供程序检索新行时都会发生**RecordsetChange**事件通知。 此事件的频率取决于**RecordsetCacheSize**属性。  
  
 必须为每个可能的**adReason**值将**adStatus**参数设置为**adStatusUnwantedEvent** ，以完全停止包含**adReason**参数的任何事件的事件通知。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
