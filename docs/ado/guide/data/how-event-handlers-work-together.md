---
title: 事件处理程序如何协同工作 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b744dbd464aedbd9b87d22aa74277787fcc3c7a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925040"
---
# <a name="how-event-handlers-work-together"></a>事件处理程序的协同工作原理
除非在 Visual Basic 中的所有事件处理程序中进行编程**连接**并**记录集**必须实现的事件，无论是否实际处理的所有事件。 您只需实现工作取决于您的编程语言。 有关详细信息，请参阅[ADO 事件实例化的语言](../../../ado/guide/data/ado-event-instantiation-by-language.md)。  
  
## <a name="paired-event-handlers"></a>成对的事件处理程序  
 每个将事件处理程序都有一个关联**完成**事件处理程序。 例如，当你的应用程序更改字段的值时，才**WillChangeField**调用事件处理程序。 如果更改是可接受的你的应用程序会使**adStatus**参数保持不变，并执行该操作。 操作完成后， **FieldChangeComplete**事件通知在操作完成后应用程序。 如果它已成功完成， **adStatus**包含**adStatusOK**; 否则为**adStatus**包含**adStatusErrorsOccurred**和必须检查**错误**对象，以确定错误的原因。  
  
 当**WillChangeField**是调用，你可能会确定不应进行更改。 在这种情况下，设置**adStatus**到**adStatusCancel。** 将取消该操作并**FieldChangeComplete**事件接收**adStatus**的值**adStatusErrorsOccurred**。 **错误**对象包含**adErrOperationCancelled** ，以便你**FieldChangeComplete**处理程序知道该操作已取消。 但是，您需要检查的值**adStatus**参数更改，因为设置之前**adStatus**到**adStatusCancel**如果该参数已设置不起作用向**adStatusCantDeny**在进入该过程。  
  
 有时，操作可以引发多个事件。 例如，**记录集**对象具有成对的事件**字段**更改并**记录**更改。 当你的应用程序更改的值**字段**，则**WillChangeField**调用事件处理程序。 如果确定，可以继续操作，请**WillChangeRecord**事件处理程序也会引发。 如果此处理程序还允许事件继续，进行更改并**FieldChangeComplete**并**RecordChangeComplete**调用事件处理程序。 未定义特定操作将事件处理程序的调用的顺序，因此，应避免编写依赖于按特定顺序调用处理程序的代码。  
  
 在实例中时引发多个将事件，其中一个事件可能会取消挂起的操作。 例如，当你的应用程序更改的值时，才**字段**，这两种**WillChangeField**并**WillChangeRecord**通常会调用事件处理程序。 但是，如果取消此操作是在第一个事件处理程序及其关联**完成**处理程序立即使用调用**adStatusOperationCancelled**。 永远不会调用第二个处理程序。 如果，但是，第一个事件处理程序即可允许事件继续，将调用另一个事件处理程序。 如果它然后取消了操作，同时**完成**事件将调用如前面的示例中所示。  
  
## <a name="unpaired-event-handlers"></a>不成对的事件处理程序  
 只要状态传递到该事件不是**adStatusCantDeny**，可以通过返回来关闭的任何事件的事件通知**adStatusUnwantedEvent**中*状态*参数。 例如，当你**完成**第一次调用事件处理程序，你可以返回**adStatusUnwantedEvent**。 随后将仅收到**将**事件。 但是，某些事件可以触发多个原因。 在这种情况下，该事件将具有*原因*参数。 当您返回**adStatusUnwantedEvent**，将停止接收该事件仅在为此特定它们发生时的通知。 换而言之，将为每个可能的原因可能触发该事件可能会收到通知。  
  
 单一**将**你想要检查将在操作中使用的参数时，事件处理程序会很有用。 您可以修改这些操作参数或取消该操作。  
  
 或者，将保留**完成**启用的事件通知。 当调用第一个将事件处理程序时，返回**adStatusUnwantedEvent**。 随后将仅收到**完成**事件。  
  
 单一**完成**事件处理程序也可用于管理异步操作。 每个异步操作具有相应**完成**事件。  
  
 例如，可能需要很长时间才能填充大型[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 如果你的应用程序编写正确，则可以启动`Recordset.Open(...,adAsyncExecute)`操作并继续进行其他处理。 最终会通知你何时**记录集**由填充**ExecuteComplete**事件。  
  
## <a name="single-event-handlers-and-multiple-objects"></a>单个事件处理程序和多个对象  
 Microsoft Visual C++® 等编程语言的灵活性，可有一个从多个对象的事件处理程序处理事件。 例如，您可以将一个**断开连接**从多个事件处理程序处理事件**连接**对象。 如果其中一个连接结束，则**断开连接**会调用事件处理程序。 您可以告知哪个连接引发此事件，因为事件处理程序对象参数将设置为相应**连接**对象。  
  
> [!NOTE]
>  在 Visual Basic 中不能使用此方法，因为该语言可将事件处理程序只有一个对象相关联。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件实例化的语言](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件参数](../../../ado/guide/data/event-parameters.md)   
 [事件类型](../../../ado/guide/data/types-of-events.md)
