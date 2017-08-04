---
title: "消息队列任务编辑器 （常规页） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.msgqueuetask.general.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 09368b18-37a5-4321-a173-7cfe5d42d2a2
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 25313cc6decaea073409143e468621a1ed40993c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="message-queue-task-editor-general-page"></a>消息队列任务编辑器（“常规”页）
  可以使用 **“消息队列任务编辑器”** 对话框的 **“常规”** 页，对消息队列任务进行命名和说明，指定消息格式，以及指示任务是发送还是接收消息。  
  
 若要了解此任务，请参阅 [Message Queue Task](../../integration-services/control-flow/message-queue-task.md)。  
  
## <a name="options"></a>选项  
 **名称**  
 为消息队列任务提供唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **Description**  
 键入对消息队列任务的说明。  
  
 **Use2000Format**  
 指示是否使用消息队列（也称为 MSMQ）的 2000 格式。 默认值为 **False**。  
  
 **MSMQConnection**  
 选择一个现有的 MSMQ 连接管理器，或单击\<**新的连接...**> 创建新的连接管理器。  
  
 **相关主题**：[MSMQ 连接管理器](../../integration-services/connection-manager/msmq-connection-manager.md)、[MSMQ 连接管理器编辑器](../../integration-services/connection-manager/msmq-connection-manager-editor.md)  
  
 **消息**  
 指定消息队列任务是发送消息还是接收消息。 如果选择了 **“发送消息”**，则该对话框的左窗格将列出“发送”页；如果选择了 **“接收消息”**，则将列出“接收”页。 默认情况下，此值设置为 **“发送消息”**。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [消息队列任务编辑器 &#40;接收页 &#41;](../../integration-services/control-flow/message-queue-task-editor-receive-page.md)   
 [消息队列任务编辑器 &#40;发送页 &#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
  
