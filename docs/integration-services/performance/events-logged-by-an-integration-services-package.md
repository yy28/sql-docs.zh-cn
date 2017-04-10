---
title: "Integration Services 包记录的事件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "包 [Integration Services], 事件"
  - "事件 [Integration Services], 包"
ms.assetid: 55a0951a-46f3-4f0f-9972-74cec9cc26b7
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Integration Services 包记录的事件
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包将各种事件消息记入 Windows 应用程序事件日志。 包会在包启动时、包停止时和特定问题出现时记录这些消息。  
  
 本主题提供有关包记入应用程序事件日志的常见事件消息的信息。 默认情况下，即使未对包启用日志记录，包也会记录其中某些消息。 但对于其他消息，只有对包启用了日志记录，包才会记录这些消息。 无论包是在默认情况下还是在启用日志记录后记录这些消息，消息的事件源都是 SQLISPackage。  
  
 有关如何运行 SSIS 包的常规信息，请参阅[项目和包的执行](https://msdn.microsoft.com/library/ms141708.aspx)。  
  
 有关如何对运行的包进行故障排除的信息，请参阅[对包执行进行故障排除的工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## 有关包状态的消息  
 运行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包时，包会通常会记录有关包的进度和状态的各种消息。 下表列出了这些消息。  
  
> [!NOTE]  
>  即使未对包启用日志记录，包也会记录下表中的消息。  
  
|事件 ID|符号名称|Text|说明|  
|--------------|-------------------|----------|-----------|  
|12288|DTS_MSG_PACKAGESTART|包“”已开始运行。|包已开始运行。|  
|12289|DTS_MSG_PACKAGESUCCESS|包“”已成功完成。|包已运行成功且不再运行。|  
|12290|DTS_MSG_PACKAGECANCEL|包“%1!s!” 已取消。|包已取消，因此不再运行。|  
|12291|DTS_MSG_PACKAGEFAILURE|包“”已失败。|包无法成功运行，已停止运行。|  
  
 默认情况下，在全新安装中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 配置为不将有关包运行的某些事件记录到应用程序事件日志中。 使用当前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的数据收集器功能时，此设置可防止生成过多的事件日志项。 未记录的事件包括 EventID 12288“包已启动”和 EventID 12289“包已成功完成”。 若要将这些事件记录到应用程序事件日志中，请打开注册表以进行编辑。 然后在注册表中，找到 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS 节点，并将 LogPackageExecutionToEventLog 设置的 DWORD 值从 1 更改为 0。 不过，在升级安装中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 配置为记录这两个事件。 若要禁用记录功能，请将 LogPackageExecutionToEventLog 设置的值从 1 更改为 0。  
  
## 与包日志记录关联的消息  
 如果已对包启用日志记录，应用程序事件日志将是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包中可选的日志记录功能所支持的目标之一。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
 如果已对包启用日志记录而且日志位置为应用程序事件日志，则包将记录与以下信息相关的项：  
  
-   有关包运行时所处的阶段的消息。  
  
-   有关包运行时发生的特定事件的消息。  
  
### 有关包执行阶段的消息  
  
|事件 ID|符号名称|Text|说明|  
|--------------|-------------------|----------|-----------|  
|12544|DTS_MSG_EVENTLOGENTRY|事件名称: %1%r 消息: %9%r 操作员: %2%r 源名称: %3%r 源 ID: %4%r 执行 ID: %5%r 开始时间: %6%r 结束时间: %7%r 数据代码: %8|将包日志记录配置为记入应用程序事件日志时，各种消息都会使用这种通用格式。|  
|12556|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|事件名称: %1%r 消息: %9%r 操作员: %2%r 源名称: %3%r 源 ID: %4%r 执行 ID: %5%r 开始时间: %6%r 结束时间: %7%r 数据代码: %8|包已启动。|  
|12547|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|事件名称: %1%r 消息: %9%r 操作员: %2%r 源名称: %3%r 源 ID: %4%r 执行 ID: %5%r 开始时间: %6%r 结束时间: %7%r 数据代码: %8|对象验证即将开始。|  
|12548|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|事件名称: %1%r 消息: %9%r 操作员: %2%r 源名称: %3%r 源 ID: %4%r 执行 ID: %5%r 开始时间: %6%r 结束时间: %7%r 数据代码: %8|对象验证已完成。|  
|12552|DTS_MSG_EVENTLOGENTRY_PROGRESS|事件名称: %1%r 消息: %9%r 操作员: %2%r 源名称: %3%r 源 ID: %4%r 执行 ID: %5%r 开始时间: %6%r 结束时间: %7%r 数据代码: %8|此通用消息用于报告包的进度。|  
|12546|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|事件名称: %1%r 消息: %9%r 操作员: %2%r 源名称: %3%r 源 ID: %4%r 执行 ID: %5%r 开始时间: %6%r 结束时间: %7%r 数据代码: %8|对象已完成其工作。|  
|12557|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|事件名称: %1%r 消息: %9%r 操作员: %2%r 源名称: %3%r 源 ID: %4%r 执行 ID: %5%r 开始时间: %6%r 结束时间: %7%r 数据代码: %8|包已经完成运行。|  
  
### 有关发生的事件的消息  
 下表仅列出属于事件结果的部分消息。 有关 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用的错误、警告和信息性消息的更全面的列表，请参阅 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)。  
  
|事件 ID|符号名称|Text|说明|  
|--------------|-------------------|----------|-----------|  
|12251|DTS_MSG_EVENTLOGENTRY_TASKFAILED|事件名称: %1%r 消息: %9%r 操作员: %2%r 源名称: %3%r 源 ID: %4%r 执行 ID: %5%r 开始时间: %6%r 结束时间: %7%r 数据代码: %8|任务失败。|  
|12250|DTS_MSG_EVENTLOGENTRY_ERROR|事件名称: %1%r 消息: %9%r 操作员: %2%r 源名称: %3%r 源 ID: %4%r 执行 ID: %5%r 开始时间: %6%r 结束时间: %7%r 数据代码: %8|此消息用于报告产生了一个错误。|  
|12249|DTS_MSG_EVENTLOGENTRY_WARNING|事件名称: %1%r 消息: %9%r 操作员: %2%r 源名称: %3%r 源 ID: %4%r 执行 ID: %5%r 开始时间: %6%r 结束时间: %7%r 数据代码: %8|此消息用于报告产生了一个警告。|  
|12258|DTS_MSG_EVENTLOGENTRY_INFORMATION|事件名称: %1%r 消息: %9%r 操作员: %2%r 源名称: %3%r 源 ID: %4%r 执行 ID: %5%r 开始时间: %6%r 结束时间: %7%r 数据代码: %8|此消息用于报告与错误或警告无关的信息。|  
  
## 相关任务  
 有关如何实时查看日志项的信息，请参阅[在“日志事件”窗口中查看日志项](../../integration-services/performance/view-log-entries-in-the-log-events-window.md)。  
  
## 另请参阅  
 [由 Integration Services 服务记录的事件](../../integration-services/service/events-logged-by-the-integration-services-service.md)  
  
  