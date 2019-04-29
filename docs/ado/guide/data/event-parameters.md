---
title: 事件参数 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e44bc264b5fd3e21e35042243ee81f7834c60b2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161641"
---
# <a name="event-parameters"></a>事件参数
每个事件处理程序有一个状态参数，用于控制事件处理程序。 对于完整事件，此参数还用于指示成功或失败的生成事件的操作。 最完整的事件还具有错误参数来提供有关可能发生，任何错误以及一个或多个引用用来执行该操作的 ADO 对象的对象参数的信息。 例如， [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)事件包括对象的参数**命令**，**记录集**，以及**连接**对象与事件关联。 在以下 Microsoft® Visual Basic® 示例中，您可以看到 pCommand、 pRecordset 和 pConnection 对象表示**命令**，**记录集**，和**连接**使用的对象**Execute**方法。  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 除**错误**对象时，相同的参数传递给将事件。 此允许您检查每个对象，将挂起的操作中使用，并确定是否应允许该操作完成。  
  
 某些事件处理程序有*原因*参数，它提供有关事件的发生原因的其他信息。 例如， **WillMove**并**MoveComplete**事件发生的任何一种导航方法原因 (**MoveNext**， **MovePrevious**，依次类推) 能够调用或作为重新查询的结果。  
  
## <a name="status-parameter"></a>状态参数  
 当调用的事件处理程序例程时，*状态*参数设置为以下值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**adStatusOK**|传递给将和完成事件数。 此值表示引发事件已成功完成的操作。|  
|**adStatusErrorsOccurred**|传递给完成事件数。 此值表示引发事件的操作不成功，或将事件已取消该操作。 检查*错误*参数的更多详细信息。|  
|**adStatusCantDeny**|传递给仅将事件。 此值表示将事件不能取消该操作。 必须执行它。|  
  
 如果您确定在将事件的操作应继续中，将保留*状态*参数保持不变。 只要传入的状态参数未设置为**adStatusCantDeny**，但是，您可以通过更改取消挂起操作*状态*到**adStatusCancel**。 与操作关联的完成事件时执行此操作，具有其*状态*参数设置为**adStatusErrorsOccurred**。 **错误**传递给完成事件对象将包含值**adErrOperationCancelled**。  
  
 如果不再想要处理的事件，则可以设置*状态*到**adStatusUnwantedEvent**和你的应用程序将不会再收到该事件的通知。 但请记住，某些事件可以引发多个原因。 在这种情况下，必须指定**adStatusUnwantedEvent**对每个可能的原因。 例如，若要停止接收通知的挂起**RecordChange**事件，必须设置*状态*参数**adStatusUnwantedEvent**为**adRsnAddNew**， **adRsnDelete**， **adRsnUpdate**， **adRsnUndoUpdate**， **adRsnUndoAddNew**，**adRsnUndoDelete**，并**adRsnFirstChange**发生。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|请求此事件处理程序接收任何进一步的通知。|  
|**adStatusCancel**|请求取消将要发生的操作。|  
  
## <a name="error-parameter"></a>错误参数  
 *错误*参数是对 ADO 引用[错误](../../../ado/reference/ado-api/error-object.md)对象。 当*状态*参数设置为**adStatusErrorsOccurred**，则**错误**对象包含有关操作失败的原因的详细信息。 如果与完成的事件关联的将事件已取消该操作，通过设置*状态*参数**adStatusCancel**，则错误对象始终设置为**adErrOperationCancelled**。  
  
## <a name="object-parameter"></a>对象参数  
 每个事件接收一个或多个对象表示在操作中涉及的对象。 例如， **ExecuteComplete**事件接收**命令**对象，**记录集**对象，和一个**连接**对象。  
  
## <a name="reason-parameter"></a>原因参数  
 *原因*参数， *adReason*，提供了有关事件的发生原因的其他信息。 使用事件*adReason*参数可能会被调用多次，即使对于相同的操作，由于其他原因每次。 例如， **WillChangeRecord**正准备执行或撤消插入、 删除或修改记录的操作调用事件处理程序。 如果你想要处理的事件，只有由于特定原因时，您可以使用*adReason*参数来筛选出不感兴趣的出现次数。 例如，如果你想要处理记录更改事件仅在它们发生因为添加一条记录时，您可以使用类似于以下的内容。  
  
```  
' BeginEventExampleVB01  
Private Sub rsTest_WillChangeRecord(ByVal adReason As ADODB.EventReasonEnum, ByVal cRecords As Long, adStatus As ADODB.EventStatusEnum, ByVal pRecordset As ADODB.Recordset)  
   If adReason = adRsnAddNew Then  
       ' Process event  
       '...  
   Else  
       ' Cancel event notification for all  
       ' other possible adReason values.  
       adStatus = adStatusUnwantedEvent  
   End If  
End Sub  
' EndEventExampleVB01  
```  
  
 在这种情况下，通知可能会为每个其他原因。 但是，它会发生一次只能对每个原因。 通知发生一次对每个原因后，将收到一条新记录添加通知。  
  
 与此相反，您需要设置*adStatus*到**adStatusUnwantedEvent**仅一次，以请求的事件处理程序而无需**adReason**参数停止接收事件通知。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件实例化的语言](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件处理程序如何协同工作](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [事件类型](../../../ado/guide/data/types-of-events.md)
