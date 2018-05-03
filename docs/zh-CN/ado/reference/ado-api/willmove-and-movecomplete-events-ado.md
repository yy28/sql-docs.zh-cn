---
title: WillMove 和 MoveComplete 事件 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da4bdd6e13cea805ef4889b57955e6dee199ed9e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="willmove-and-movecomplete-events-ado"></a>WillMove 和 MoveComplete 事件 (ADO)
**WillMove**事件时调用之前的挂起操作更改中的当前位置[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。 **MoveComplete**中当前的位置后，将调用事件**记录集**更改。  
  
## <a name="syntax"></a>语法  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，该值指定此事件的原因。 其值可以是**adRsnMoveFirst**， **adRsnMoveLast**， **adRsnMoveNext**， **adRsnMovePrevious**， **adRsnMove**，或**adRsnRequery**。  
  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述发生错误的值*adStatus*是**adStatusErrorsOccurred**; 否则为未设置参数。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 当**WillMove**是调用，此参数设置为**adStatusOK**引起该事件的操作是否成功。 设置为**adStatusCantDeny**如果此事件不能请求取消挂起操作。  
  
 当**MoveComplete**是调用，此参数设置为**adStatusOK**引起该事件的操作是否成功，或到**adStatusErrorsOccurred**如果操作失败。  
  
 之前**WillMove**返回时，将此参数设置为**adStatusCancel**若要请求取消挂起的操作，或将此参数设置为**adStatusUnwantedEvent**若要防止后续的通知。  
  
 之前**MoveComplete**返回时，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pRecordset*  
 A[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 **记录集**此事件发生的。  
  
## <a name="remarks"></a>注释  
 A **WillMove**或**MoveComplete**事件可能导致以下**记录集**操作：[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)，[移动](../../../ado/reference/ado-api/move-method-ado.md)， [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)， [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)， [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)， [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)， [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)，和[Requery](../../../ado/reference/ado-api/requery-method.md)。 这些事件可能由于以下属性：[筛选器](../../../ado/reference/ado-api/filter-property.md)，[索引](../../../ado/reference/ado-api/index-property.md)，[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)， [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)，和[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)。 如果子级，也会发生这些事件**记录集**具有**记录集**连接的事件和父**记录集**移动。  
  
 必须设置*adStatus*参数**adStatusUnwantedEvent**对每个可能*adReason*若要完全停止任何事件的事件通知的值，包括*adReason*参数。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
