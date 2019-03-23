---
title: 传输错误消息任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfererrormessagestask.f1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: eaefd6e7ae4748505db9bd84601de6166f9d5f98
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388365"
---
# <a name="transfer-error-messages-task"></a>传输错误消息任务
  传输错误消息任务可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间传输一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户定义错误消息。 用户定义的消息是标识符等于或大于 50000 的消息。 标识符小于 50000 的消息是系统错误消息，无法使用传输错误消息任务来传输它。  
  
 传输错误消息任务可以配置为传输所有错误消息，也可以配置为只传输指定的错误消息。 用户定义的错误消息可以多种不同的语言提供，该任务可以配置为只传输选定语言的消息。 对于使用代码页 1033 的 us_english 版本的消息来说，在可以将该消息的其他语言版本传输到目标服务器之前，此消息必须已存在于该服务器上。  
  
 master 数据库中的 sysmessages 表包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的所有错误消息，包括系统错误消息和用户定义的错误消息。  
  
 要传输的用户定义的消息可能已经存在于目标服务器上。 如果标识符和语言相同，则错误消息会被视为重复的错误消息。 传输错误消息任务可以配置为以下列方式处理现有错误消息：  
  
-   覆盖现有错误消息。  
  
-   如果存在重复消息，则该任务失败。  
  
-   跳过重复的错误消息。  
  
 在运行时，传输错误消息任务使用一个或多个 SMO 连接管理器连接到源服务器和目标服务器。 SMO 连接管理器与传输错误消息任务分开进行配置，然后在传输错误消息任务中引用连接管理器。 SMO 连接管理器指定服务器以及在访问该服务器时要使用的身份验证模式。 有关详细信息，请参阅 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)。  
  
 传输错误消息任务支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源和目标。 对于使用哪个版本作为源或目标，没有限制。  
  
## <a name="events"></a>事件  
 该任务引发一个报告已经传输的错误消息数的信息事件。  
  
 传输错误消息任务并不报告错误消息传输的进度，它仅报告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>执行值  
 在该任务的 `ExecutionValue` 属性中定义的执行值返回已传输的错误消息数。 通过将用户定义的变量分配给传输错误消息任务的 `ExecValueVariable` 属性，包中的其他对象就可以访问有关错误消息传输的信息。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)和[在包中使用变量](../use-variables-in-packages.md)。  
  
## <a name="log-entries"></a>日志项  
 传输错误消息任务包括下列自定义日志项：  
  
-   TransferErrorMessagesTaskStartTransferringObjects    此日志项报告传输已经开始。 日志项包括开始时间。  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects   此日志项报告传输已经完成。 日志项包括结束时间。  
  
 此外，`OnInformation` 事件的日志项报告已传输的错误消息数，`OnWarning event`的日志项是为目标服务器上被覆盖的每个错误消息写入的。  
  
## <a name="security-and-permissions"></a>安全性和权限  
 若要新建错误消息，运行该包的用户必须是目标服务器上 sysadmin 的成员或 serveradmin 服务器角色。  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>配置传输错误消息任务  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [传输错误消息任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)  
  
-   [传输错误消息任务编辑器（“消息”页）](../transfer-error-messages-task-editor-messages-page.md)  
  
-   [“表达式”页](../expressions/expressions-page.md)  
  
 有关以编程方式设置这些属性的信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 任务](integration-services-tasks.md)   
 [控制流](control-flow.md)  
  
  
