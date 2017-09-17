---
title: "事件参数 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ae7ee638c8489795df8894be23ef80e63b26f07
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="event-parameters"></a>事件参数
每个事件处理程序有一个控制事件处理程序的状态参数。 对于完整事件，此参数还用于指示成功或失败的生成事件的操作。 最完整事件还具有一个错误参数，以便提供有关可能发生，任何错误以及一个或多个引用用来执行该操作的 ADO 对象的对象参数的信息。 例如， [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)事件包括对象参数**命令**，**记录集**，和**连接**对象与事件关联。 在以下的 Microsoft® Visual Basic® 示例中，你可以看到 pCommand、 pRecordset 和 pConnection 对象表示**命令**，**记录集**，和**连接**程序使用的对象**执行**方法。  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 除**错误**对象，相同的参数传递给将事件。 可以在此检查每个对象，将在挂起的操作中使用，并确定是否应允许该操作完成。  
  
 某些事件处理程序具有*原因*参数，它提供有关事件的发生原因的其他信息。 例如， **WillMove**和**MoveComplete**事件可能会导致任何一种导航方法出现 (**MoveNext**， **MovePrevious**，依次类推) 能够调用或作为重新查询的结果。  
  
## <a name="status-parameter"></a>状态参数  
 当调用的事件处理程序例程时，*状态*参数设置为下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**adStatusOK**|传递给将和完成的事件。 此值意味着引起该事件已成功完成该操作。|  
|**adStatusErrorsOccurred**|传递给完成的事件。 此值表示引起该事件的操作不成功，或将事件取消该操作。 检查*错误*更多详细信息的参数。|  
|**adStatusCantDeny**|传递给仅将事件。 此值表示不能通过将事件取消该操作。 必须执行它。|  
  
 如果你确定应继续该操作，你将事件中，将*状态*参数保持不变。 只要传入的状态参数未设置为**adStatusCantDeny**，但是，可以通过更改取消挂起的操作*状态*到**adStatusCancel**。 执行此操作时，与操作关联的完整事件具有其*状态*参数设置为**adStatusErrorsOccurred**。 **错误**对象传递给完成的事件将包含值**adErrOperationCancelled**。  
  
 如果你不再想要处理的事件，则可以设置*状态*到**adStatusUnwantedEvent**和你的应用程序将不再接收该事件的通知。 但请记住某些事件可以由多个原因。 在这种情况下，必须指定**adStatusUnwantedEvent**对于每个可能的原因。 例如，若要停止接收通知的挂起**RecordChange**事件，必须设置*状态*参数**adStatusUnwantedEvent**为**adRsnAddNew**， **adRsnDelete**， **adRsnUpdate**， **adRsnUndoUpdate**， **adRsnUndoAddNew**，**adRsnUndoDelete**，和**adRsnFirstChange**发生。  
  
|值|Description|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|请求此事件处理程序接收任何进一步的通知。|  
|**adStatusCancel**|请求取消将要发生的操作。|  
  
## <a name="error-parameter"></a>错误参数  
 *错误*参数是对 ADO 的引用[错误](../../../ado/reference/ado-api/error-object.md)对象。 当*状态*参数设置为**adStatusErrorsOccurred**、**错误**对象包含有关操作失败的原因的详细信息。 如果将事件与完整的事件相关联已取消该操作，通过设置*状态*参数**adStatusCancel**，错误对象始终设置为**adErrOperationCancelled**。  
  
## <a name="object-parameter"></a>对象参数  
 每个事件都接收一个或多个对象表示在操作中涉及的对象。 例如， **ExecuteComplete**事件接收**命令**对象，**记录集**对象，和一个**连接**对象。  
  
## <a name="reason-parameter"></a>原因参数  
 *原因*参数， *adReason*，提供有关事件发生原因的其他信息。 事件的*adReason*参数可能被调用多次，即使对于相同的操作，由于其他原因每次。 例如， **WillChangeRecord**即将做或撤消插入、 删除或修改的记录的操作调用事件处理程序。 如果你想要处理的事件，只有由于特定原因时，您可以使用*adReason*参数来筛选出您不感兴趣的匹配项。 例如，如果你想要处理记录更改事件仅当它们发生原因已添加一条记录时，你可以使用类似于以下内容。  
  
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
  
 在这种情况下，通知可能会为每个其他原因。 但是，它将只出现一次对于每个原因。 通知发生一次对于每个原因之后，你将收到通知仅用于添加一条新记录。  
  
 与此相反，你需要设置*adStatus*到**adStatusUnwantedEvent**仅一次，以请求的事件处理程序而无需**adReason**参数停止接收事件发送通知。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [通过语言的 ADO 事件实例化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件处理程序是如何协同工作](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [类型的事件](../../../ado/guide/data/types-of-events.md)
