---
title: 处理 ADO 事件 |Microsoft 文档
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
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c8c1bf091c6c41b8700679cce7b696da89e9eff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="handling-ado-events"></a>处理 ADO 事件
ADO 事件模型支持某些可发出的同步和异步 ADO 操作*事件*，或通知，在操作开始之前或之后完成。 事件是实际应用程序中定义的事件处理程序例程的调用。  
  
 如果你提供在操作开始前发生的事件组的处理程序函数或过程，您可以检查或修改已传递给的操作的参数。 因为它已尚未执行，你可以取消该操作，或允许其完成。  
  
 操作完成之后进行的事件是如果以异步方式使用 ADO 尤其重要。 例如，启动应用程序异步[Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)通过执行完成的事件的操作结束时通知操作。  
  
 使用 ADO 事件模型将一些开销添加到你的应用程序，但提供的其他方法与异步操作，例如监视处理更大的灵活性[状态](../../../ado/reference/ado-api/state-property-ado.md)循环对象的属性。  
  
> [!NOTE]
>  若要处理的事件，需要有一个消息泵，或在单线程单元 (STA) 模型中使用 ADO。 通过创建一个隐藏的窗口内部处理 ADO 事件。 ADO 将消息发送到此窗口，当需要激发事件时。 这样做是为了确保事件都发送到的线程中调用**IConnectionPoint::Advise**连接点上。 此体系结构会导致问题时应接收通知的线程不发送窗口消息。 潜在问题包括 ADO 事件未发送到的线程和全局窗口广播超时，并且因为隐藏的 windows 不处理消息可能减缓整个系统。 STA 线程通常具有运行使此问题在 STA 线程上都不清单本身的消息泵。 MTA 线程，但是，通常没有消息泵这样问题将通常清单本身 MTA 线程上。  
  
 本部分包含以下主题。  
  
-   [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [事件类型](../../../ado/guide/data/types-of-events.md)  
  
-   [事件参数](../../../ado/guide/data/event-parameters.md)  
  
-   [事件处理程序的协同工作原理](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [ADO 事件实例化（按语言）](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [通过语言的 ADO 事件实例化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [事件参数](../../../ado/guide/data/event-parameters.md)   
 [事件类型](../../../ado/guide/data/types-of-events.md)
