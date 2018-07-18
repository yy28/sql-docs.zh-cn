---
title: 包执行的疑难解答工具 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: f18d6ff6-e881-444c-a399-730b52130e7c
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 88a5fb5fbac36bfa7dc0eb6d7f3495c9306c8513
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403489"
---
# <a name="troubleshooting-tools-for-package-execution"></a>对包执行进行故障排除的工具
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括可用于在包完成和部署以后的执行过程中进行故障排除的功能和工具。  
  
 在设计时， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供了用于暂停包的执行的断点、“进度”窗口和用于在数据通过数据流时查看数据的数据查看器。 但是，这些功能在包部署后运行包时不再可用。 用于排除已部署包故障的主要技术如下：  
  
-   使用事件处理程序捕获和处理包错误。  
  
-   使用错误输出捕获错误数据。  
  
-   使用日志记录跟踪包的执行步骤。  
  
 还可以使用下列技巧和技术避免正在运行的包的问题  
  
-   **使用事务帮助确保数据的完整性**。 有关详细信息，请参阅 [Integration Services 事务](../../integration-services/integration-services-transactions.md)。  
  
-   **使用检查点从故障点重新启动包**。 有关详细信息，请参阅 [通过使用检查点重新启动包](../../integration-services/packages/restart-packages-by-using-checkpoints.md)。  
  
## <a name="catch-and-handle-package-errors-by-using-event-handlers"></a>使用事件处理程序捕获和处理包错误  
 通过使用事件处理程序，您可以响应许多由包和包中的对象引发的事件。  
  
-   **创建 OnError 事件的事件处理程序**。 在事件处理程序中，您可以使用发送邮件任务将故障通知给管理员，使用脚本任务和自定义逻辑获取用于故障排除的系统信息或者清除临时资源或不完整的输出。 有关详细信息，请参阅 [Integration Services (SSIS) 事件处理程序](../../integration-services/integration-services-ssis-event-handlers.md)。  
  
## <a name="troubleshoot-bad-data-by-using-error-outputs"></a>使用错误输出对错误数据进行故障排除  
 您可以使用对许多数据流组件可用的错误输出将包含错误的行定向到单独的目标中，供以后分析。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。  
  
-   **使用错误输出捕获错误数据**。 将包含错误的行发送到单独的目标（如错误表或文本文件）。 错误输出自动添加两个数值列（包含导致该行被拒绝的错误的编号）以及发生该错误的列的 ID。  
  
-   **向错误输出添加易于理解的信息**。 除了由错误输出提供的两个数字标识符外，你还可以添加错误消息和列名称以便更容易分析错误输出。 有关如何通过使用脚本添加这两个附加列的示例，请参阅 [Enhancing an Error Output with the Script Component](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md)。  
  
-   **或者，通过记录 DiagnosticEx 事件获取列名称**。 此事件将数据流沿袭映射写入到日志中。 然后就可以使用由错误输出捕获的列标识符来查找此沿袭映射中的列名称。  有关详细信息，请参阅[数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。  
  
     **DiagnosticEx** 的消息列的值是 XML 文本。 若要查看包执行的消息文本，请查询 [catalog.operation_messages（SSISDB 数据库）](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)视图。 请注意，为了缩减日志大小， **DiagnosticEx** 事件不在其 XML 输出中保留空白。 若要提高可读性，请将日志复制到支持 XML 格式和语法突出显示的 XML 编辑器中 - 例如 Visual Studio 中的 XML 编辑器。  
  
## <a name="troubleshoot-package-execution-by-using-operations-reports"></a>使用操作报告对包执行进行故障排除  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供标准操作报告，帮助您监视部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。 这些包报告有助于您查看包状态和历史记录，并根据需要确定执行失败的原因。  
  
 有关详细信息，请参阅 [Troubleshooting Reports for Package Execution](../../integration-services/troubleshooting/troubleshooting-reports-for-package-execution.md)。  
  
## <a name="troubleshoot-package-execution-by-using-ssisdb-views"></a>使用 SSISDB 视图对包执行进行故障排除  
 提供了一些 SSISDB 数据库视图，您可以查询它们来监视包执行和其他操作信息。 有关详细信息，请参阅 [监视包运行和其他操作](../../integration-services/performance/monitor-running-packages-and-other-operations.md)。  
  
## <a name="troubleshoot-package-execution-by-using-logging"></a>使用日志记录对包执行进行故障排除  
 通过启用日志记录，您可以跟踪正在运行的包中所发生的大部分问题。 日志提供程序捕获有关指定事件的信息供以后分析，并且以数据库表、平面文件、XML 文件或支持的其他输出格式保存该信息。  
  
-   **启用日志记录**。 您可以只选择所要捕获的事件以及只选择所要捕获的信息项，以修改日志记录输出。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../performance/integration-services-ssis-logging.md)。  
  
-   **选择包的“诊断”事件对访问接口问题进行故障排除。** 一些日志记录消息可以帮助您对包与外部数据源的交互情况进行故障排除。 有关详细信息，请参阅 [Troubleshooting Tools Package Connectivity](troubleshooting-tools-for-package-connectivity.md)。  
  
