---
title: MSMQ 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 015488fc30b364b9f82086acb995df3967eb5b10
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52766849"
---
# <a name="msmq-connection-manager"></a>MSMQ 连接管理器
  MSMQ 连接管理器使包能够连接到使用“消息队列”（也称为 MSMQ）的消息队列。  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的消息队列任务使用 MSMQ 连接管理器。  
  
 将 MSMQ 连接管理器添加到包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时解析 MSMQ 连接的连接管理器，同时还会设置该连接管理器的属性，并将该连接管理器添加到包的 `Connections` 集合。 该连接管理器的 `ConnectionManagerType` 属性设置为 `MSMQ`。  
  
 可以按下列方式来配置 MSMQ 连接管理器：  
  
-   提供一个连接字符串。  
  
-   提供要连接的消息队列的路径。  
  
 路径的格式取决于队列的类型，如下表所示。  
  
|队列类型|示例路径|  
|----------------|-----------------|  
|公共|\<computer name>\\<queue name\>|  
|Private|\<computer name>\Private$\\<queue name\>|  
  
 可以用句点 (.) 代表本地计算机。  
  
## <a name="configuration-of-the-msmq-connection-manager"></a>MSMQ 连接管理器的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [MSMQ 连接管理器编辑器](../msmq-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
## <a name="see-also"></a>请参阅  
 [消息队列任务](../control-flow/message-queue-task.md)   
 [Integration Services (SSIS) 连接](integration-services-ssis-connections.md)  
  
  
