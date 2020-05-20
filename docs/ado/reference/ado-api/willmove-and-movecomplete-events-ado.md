---
title: WillMove 和 MoveComplete 事件（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::MoveComplete
- WillMove
- MoveComplete
- Recordset::WillMove
helpviewer_keywords:
- MoveComplete event [ADO]
- WillMove event [ADO]
ms.assetid: 1a3d1042-4f30-4526-a0c7-853c242496db
author: rothja
ms.author: jroth
ms.openlocfilehash: a714b0c8f6d41060dfe66e898f01d7ce1037e516
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764438"
---
# <a name="willmove-and-movecomplete-events-ado"></a>WillMove 和 MoveComplete 事件 (ADO)
在挂起的操作更改[记录集中](../../../ado/reference/ado-api/recordset-object-ado.md)的当前位置之前，调用**WillMove**事件。 在**记录集**的当前位置发生更改后，将调用**MoveComplete**事件。  
  
## <a name="syntax"></a>语法  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>参数  
 *adReason*  
 一个[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，该值指定此事件的原因。 其值可以是**adRsnMoveFirst**、 **adRsnMoveLast**、 **adRsnMoveNext**、 **adRsnMovePrevious**、 **adRsnMove**或**adRsnRequery**。  
  
 *pError*  
 一个[错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述了*adStatus*的值为**adStatusErrorsOccurred**时所发生的错误;否则，不会设置参数。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 调用**WillMove**时，如果导致事件的操作成功，则将此参数设置为**adStatusOK** 。 如果此事件无法请求取消挂起操作，则将其设置为**adStatusCantDeny** 。  
  
 调用**MoveComplete**时，如果导致事件的操作成功，则此参数设置为**adStatusOK** ; 如果操作失败，则设置为**adStatusErrorsOccurred** 。  
  
 在**WillMove**返回之前，将此参数设置为**adStatusCancel** ，以请求取消挂起的操作，或将此参数设置为**adStatusUnwantedEvent**以阻止后续通知。  
  
 在**MoveComplete**返回之前，将此参数设置为**adStatusUnwantedEvent** ，以防止后续通知。  
  
 *pRecordset*  
 [记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 发生此事件的**记录集**。  
  
## <a name="remarks"></a>备注  
 **WillMove**或**MoveComplete**事件可能因以下**记录集**操作而发生：[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)、[移动](../../../ado/reference/ado-api/move-method-ado.md)、 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)和[Requery](../../../ado/reference/ado-api/requery-method.md)。 这些事件可能由以下属性引起： [Filter](../../../ado/reference/ado-api/filter-property.md)、 [Index](../../../ado/reference/ado-api/index-property.md)、 [Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md)、 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)和[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)。 如果子**记录**集已连接**记录集**事件并移动了父**记录集**，也会发生这些事件。  
  
 必须为每个可能的*adReason*值将*adStatus*参数设置为**adStatusUnwantedEvent** ，以便完全停止包含*adReason*参数的任何事件的事件通知。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