-   **增强默认日志记录输出**。 通常，每次该包运行时日志记录都会向日志记录目标中追加行。 虽然日志记录输出的每一行都使用包的名称和唯一标识符来标识包，也通过唯一的 ExecutionID 来标识包的执行，但单一列表中的大量日志记录输出会使分析变得困难。  
  
     建议采用下列方法增强默认日志记录输出并使其更容易生成报告：  
  
    1.  **创建记录包的每次执行情况的父表**。 此父表只有一行用于包的每次执行，并使用 ExecutionID 链接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 日志记录表中的子记录。 您可以在每个包的开始使用一个执行 SQL 任务创建此新行并记录开始时间。 然后您可以在包的结尾使用另一个执行 SQL 任务，用结束时间、持续时间和状态来更新该行。  
  
    2.  **将审核信息添加到数据流**。 您可以使用审核转换将有关创建或修改每一行的包执行的信息添加到数据流的行中。 审核转换可以提供九条信息，包括 PackageName 和 ExecutionInstanceGUID。 有关详细信息，请参阅 [Audit Transformation](../../integration-services/data-flow/transformations/audit-transformation.md)。 如果您希望在每一行中包括自定义信息以便审核，可以使用派生列转换将此信息添加到数据流的行中。 有关详细信息，请参阅 [派生列转换](../../integration-services/data-flow/transformations/derived-column-transformation.md)。  
  
    3.  **考虑捕获行计数数据**。 考虑另行创建一个表，用于存储行计数信息。其中，每个包执行实例均由其 ExecutionID 标识。 使用行计数转换在数据流的关键点将行计数保存到一系列变量中。 数据流结束后，请使用执行 SQL 任务将该系列值插入到表的行中，供以后分析和报告。  
  
     有关此方法的详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 白皮书 [Project REAL: Business Intelligence ETL Design Practices](http://go.microsoft.com/fwlink/?LinkId=96602)（Project REAL：Business Intelligence ETL 设计实践）中的 "ETL Auditing and Logging"（ETL 审核和日志记录）一节。  
  
## <a name="troubleshoot-package-execution-by-using-debug-dump-files"></a>使用调试转储文件对包执行进行故障排除  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，可以创建提供包执行信息的调试转储文件。 有关详细信息，请参阅 [生成包执行的转储文件](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)。  
  
## <a name="troubleshoot-run-time-validation-issues"></a>针对运行时验证问题进行故障排除  
 有时在包中前一个任务执行完成之前，您也许不能连接到数据源，或者无法验证包的某些部分。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括以下功能，可帮助您避免由这些情况导致的验证错误：  
  
-   **配置加载包时无效包元素的 DelayValidation 属性**。 您可以将具有无效配置的包元素的 **DelayValidation** 设置为 **True** ，以防止包加载时的验证错误。 例如，可以使用只有在运行时通过执行 SQL 任务创建才存在的目标表来执行数据流任务。 可以在包级或包中的各个任务和容器级启用 **DelayValidation** 属性。  
  
     可以对数据流任务设置 **DelayValidation** 属性，但不能对单个数据流组件设置该属性。 可以通过将单个数据流组件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> 属性设置为 **false**。 但是，当此属性的值为 **false**时，该组件不能识别外部数据源的元数据的更改。 设置为 **true**时， <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> 属性可帮助避免数据库中由于锁定导致的阻塞问题，特别是在包使用事务时。  
  
## <a name="troubleshoot-run-time-permissions-issues"></a>运行时权限问题的故障排除  
 如果您在尝试使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理运行已部署的包时遇到错误，则代理所使用的帐户可能不具备必需的权限。 有关如何对从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业运行的包进行故障排除的信息，请参阅 [An SSIS package does not run when you call the SSIS package from a SQL Server Agent job step](http://support.microsoft.com/kb/918760)（从 SQL Server 代理作业步骤调用 SSIS 包时 SSIS 包不运行）。 有关如何从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业运行包的详细信息，请参阅 [包的 SQL Server 代理作业](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)。  
  
 若要连接到 Excel 或 Access 数据源， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理要求帐户具有在 TEMP 和 TMP 环境变量所指定的在文件夹中读取、写入、创建和删除临时文件的权限。  
  
## <a name="troubleshoot-64-bit-issues"></a>64 位问题的故障排除  
  
-   **部分数据访问接口在 64 位平台上不可用**。 尤其是，需要连接到 Excel 或 Access 数据源的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB 访问接口在 64 位版本中不可用。  
  
## <a name="troubleshoot-errors-without-a-description"></a>无说明错误的故障排除  
 如果遇到了没有附带说明的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 错误，您可以根据其错误号在 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md) 中查找错误来找到说明。 目前该列表中不包括故障排除信息。  
  
## <a name="related-tasks"></a>Related Tasks  
 [调试数据流](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
## <a name="related-content"></a>相关内容  
 dougbert.com 上的博客文章： [向错误输出中添加错误列名](http://go.microsoft.com/fwlink/?LinkId=261546)。  
