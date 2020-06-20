---
title: 日志记录的自定义消息 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], custom
- writing log entries
- SSIS packages, logs
- custom messages for logging [Integration Services]
ms.assetid: 3c74bba9-02b7-4bf5-bad5-19278b680730
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a7fe7d714d93915814b6658409a9f892c28e03b7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84917147"
---
# <a name="custom-messages-for-logging"></a>日志记录的自定义消息
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供了一组丰富的自定义事件，可以用来写入包和很多任务的日志项。 使用这些项可以记录预定义的事件或用户定义的消息，供随后分析时使用，从而将有关执行进度、结果和问题的详细信息保存下来。 例如，可以记录大容量插入的开始和结束时间，从而找出包运行时的性能问题。  
  
 与对包和所有容器及任务可用的标准日志记录事件集相比，自定义日志项是一组不同的项。 您可以根据需要使用自定义日志项来捕获有关包中特定任务的有用信息。 例如，执行 SQL 任务的一个自定义日志项可以在日志中记录该任务所执行的 SQL 语句。  
  
 所有日志项都包括日期和时间信息，包括在包开始和完成时自动写入的日志项。 很多日志事件都会在日志中写入多个项。 这通常发生在事件有不同阶段时。 例如，`ExecuteSQLExecutingQuery` 日志事件写入三项：在任务获得与数据库的连接之后写入一项，在任务开始准备 SQL 语句之后写入另一项，并在执行完 SQL 语句之后再写入一项。  
  
 以下 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象有自定义日志项：  
  
 [包](#Package)  
  
 [大容量插入任务](#BulkInsert)  
  
 [数据流任务](#DataFlow)  
  
 [执行 DTS 2000 任务](#ExecuteDTS200)  
  
 [执行进程任务](#ExecuteProcess)  
  
 [执行 SQL 任务](#ExecuteSQL)  
  
 [文件系统任务](#FileSystem)  
  
 [FTP 任务](#FTP)  
  
 [消息队列任务](#MessageQueue)  
  
 [脚本任务](#Script)  
  
 [发送邮件任务](#SendMail)  
  
 [传输数据库任务](#TransferDatabase)  
  
 [传输错误消息任务](#TransferErrorMessages)  
  
 [传输作业任务](#TransferJobs)  
  
 [传输登录名任务](#TransferLogins)  
  
 [传输主存储过程任务](#TransferMasterStoredProcedures)  
  
 [传输 SQL Server 对象任务](#TransferSQLServerObjects)  
  
 [Web 服务任务](#WebServices)  
  
 [WMI 数据读取器任务](#WMIDataReader)  
  
 [WMI 事件观察器任务](#WMIEventWatcher)  
  
 [XML 任务](#XML)  
  
## <a name="log-entries"></a>日志项  
  
###  <a name="package"></a><a name="Package"></a>软件包  
 下表列出了包的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`PackageStart`|指示包开始运行。<br /><br /> 注意：此日志项自动写入日志。 无法排除它。|  
|`PackageEnd`|指示包已完成。<br /><br /> 注意：此日志项自动写入日志。 无法排除它。|  
|`Diagnostic`|提供影响包执行的系统配置的相关信息，例如，可并发运行的可执行文件数。<br /><br /> `Diagnostic` 日志项还包括调用外部数据访问接口之前和之后的项。 有关详细信息，请参阅 [对包连接进行故障排除的工具](troubleshooting/troubleshooting-tools-for-package-connectivity.md)。|  
  
###  <a name="bulk-insert-task"></a><a name="BulkInsert"></a>大容量插入任务  
 下表列出了大容量插入任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`DTSBulkInsertTaskBegin`|指示大容量插入开始。|  
|`DTSBulkInsertTaskEnd`|指示大容量插入完成。|  
|`DTSBulkInsertTaskInfos`|提供有关任务的说明性信息。|  
  
###  <a name="data-flow-task"></a><a name="DataFlow"></a>数据流任务  
 下表列出了数据流任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`BufferSizeTuning`|指示数据流任务更改了缓冲区的大小。 日志条目描述了大小更改的原因，并列出了临时的新缓冲区大小。|  
|`OnPipelinePostEndOfRowset`|表示组件已经给出它的行集结束信号，该信号由对 `ProcessInput` 方法的最后调用设置。 对于数据流中处理输入的每个组件，都会写入一项。 该项包括组件的名称。|  
|`OnPipelinePostPrimeOutput`|指示组件已经完成它对 `PrimeOutput` 方法的最后一次调用。 取决于数据流，可能写入多个日志条目。 如果组件是源组件，这意味着该组件已经完成对行的处理。|  
|`OnPipelinePreEndOfRowset`|指示组件将要接收它的行集结束信号，该信号由对 `ProcessInput` 方法的最后一次调用设置。 对于数据流中处理输入的每个组件，都会写入一项。 该项包括组件的名称。|  
|`OnPipelinePrePrimeOutput`|指示组件将从 `PrimeOutput` 方法接收它的调用。 取决于数据流，可能写入多个日志条目。|  
|`OnPipelineRowsSent`|报告对 `ProcessInput` 方法的调用为组件输入所提供的行数。 此日志条目包括组件名。|  
|`PipelineBufferLeak`|提供在缓冲区管理器退出之后使缓冲区保持活动状态的任何组件的相关信息。 这意味着缓冲区资源未释放，并且可能导致内存泄漏。 日志条目提供组件的名称和缓冲区的 ID。|  
|`PipelineExecutionPlan`|报告数据流的执行计划。 它提供有关缓冲区将如何发送到组件的信息。 此信息与 PipelineExecutionTrees 项组合，一起描述在任务中所发生的事情。|  
|`PipelineExecutionTrees`|报告数据流中的布局的执行树。 数据流引擎的计划程序使用这些树生成数据流的执行计划。|  
|`PipelineInitialization`|提供有关任务的初始化信息。 此信息包括要用来临时存储 BLOB 数据、默认缓冲区大小和缓冲区行数的目录。 取决于数据流任务的配置，可能写入多个日志条目。|  
  
###  <a name="execute-dts-2000-task"></a><a name="ExecuteDTS200"></a> 执行 DTS 2000 任务  
 下表列出了执行 DTS 2000 任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`ExecuteDTS80PackageTaskBegin`|指示任务开始运行 DTS 2000 包。|  
|`ExecuteDTS80PackageTaskEnd`|指示任务已完成。<br /><br /> 注意：任务结束之后，DTS 2000 包可能继续运行。|  
|`ExecuteDTS80PackageTaskTaskInfo`|提供有关任务的说明性信息。|  
|`ExecuteDTS80PackageTaskTaskResult`|报告该任务所运行的 DTS 2000 包的执行结果。|  
  
###  <a name="execute-process-task"></a><a name="ExecuteProcess"></a>执行进程任务  
 下表列出了执行进程任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|提供有关进程的信息，该进程运行此任务按配置要求要运行的可执行文件。<br /><br /> 写入两个日志条目。 一个日志项包含有关任务所运行的可执行文件的名称和位置的信息，另一个则记录从可执行文件退出的信息。|  
|`ExecuteProcessVariableRouting`|提供有关哪些变量被路由到可执行文件的输入和输出的信息。 将为 stdin（输入）、stdout（输出）和 stderr（错误输出）写入日志条目。|  
  
###  <a name="execute-sql-task"></a><a name="ExecuteSQL"></a>执行 SQL 任务  
 下表介绍了执行 SQL 任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`ExecuteSQLExecutingQuery`|提供有关 SQL 语句的执行阶段的信息。 在任务获得与数据库的连接时、任务开始准备 SQL 语句时以及执行完 SQL 语句之后写入日志项。 准备阶段的日志条目包括任务所使用的 SQL 语句。|  
  
###  <a name="file-system-task"></a><a name="FileSystem"></a>文件系统任务  
 下表介绍了文件系统任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`FileSystemOperation`|报告任务所执行的操作。 在文件系统操作开始时写入日志项，日志项包括有关源和目标的信息。|  
  
###  <a name="ftp-task"></a><a name="FTP"></a>FTP 任务  
 下表列出了 FTP 任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`FTPConnectingToServer`|指示任务已启动与 FTP 服务器的连接。|  
|`FTPOperation`|报告任务所执行的 FTP 操作的开始及其类型。|  
  
###  <a name="message-queue-task"></a><a name="MessageQueue"></a>消息队列任务  
 下表列出了消息队列任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`MSMQAfterOpen`|指示任务已完成打开消息队列的操作。|  
|`MSMQBeforeOpen`|指示任务开始打开消息队列。|  
|`MSMQBeginReceive`|指示任务开始接收消息。|  
|`MSMQBeginSend`|指示任务开始发送消息。|  
|`MSMQEndReceive`|指示任务完成接收消息。|  
|`MSMQEndSend`|指示任务完成发送消息的操作。|  
|`MSMQTaskInfo`|提供有关任务的说明性信息。|  
|`MSMQTaskTimeOut`|指示任务已超时。|  
  
###  <a name="script-task"></a><a name="Script"></a>脚本任务  
 下表介绍了脚本任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`ScriptTaskLogEntry`|报告在脚本中实现日志记录的结果。 在每次调用 `Log` 对象的 `Dts` 方法时将写入日志项。 代码运行时将写入日志项。 有关详细信息，请参阅 [Logging in the Script Task](extending-packages-scripting/task/logging-in-the-script-task.md)。|  
  
###  <a name="send-mail-task"></a><a name="SendMail"></a>发送邮件任务  
 下表列出了发送邮件任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`SendMailTaskBegin`|指示任务开始发送电子邮件。|  
|`SendMailTaskEnd`|指示任务已发送完电子邮件。|  
|`SendMailTaskInfo`|提供有关任务的说明性信息。|  
  
###  <a name="transfer-database-task"></a><a name="TransferDatabase"></a>传输数据库任务  
 下表列出了传输数据库任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`SourceDB`|指定任务所复制的数据库。|  
|`SourceSQLServer`|指定从中复制数据库的计算机。|  
  
###  <a name="transfer-error-messages-task"></a><a name="TransferErrorMessages"></a>传输错误消息任务  
 下表列出了传输错误消息任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`TransferErrorMessagesTaskFinishedTransferringObjects`|指示任务已完成传输错误消息的操作。|  
|`TransferErrorMessagesTaskStartTransferringObjects`|指示任务已开始传输错误消息。|  
  
###  <a name="transfer-jobs-task"></a><a name="TransferJobs"></a>传输作业任务  
 下表列出传输作业任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`TransferJobsTaskFinishedTransferringObjects`|指示任务已完成传输 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理作业。|  
|`TransferJobsTaskStartTransferringObjects`|指示任务已开始传输 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理作业。|  
  
###  <a name="transfer-logins-task"></a><a name="TransferLogins"></a>传输登录名任务  
 下表列出了传输登录名任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`TransferLoginsTaskFinishedTransferringObjects`|指示任务已传输完登录名。|  
|`TransferLoginsTaskStartTransferringObjects`|指示任务已开始传输登录名。|  
  
###  <a name="transfer-master-stored-procedures-task"></a><a name="TransferMasterStoredProcedures"></a>传输主存储过程任务  
 下表列出可传输主存储过程任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`TransferStoredProceduresTaskFinishedTransferringObjects`|指示任务已传输完在 **master** 数据库中存储的用户定义的存储过程。|  
|`TransferStoredProceduresTaskStartTransferringObjects`|指示任务已开始传输 **master** 数据库中存储的用户定义的存储过程。|  
  
###  <a name="transfer-sql-server-objects-task"></a><a name="TransferSQLServerObjects"></a>传输 SQL Server 对象任务  
 下表列出了传输 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 对象任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`TransferSqlServerObjectsTaskFinishedTransferringObjects`|指示任务已完成传输 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库对象。|  
|`TransferSqlServerObjectsTaskStartTransferringObjects`|指示任务已开始传输 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库对象。|  
  
###  <a name="web-services-task"></a><a name="WebServices"></a> Web 服务任务  
 下表列出了可以为 Web 服务任务启用的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`WSTaskBegin`|任务已开始访问 Web 服务。|  
|`WSTaskEnd`|任务已完成 Web 服务方法。|  
|`WSTaskInfo`|有关任务的说明性信息。|  
  
###  <a name="wmi-data-reader-task"></a><a name="WMIDataReader"></a>WMI 数据读取器任务  
 下表列出了 WMI 数据读取器任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`WMIDataReaderGettingWMIData`|指示任务已开始读取 WMI 数据。|  
|`WMIDataReaderOperation`|报告任务所运行的 WQL 查询。|  
  
###  <a name="wmi-event-watcher-task"></a><a name="WMIEventWatcher"></a>WMI 事件观察器任务  
 下表列出了 WMI 事件观察器任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`WMIEventWatcherEventOccurred`|表示发生了任务正在监视的事件。|  
|`WMIEventWatcherTimedout`|指示任务已超时。|  
|`WMIEventWatcherWatchingForWMIEvents`|指示任务已开始执行 WQL 查询。 日志项包括查询。|  
  
###  <a name="xml-task"></a><a name="XML"></a>XML 任务  
 下表介绍了 XML 任务的自定义日志项。  
  
|日志项|说明|  
|---------------|-----------------|  
|`XMLOperation`|提供任务所执行的操作的相关信息|   
  
## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 日志记录](performance/integration-services-ssis-logging.md)  
  
