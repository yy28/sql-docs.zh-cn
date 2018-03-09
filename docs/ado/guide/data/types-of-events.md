---
title: "类型的事件 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EventComplete event [ADO]
- events [ADO], types
- Will events [ADO]
- complete events [ADO]
- WillEvent event [ADO]
ms.assetid: f3327ea0-635a-43d4-bd78-c1674f62f1a2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 52d78d1a6ae1fc2ccb34ee6b8d810f1ca5ba1c22
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="types-of-events"></a>类型的事件
有两种基本类型的事件。 "将事件，"在其调用操作开始之前，通常在其名称中包含"将"— 例如， **WillChangeRecordset**或**WillConnect**。 事件通常完成后调用的事件在其名称中包含"完成"— 例如， **RecordChangeComplete**或**ConnectComplete**。 存在例外-如**InfoMessage** -但这些关联的操作已完成后，执行。  
  
## <a name="will-events"></a>将事件  
 在操作开始提供机会检查或修改的操作参数，然后取消该操作或允许应用程序完成之前，将调用事件处理程序。 这些事件处理程序例程通常具有窗体的名称 **将*事件 * * *。  
  
## <a name="complete-events"></a>完成事件  
 操作完成后调用的事件处理程序可以通知你的应用程序操作已结束。 当将事件处理程序取消挂起的操作，则也会通知此类事件处理程序。 这些事件处理程序例程通常具有窗体的名称 ***事件 * 完成**。  
  
 对通常用于将和完成的事件。  
  
## <a name="other-events"></a>其他事件  
 其他事件处理程序 — 也就是说，其名称并不属于该窗体的事件**将 * 事件*** 或 ***事件 * 完成**-仅在操作完成后调用。 这些事件是**断开连接**， **EndOfRecordset**，和**InfoMessage**。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [通过语言的 ADO 事件实例化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件参数](../../../ado/guide/data/event-parameters.md)   
 [事件处理程序的协同工作原理](../../../ado/guide/data/how-event-handlers-work-together.md)
