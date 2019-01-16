---
title: 类型的事件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EventComplete event [ADO]
- events [ADO], types
- Will events [ADO]
- complete events [ADO]
- WillEvent event [ADO]
ms.assetid: f3327ea0-635a-43d4-bd78-c1674f62f1a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78505f010706a39e5278d50219dd4504e33dd67c
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2019
ms.locfileid: "54254862"
---
# <a name="types-of-events"></a>事件类型
有两种基本类型的事件。 "将事件，"调用操作开始之前，通常包括在其名称中的"将"，例如， **WillChangeRecordset**或**WillConnect**。 通常完成事件后调用的事件名称-中包括"已完成"等**RecordChangeComplete**或**ConnectComplete**。 存在例外-例如**InfoMessage** -但关联的操作完成后，会发生这些问题。  
  
## <a name="will-events"></a>将事件  
 在操作开始为您提供机会来检查或修改操作参数，然后取消操作或允许它完成之前，将调用事件处理程序。 这些事件处理程序例程通常具有窗体的名称<strong>会*事件*</strong>。  
  
## <a name="complete-events"></a>完成事件数  
 操作完成后调用的事件处理程序可以通知操作已结束相关应用程序。 当将事件处理程序取消挂起操作时，此类事件处理程序也会收到通知。 这些事件处理程序例程通常具有窗体的名称<strong>*事件*完成</strong>。  
  
 对通常使用将和完成事件数。  
  
## <a name="other-events"></a>其他事件  
 其他事件处理程序-即，其名称不是窗体的事件<strong>会*事件*</strong>或<strong>*事件*完成</strong>-仅后调用操作完成。 这些事件是**断开连接**， **EndOfRecordset**，并**InfoMessage**。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件实例化的语言](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件参数](../../../ado/guide/data/event-parameters.md)   
 [事件处理程序的协同工作原理](../../../ado/guide/data/how-event-handlers-work-together.md)
