---
title: 事件处理程序是如何协同工作 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a50612e9bd16eafc2afb74c39ba2e5de7285e5a
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271966"
---
# <a name="how-event-handlers-work-together"></a>事件处理程序是如何协同工作
除非在 Visual Basic 中，所有事件处理程序中进行编程**连接**和**记录集**必须实现的事件，而不考虑是否实际处理的所有事件。 你所要做的实现工作量取决于您的编程语言。 有关详细信息，请参阅[ADO 事件实例化语言](../../../ado/guide/data/ado-event-instantiation-by-language.md)。  
  
## <a name="paired-event-handlers"></a>成对的事件处理程序  
 每个将事件处理程序都有一个相关**完成**事件处理程序。 例如，当你的应用程序更改字段的值时，才**WillChangeField**调用事件处理程序。 如果更改是可接受的你的应用程序离开**adStatus**参数保持不变，执行该操作。 操作完成后， **FieldChangeComplete**事件通知您在操作完成后的应用程序。 如果它已成功完成， **adStatus**包含**adStatusOK**; 否则为**adStatus**包含**adStatusErrorsOccurred**和必须检查**错误**对象以确定错误的原因。  
  
 当**WillChangeField**是调用，你可能会确定不应做的更改。 在这种情况下，设置**adStatus**到**adStatusCancel。** 将取消该操作与**FieldChangeComplete**事件接收**adStatus**值**adStatusErrorsOccurred**。 **错误**对象包含**adErrOperationCancelled** ，以便你**FieldChangeComplete**处理程序都知道该操作已取消。 但是，你需要检查的值**adStatus**在更改之前，因为设置的参数**adStatus**到**adStatusCancel**如果该参数已设置不起作用到**adStatusCantDeny**在进入该过程。  
  
 有时，操作可以引发多个事件。 例如，**记录集**对象具有成对的事件**字段**更改和**记录**更改。 你的应用程序的值更改时**字段**、 **WillChangeField**调用事件处理程序。 如果确定，可以继续操作， **WillChangeRecord**事件处理程序也会引发。 如果此处理程序还允许事件后，若要继续，进行更改和**FieldChangeComplete**和**RecordChangeComplete**调用事件处理程序。 在其中调用某一特定操作将事件处理程序的顺序是未定义的因此应避免编写依赖于按特定顺序调用处理程序的代码。  
  
 在实例时引发多个将事件，事件之一可能会取消挂起的操作。 例如，当你的应用程序更改的值时，才**字段**，这两个**WillChangeField**和**WillChangeRecord**通常会调用事件处理程序。 但是，如果第一个事件处理程序中，其关联的取消此操作**完成**与立即调用处理程序**adStatusOperationCancelled**。 永远不会调用第二个处理程序。 如果，但是，第一个事件处理程序允许的事件以继续，将调用其他事件处理程序。 如果它然后取消此操作，同时**完成**事件将调用如前面的示例所示。  
  
## <a name="unpaired-event-handlers"></a>不成对的事件处理程序  
 只要状态传递到该事件不是**adStatusCantDeny**，你可以为任何事件的事件通知通过关闭返回**adStatusUnwantedEvent**中*状态*参数。 例如，当你**完成**第一次，就会调用事件处理程序，你可以返回**adStatusUnwantedEvent**。 你随后仅接收**将**事件。 但是，某些事件可以触发多个原因。 在这种情况下，事件将具有*原因*参数。 当您返回**adStatusUnwantedEvent**，将停止接收该事件仅在该特定原因它们发生时的通知。 换而言之，你可能将对每个可能的原因，无法触发事件收到通知。  
  
 单个**将**事件处理程序在你想要检查将在操作中使用的参数时很有用。 你可以修改这些操作参数或取消该操作。  
  
 或者，将保留**完成**启用事件通知。 当调用第一个将事件处理程序时，返回**adStatusUnwantedEvent**。 你随后仅接收**完成**事件。  
  
 单个**完成**事件处理程序可用于管理异步操作。 每个异步操作的适当**完成**事件。  
  
 例如，它可能需要很长时间才能填充大型[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 如果你的应用程序编写正确，你可以启动`Recordset.Open(...,adAsyncExecute)`操作并继续进行其他处理。 你最终将时收到通知**记录集**由填充**ExecuteComplete**事件。  
  
## <a name="single-event-handlers-and-multiple-objects"></a>单个事件处理程序和多个对象  
 如 Microsoft Visual C++® 编程语言的灵活性使您有一个从多个对象的事件处理程序处理事件。 例如，你可以有一个**断开连接**从多个事件处理程序处理事件**连接**对象。 如果其中一个连接结束，**断开连接**将调用事件处理程序。 你无法判断哪种连接引起该事件，因为事件处理程序对象参数将设置为相应**连接**对象。  
  
> [!NOTE]
>  Visual Basic 中不能使用此技术，因为该语言可以关联的事件处理程序只能有一个对象。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [通过语言的 ADO 事件实例化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件参数](../../../ado/guide/data/event-parameters.md)   
 [事件类型](../../../ado/guide/data/types-of-events.md)
