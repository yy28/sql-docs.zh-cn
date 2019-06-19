---
title: 处理 ADO 事件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 162cac52920b076e4388a74a251cd347137f49cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702016"
---
# <a name="handling-ado-events"></a>处理 ADO 事件
ADO 事件模型支持某些可发出的同步和异步 ADO 操作*事件*，或在操作开始前或后完成的通知。 事件是实际应用程序中定义的事件处理程序例程的调用。  
  
 如果组的操作开始之前发生的事件提供处理程序函数或过程，您可以检查或修改传递给该操作的参数。 因为它已尚未执行，可以取消该操作或允许它完成。  
  
 在操作完成之后发生的事件是以异步方式使用 ADO 尤其重要。 例如，应用程序启动异步[Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)通过执行完整的事件在操作结束时通知操作。  
  
 使用 ADO 事件模型会为你的应用程序增加一些开销，但提供处理异步操作，如监视的其他方法相比更大的灵活性[状态](../../../ado/reference/ado-api/state-property-ado.md)具有一个循环对象的属性。  
  
> [!NOTE]
>  若要处理的事件，需要有一个消息泵，或在单线程单元 (STA) 模型中使用 ADO。 通过创建隐藏的窗口在内部处理 ADO 事件。 当需要激发事件时，ADO 将消息发布给此窗口。 这样做是为了确保事件都发送到的线程中调用**IConnectionPoint::Advise**连接点上。 要接收通知的线程不抽取窗口消息时，此体系结构可能会导致问题。 潜在的问题包括 ADO 事件未传递到线程，并全局窗口广播发生超时，并可能降低整个系统，因为隐藏的 windows 不处理消息。 STA 线程通常有一个运行，因此此问题不显示在 STA 线程上自己的消息泵。 MTA 线程，但是，通常没有消息泵因此该问题将通常表现 MTA 线程上。  
  
 本部分包含以下主题。  
  
-   [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [事件类型](../../../ado/guide/data/types-of-events.md)  
  
-   [事件参数](../../../ado/guide/data/event-parameters.md)  
  
-   [事件处理程序的协同工作原理](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [ADO 事件实例化（按语言）](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件实例化的语言](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [事件参数](../../../ado/guide/data/event-parameters.md)   
 [事件类型](../../../ado/guide/data/types-of-events.md)
