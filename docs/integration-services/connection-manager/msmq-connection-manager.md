---
title: "MSMQ 连接管理器 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.msmqconnectionmanager.f1
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 0e028f9f648acc18d56dc05262adccbbc52f8f7e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="msmq-connection-manager"></a>MSMQ 连接管理器
  MSMQ 连接管理器使包能够连接到使用“消息队列”（也称为 MSMQ）的消息队列。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的消息队列任务使用 MSMQ 连接管理器。  
  
 将 MSMQ 连接管理器添加到包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时解析 MSMQ 连接的连接管理器，同时还会设置该连接管理器的属性，并将该连接管理器添加到包的“连接”集合。 该连接管理器的 **ConnectionManagerType** 属性设置为 **MSMQ**。  
  
 可以按下列方式来配置 MSMQ 连接管理器：  
  
-   提供一个连接字符串。  
  
-   提供要连接的消息队列的路径。  
  
 路径的格式取决于队列的类型，如下表所示。  
  
|队列类型|示例路径|  
|----------------|-----------------|  
|公共|\<计算机名称 >\\< 队列名称\>|  
|Private|\<计算机名称 > \Private$\\< 队列名称\>|  
  
 可以用句点 (.) 代表本地计算机。  
  
## <a name="configuration-of-the-msmq-connection-manager"></a>MSMQ 连接管理器的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [MSMQ 连接管理器编辑器](../../integration-services/connection-manager/msmq-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="msmq-connection-manager-editor"></a>MSMQ 连接管理器编辑器
  可以使用“MSMQ 连接管理器”对话框指定“消息队列”（也称为 MSMQ）消息队列的路径。  
  
 若要了解有关 MSMQ 连接管理器的详细信息，请参阅 [MSMQ Connection Manager](../../integration-services/connection-manager/msmq-connection-manager.md)。  
  
> [!NOTE]  
>  MSMQ 连接管理器支持本地公共队列、本地专用队列和远程公共队列。 它不支持远程专用队列。 有关使用脚本任务的解决方法，请参阅 [Sending to a Remote Private Message Queue with the Script Task](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md)。  
  
### <a name="options"></a>选项  
 **名称**  
 为工作流中的 MSMQ 连接管理器提供唯一的名称。 所提供的名称将在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中显示。  
  
 **描述**  
 描述连接管理器。 最好按照连接管理器的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **路径**  
 键入消息队列的完整路径。 路径的格式取决于队列的类型。  
  
|队列类型|示例路径|  
|----------------|-----------------|  
|公共|\<计算机名称 >\\< 队列名称\>|  
|Private|\<计算机名称 > \Private$\\< 队列名称\>|  
  
 可以用“.”代表本地计算机。  
  
 **测试**  
 在配置 MSMQ 连接管理器之后，单击“测试”确定该连接是否可用。  
  
## <a name="see-also"></a>另請參閱  
 [消息队列任务](../../integration-services/control-flow/message-queue-task.md)   
 [Integration Services &#40;SSIS &#41;连接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  

