---
title: 消息队列任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.messagequeuetask.f1
helpviewer_keywords:
- Message Queue task [Integration Services]
- receiving messages
- messages [Integration Services]
- sending messages
ms.assetid: ae1d8fad-6649-4e93-b589-14a32d07da33
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e7857294534f1c3c434f43c302cee8864925d953
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62831474"
---
# <a name="message-queue-task"></a>Message Queue Task
  通过消息队列任务，你可以使用消息队列（也称为 MSMQ）在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包之间发送和接收消息，或将消息发送到由自定义应用程序处理的应用程序队列。 这些消息可以采用简单文本格式、文件格式或变量及其值的格式。  
  
 用消息队列任务可以协调整个企业的运作。 如果目标不可用或繁忙，可以将消息排队供以后发送；例如，该任务可以将要发给销售代表的离线便携式计算机的消息排队，当他们连接到网络时就会收到消息。 可以将消息队列任务用于下列目的：  
  
-   将任务推迟到其他包签入时执行。 例如，消息队列任务在各个零售站点夜间维护完成之后向公司计算机发送消息。 在公司计算机上运行的包含有消息队列任务，每个任务等待来自特定零售站点的消息。 当来自站点的消息到达时，任务便从该站点上载数据。 所有站点都签入完毕之后，包才计算汇总和。  
  
-   将数据文件发送到负责处理这些文件的计算机中。 例如，可以用数据文件消息把餐馆收银机的输出发送到公司的工资系统，在此处提取出有关各服务员小费的数据。  
  
-   在整个企业分发文件。 例如，包可以使用消息队列任务将包文件发送给另一台计算机。 然后，在目标计算机上运行的包可以使用消息队列任务在本地检索并保存该包。  
  
 发送或接收消息时，“消息队列”任务使用以下四种消息类型之一：数据文件、字符串、变量的字符串消息或变量。 仅在接收消息时才能使用针对变量消息类型的字符串消息。  
  
 任务使用 MSMQ 连接管理器连接到消息队列。 有关详细信息，请参阅 [MSMQ 连接管理器](../connection-manager/msmq-connection-manager.md)。 有关消息队列的详细信息，请参阅 [MSDN Library](https://go.microsoft.com/fwlink/?LinkId=7022)。  
  
 消息队列任务要求安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务。 如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导的 **“要安装的组件”** 页或 **“功能选择”** 页上选择安装某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件，将同时安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件的部分子集。 这些组件对特定任务是有用的，但 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 功能将受到限制。 例如， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 选项会安装设计包所需的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件，但不安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务，因此消息队列任务不起作用。 为了确保完整安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，必须在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] “要安装的组件” **页上选择** 。 有关安装和运行“消息队列”任务的详细信息，请参阅 [安装 Integration Services](../install-windows/install-integration-services.md)。  
  
> [!NOTE]  
>  如果将计算机的操作系统配置为 FIPS 模式并且任务使用加密，则“消息队列”任务将无法遵守联邦信息处理标准 (FIPS) 140-2。 如果“消息队列”任务不使用加密，则该任务可以成功运行。  
  
## <a name="message-types"></a>消息类型  
 可以按下列方式配置消息队列任务提供的消息类型：  
  
-   `Data file` 消息指定文件包含消息。 在接收消息时，可以将任务配置为保存文件、覆盖现有文件以及指定该任务可从中接收消息的包。  
  
-   `String` 消息将消息指定为字符串。 在接收消息时，可以将任务配置为比较接收到的字符串和用户定义字符串，并根据对比结果执行操作。 字符串比较可以是完全匹配、区分大小写或不区分大小写，或者使用子字符串。  
  
-   `String message to variable` 将源消息指定为发送到目标变量的字符串。 可以将任务配置为使用完全匹配、不区分大小写或子字符串的比较方式来比较接收到的字符串和用户定义字符串。 这种消息类型只能在任务接收消息时使用。  
  
-   `Variable` 指定消息包含一个或多个变量。 可以将任务配置为指定消息中所包含变量的名称。 在接收消息时，可以将任务配置为指定任务从中接收消息的包和作为消息目标的变量。  
  
## <a name="sending-messages"></a>发送消息  
 配置消息队列任务以发送消息时，可以使用消息队列技术当前支持的加密算法（RC2 和 RC4）之一来加密消息。 与较新的算法相比，这两种加密算法都被视为加密性很弱的算法，但消息队列技术尚不支持较新的算法。 因此，在使用消息队列任务发送消息时，应考虑您的加密需要。  
  
## <a name="receiving-messages"></a>接收消息  
 在接收消息时，可以按下列方式配置消息队列任务：  
  
-   跳过消息，或从队列中删除消息。  
  
-   指定超时。  
  
-   如果出现超时便失败。  
  
-   如果消息存储在 `Data file` 中，则覆盖现有文件。  
  
-   如果消息使用 `Data file message` 类型，则将消息文件另存为其他文件名。  
  
## <a name="custom-logging-messages-available-on-the-message-queue-task"></a>消息队列任务可用的自定义日志记录消息  
 下表列出了消息队列任务的自定义日志项。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../performance/integration-services-ssis-logging.md)和[日志记录的自定义消息](../custom-messages-for-logging.md)。  
  
|日志项|Description|  
|---------------|-----------------|  
|`MSMQAfterOpen`|指示任务已完成打开消息队列的操作。|  
|`MSMQBeforeOpen`|指示任务开始打开消息队列。|  
|`MSMQBeginReceive`|指示任务开始接收消息。|  
|`MSMQBeginSend`|指示任务开始发送消息。|  
|`MSMQEndReceive`|指示任务完成接收消息。|  
|`MSMQEndSend`|指示任务已完成了发送消息的操作。|  
|`MSMQTaskInfo`|提供有关任务的说明性信息。|  
|`MSMQTaskTimeOut`|指示任务已超时。|  
  
## <a name="configuration-of-the-message-queue-task"></a>消息队列任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的信息，请单击以下主题之一：  
  
-   [消息队列任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)  
  
-   [消息队列任务编辑器（“接收”页）](../message-queue-task-editor-receive-page.md)  
  
-   [消息队列任务编辑器（“发送”页）](../message-queue-task-editor-send-page.md)  
  
-   [“表达式”页](../expressions/expressions-page.md)  
  
 有关以编程方式设置这些属性的信息，请参阅开发人员指南中针对 **Microsoft.SqlServer.Dts.Tasks.MessageQueueTask.MessageQueueTask** 类的文档。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请参阅 [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 任务](integration-services-tasks.md)   
 [控制流](control-flow.md)  
  
  
