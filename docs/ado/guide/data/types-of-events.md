---
description: 事件类型
title: 事件类型 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3fa59b0faeb5b1c74ccd4dff3f9d3c274a8f12c6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452679"
---
# <a name="types-of-events"></a>事件类型
事件有两种基本类型。 "将在操作开始之前调用的" 事件 "，通常在其名称中包括" WillChangeRecordset "，例如，" **WillChangeRecordset** "或" **WillConnect**"。 在事件完成后调用的事件通常会在其名称中包括 "Complete" （例如， **RecordChangeComplete** 或 **ConnectComplete**）。 存在异常（如 **InfoMessage** ），但会在关联的操作完成后发生。  
  
## <a name="will-events"></a>将事件  
 在操作开始之前调用的事件处理程序提供了检查或修改操作参数的机会，然后取消操作或允许其完成。 这些事件处理程序例程通常具有形式为<strong>*事件*</strong>的名称。  
  
## <a name="complete-events"></a>完成事件  
 操作完成后调用的事件处理程序可以通知应用程序操作已结束。 当事件处理程序将取消挂起的操作时，也会通知此类事件处理程序。 这些事件处理程序例程通常具有完成的窗体<strong>*事件*</strong>的名称。  
  
 将和完成事件通常成对使用。  
  
## <a name="other-events"></a>其他事件  
 其他事件处理程序（即，其名称不是 " <strong>*事件*</strong> " 或 " <strong>*事件*完成</strong>" 的事件）仅在操作完成后才会被调用。 这些事件为 **Disconnect**、 **EndOfRecordset**和 **InfoMessage**。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [按语言的 ADO 事件实例化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件参数](../../../ado/guide/data/event-parameters.md)   
 [事件处理程序的协同工作原理](../../../ado/guide/data/how-event-handlers-work-together.md)
