---
title: Integration Services (SSIS) 日志 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], logs
- Windows Event log provider [Integration Services]
- XML File log provider [Integration Services]
- SQL Server Profiler, log provider
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- tasks [Integration Services], logs
- logs [Integration Services], log providers
- Integration Services packages, logs
- log providers [Integration Services]
- packages [Integration Services], logs
- Text File log provider
- SQL Server log provider
ms.assetid: 65e17889-371f-4951-9a7e-9932b2d0dcde
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 30f65b7bfd4563bbc9ada1d615f0d48af225895d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423404"
---
# <a name="integration-services-ssis-logging"></a>Integration Services (SSIS) 日志记录
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含可用来在包、容器和任务中执行日志记录的日志提供程序。 通过日志记录可以捕获有关包的运行时信息，从而帮助您在每次运行包时对其进行审核和故障排除。 例如，日志可以捕获运行包的操作员的姓名以及包开始和完成的时间。  
  
 您可以配置在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器上执行包的过程中出现的日志记录范围。 有关详细信息，请参阅 [在 SSIS 服务器上启用包执行的日志记录](../enable-logging-for-package-execution-on-the-ssis-server.md)。  
  
 在使用 **dtexec** 命令提示实用工具运行包时，还可以包括日志记录。 有关支持日志记录的命令提示参数的详细信息，请参阅 [dtexec Utility](../packages/dtexec-utility.md)。  
  
## <a name="configure-logging-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中配置日志记录  
 日志与包关联，而且可以在包级进行配置。 包中的每项任务或容器都可以将信息记录到任何包日志中。 即使不对包本身启用日志记录，也可以对包中的任务和容器启用日志记录。 例如，您可以对执行 SQL 任务启用日志记录，而不对父包启用日志记录。 包、容器或任务都可以将信息写入多个日志中。 可以只在包上启用日志记录，也可以选择在包所包括的任何单个任务或容器上启用日志记录。  
  
 将日志添加到包时，请选择日志提供程序和日志的位置。 日志提供程序指定日志数据的格式：例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库或文本文件。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含下列日志提供程序：  
  
-   文本文件日志提供程序，将日志项以逗号分隔值 (CSV) 格式写到 ASCII 文本文件。 这种提供程序的默认文件扩展名是 .log。  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 日志提供程序，写入可用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件探查器查看的跟踪。 这种提供程序的默认文件扩展名是 .trc。  
  
    > [!NOTE]  
    >  无法在以 64 位模式运行的包中使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 日志提供程序。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日志提供程序，它将日志项写入 `sysssislog` 数据库中的表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   Windows 事件日志提供程序，将日志项写入本地计算机上 Windows 事件日志中的应用程序日志。  
  
-   XML 文件日志提供程序，将日志文件写入 XML 文件。 这种提供程序的默认文件扩展名是 .xml。  
  
 如果要将日志提供程序添加到包或者以编程方式配置日志记录，可以使用 ProgID 或 ClassID 标识日志提供程序，而不必使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器在 **“配置 SSIS 日志”** 对话框中显示的名称。  
  
 下表列出了用于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所包含日志提供程序的 ProgID 和 ClassID，以及日志提供程序写入的日志的位置。  
  
|日志提供程序|ProgID|ClassID|位置|  
|------------------|------------|-------------|--------------|  
|文本文件|DTS.LogProviderTextFile|{0A039101-ACC1-4E06-943F-279948323883}|日志提供程序使用的文件连接管理器指定此文本文件的路径。|  
|SQL Server Profiler|DTS.LogProviderSQLProfiler|{E93F6300-AE0C-4916-A7BF-A8D0CE12C77A}|日志提供程序使用的文件连接管理器指定 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]所使用的文件的路径。|  
|SQL Server|DTS.LogProviderSQLServer|{94150B25-6AEB-4C0D-996D-D37D1C4FDEDA}|日志提供程序使用的 OLE DB 连接管理器指定包含存储日志项的 sysssislog 表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。|  
|Windows 事件日志|DTS.LogProviderEventLog|{071CC8EB-C343-4CFF-8D58-564B92FCA3CF}|Windows 事件查看器中的应用程序日志包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 日志信息。|  
|XML 文件|DTS.LogProviderXMLFile|{440945A4-2A22-4F19-B577-EAF5FDDC5F7A}|日志提供程序使用的文件连接管理器指定 XML 文件的路径。|  
  
 也可以创建自定义日志提供程序。 有关详细信息，请参阅 [Creating a Custom Log Provider](../extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)。  
  
 包中的日志提供程序是该包的日志提供程序集合的成员。 在使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器创建包并实现日志记录时，您可以在 **设计器的** “包资源管理器” **选项卡上的** “日志提供程序” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 文件夹中看到集合成员列表。  
  
 请提供日志提供程序的名称和说明，并指定日志提供程序使用的连接管理器，以配置日志提供程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日志提供程序使用 OLE DB 连接管理器。 文本文件、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]和 XML 文件日志提供程序全都使用文件连接管理器。 Windows 事件日志提供程序不使用连接管理器，因为它直接写入 Windows 事件日志。 有关详细信息，请参阅 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md) 和 [File Connection Manager](../connection-manager/file-connection-manager.md)。  
  
### <a name="logging-customization"></a>自定义日志记录  
 为了自定义事件或自定义消息的日志记录， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了要包括在日志项中的常用记录信息的架构。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 日志架构定义您可以记录的信息。 您可以从日志架构中为每个日志项选择元素。  
  
 包及其容器和任务不必记录相同的信息，同一包或容器内的任务可以记录不同的信息。 例如，包可以在包启动时记录操作员信息，一个任务可以记录任务失败的原因，而另一个任务可以在出现错误时记录信息。 如果包及其容器和任务使用多个日志，则相同信息会写入所有日志中。  
  
 通过指定要记录的事件以及要为每个事件记录的信息，您可以选择满足自己需求的日志记录级别。 您可能会发现一些事件提供的信息更为有用。 例如，对于 **PreExecute** 事件，您希望仅记录计算机名和操作员姓名，而对于 **Error** 事件，您希望记录所有可用的信息。  
  
 若要防止日志文件占用大量的磁盘空间或者避免过多的日志记录（这可能会降低性能），可以通过选择记录特定的事件和信息项来限制日志记录。 例如，您可以将日志配置为仅捕获每个错误的日期和计算机名。  
  
 在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中，您可以使用 **“配置 SSIS 日志”** 对话框来定义日志记录选项。  
  
#### <a name="log-schema"></a>日志架构  
 下表介绍了日志架构中的元素：  
  
|元素|说明|  
|-------------|-----------------|  
|Computer|发生日志事件的计算机的名称。|  
|操作员|启动包的用户的标识。|  
|SourceName|发生日志事件的容器或任务的名称。|  
|SourceID|发生日志事件的包、 For 循环容器、Foreach 循环容器、序列容器或任务的唯一标识符。|  
|ExecutionID|包执行实例的 GUID。<br /><br /> 注意：运行单个包可能会创建具有不同的 ExecutionID 元素的值的日志条目。 例如，当在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中运行包时，验证阶段可能会创建 ExecutionID 元素与 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]对应的日志项。 但是，执行阶段可能会创建 ExecutionID 元素与 dtshost.exe 对应的日志项。 再比如，当运行包含“执行包”任务的包时，这些任务中的每个任务都会运行子包。 这些子包创建的日志项所具有的 ExecutionID 元素可能不同于父包创建的日志项。|  
|MessageText|与日志项关联的消息。|  
|DataBytes|日志项特定的字节数组。 此字段的意义因日志项的不同而不同。|  
  
 下表介绍日志架构中三个附加元素，这些元素在 **“配置 SSIS 日志”** 对话框的 **“详细信息”** 选项卡中不可用。  
  
|元素|说明|  
|-------------|-----------------|  
|StartTime|容器或任务开始运行的时间。|  
|EndTime|容器或任务停止运行的时间。|  
|DataCode|可选整数值通常包含 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 枚举值，该枚举值指示运行该容器或任务的结果：<br /><br /> 0 – 成功<br /><br /> 1 - 失败<br /><br /> 2 – 已完成<br /><br /> 3 – 已取消|  
  
##### <a name="log-entries"></a>日志项  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支持预定义事件的日志项，并提供了可用于很多 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象的自定义日志项。 **设计器中的** “配置 SSIS 日志” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 对话框列出了这些事件和自定义日志项。  
  
 下表描述了可以在发生运行时事件时启用日志项写入功能的预定义事件。 这些日志项将应用到可执行文件、包以及包中的任务和容器。 日志项的名称与引发并导致写入日志项的运行时事件的名称相同。  
  
|事件|说明|  
|------------|-----------------|  
|**OnError**|出现错误时写入日志项。|  
|**OnExecStatusChanged**|在提示期间挂起或恢复任务（而非容器时），写入日志项。|  
|**OnInformation**|在验证和执行可执行文件的过程中写入报告信息的日志项。|  
|**OnPostExecute**|在可执行文件运行完成后立即写入日志项。|  
|**OnPostValidate**|在可执行文件的验证完成时写入日志项。|  
|**OnPreExecute**|在可执行文件即将运行前写入日志项。|  
|**OnPreValidate**|可执行文件的验证开始时写入日志项。|  
|**OnProgress**|在可执行文件的进度可度量时写入日志项。|  
|**OnQueryCancel**|在任务处理过程中可以取消执行的任何时刻写入日志项。|  
|**OnTaskFailed**|在任务失败时写入日志项。|  
|**OnVariableValueChanged**|在变量的值更改时写入日志项。|  
|**OnWarning**|在出现警告时写入日志项。|  
|**PipelineComponentTime**|对于每个数据流组件，为验证和执行的每个阶段写入日志项。 该日志条目为每个阶段指定处理时间。|  
|**诊断**|写入提供诊断信息的日志项。<br /><br /> 例如，您可以在每次调用外部数据访问接口之前和之后记录消息。 有关详细信息，请参阅 [包执行的疑难解答工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。|  
  
 包和很多任务都有可以启用日志记录功能的自定义日志项。 例如，发送邮件任务提供了 **SendMailTaskBegin** 自定义日志项，该日志项在发送邮件任务开始运行时（但在发送电子邮件消息之前）记录信息。 有关详细信息，请参阅[日志记录的自定义消息](../custom-messages-for-logging.md)。  
  
### <a name="differentiating-package-copies"></a>区分包副本  
 日志数据包括日志项所属的包的名称和 GUID。 如果通过复制现有包而创建了新的包，则现有包的名称和 GUID 也会被复制。 结果，可能有两个包具有相同的 GUID 和名称，这将使您难以区分日志数据中的包。  
  
 若要消除这种不明确性，应当更新新包的名称和 GUID。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，可以在 `ID` 属性中重新生成 GUID，并在“属性”窗口中更新 `Name` 属性的值。 还可以通过编程或使用 **dtutil** 命令提示符工具来更改 GUID 和名称。 有关详细信息，请参阅 [设置包属性](../set-package-properties.md) 和 [dtutil 实用工具](../dtutil-utility.md)。  
  
### <a name="parent-logging-options"></a>父日志记录选项  
 通常，任务以及 For 循环、Foreach 循环和序列容器的日志记录选项与包或父容器的日志记录选项匹配。 在这种情况下，您可以将它们配置为继承其父容器的日志记录选项。 例如，在包括执行 SQL 任务的 For 循环容器中，执行 SQL 任务可以使用已对 For 循环容器设置的日志记录选项。 若要使用父日志记录选项，可以将容器的 LoggingMode 属性设置为 **UseParentSetting**。 可以在 **的** “属性” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 窗口中设置此属性，也可以通过 **设计器中的** “配置 SSIS 日志” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 对话框设置此属性。  
  
### <a name="logging-templates"></a>日志记录模板  
 在 **“配置 SSIS 日志”** 对话框中，还可以创建经常使用的日志记录配置并将其保存为模板，然后在多个包中使用这些模板。 这样便于对多个包应用一致的日志记录策略，以及通过更新并应用模板来修改包的日志设置。 这些模板存储为 XML 文件。  
  
 **使用“配置 SSIS 日志”对话框配置日志记录**  
  
1.  为包及其任务启用日志记录。 可以在包级、容器级以及任务级进行日志记录。 可以为包、容器和任务指定不同的日志。  
  
2.  选择日志提供程序并为包添加日志。 可以仅在包级创建日志，任务或容器必须使用为包创建的日志之一。 每个日志都与下列某个日志提供程序关联：文本文件、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Windows 事件日志或 XML 文件。 有关详细信息，请参阅 [在 SQL Server Data Tools 中启用包日志记录](../enable-package-logging-in-sql-server-data-tools.md)。  
  
3.  选择要在日志中捕获的事件以及每个事件的日志架构信息。 有关详细信息，请参阅 [使用保存的配置文件配置日志记录](../configure-logging-by-using-a-saved-configuration-file.md)。  
  
### <a name="configuration-of-log-provider"></a>日志提供程序的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 作为在包中实现日志记录的一个步骤来创建和配置日志提供程序。 有关详细信息，请参阅[Integration Services 日志记录](integration-services-ssis-logging.md)。  
  
 创建日志提供程序后，可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的“属性”窗口中查看和修改其属性。  
  
 有关如何以编程方式设置这些属性的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 类的文档。  
  
### <a name="logging-for-data-flow-tasks"></a>数据流任务的日志记录  
 数据流任务提供了许多可用于监视和调整性能的自定义日志项。 例如，您可以监视可能会导致内存泄漏的组件，或者跟踪特定组件运行所用的时间。 有关这些自定义日志项的列表和日志记录输出示例，请参阅 [Data Flow Task](../control-flow/data-flow-task.md)。  
  
#### <a name="use-the-pipelinecomponenttime-event"></a>使用 PipelineComponentTime 事件  
 最有用的自定义日志项可能是 PipelineComponentTime 事件。 该日志项报告数据流中的每个组件执行五个主要处理步骤中的每个步骤所用的毫秒数。 下表说明了这些处理步骤。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 开发人员会将这些步骤标识为 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>。  
  
|步骤|说明|  
|----------|-----------------|  
|验证|该组件查看有效的属性值和配置设置。|  
|PreExecute|该组件在开始处理数据行之前执行一次性处理。|  
|PostExecute|该组件在处理所有数据行之后执行一次性处理。|  
|ProcessInput|转换或目标组件处理由上游源或转换传递的传入数据行。|  
|PrimeOutput|源或转换组件填充数据缓冲区，以传递给下游转换或目标组件。|  
  
 启用 PipelineComponentTime 事件时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将针对每个组件执行的各处理步骤记录一则消息。 以下日志项显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CalculatedColumns 包示例记录的消息的子集。  
  
 `The component "Calculate LineItemTotalCost" (3522) spent 356 milliseconds in ProcessInput.`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 79 milliseconds in ProcessInput.`  
  
 `The component "Calculate Average Cost" (3662) spent 16 milliseconds in ProcessInput.`  
  
 `The component "Sort by ProductID" (3717) spent 125 milliseconds in ProcessInput.`  
  
 `The component "Load Data" (3773) spent 0 milliseconds in ProcessInput.`  
  
 `The component "Extract Data" (3869) spent 688 milliseconds in PrimeOutput filling buffers on output "OLE DB Source Output" (3879).`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 141 milliseconds in PrimeOutput filling buffers on output "Aggregate Output 1" (3621).`  
  
 `The component "Sort by ProductID" (3717) spent 16 milliseconds in PrimeOutput filling buffers on output "Sort Output" (3719).`  
  
 下列日志项显示数据流任务在下列步骤中消耗了大多数时间，如下所示（按降序排序）：  
  
-   名为“Extract Data”的 OLE DB 源在加载数据期间耗时 688 毫秒 加载数据。  
  
-   名为“Calculate LineItemTotalCost”的派生列转换 在对传入行执行计算期间耗时 356 毫秒。  
  
-   名为“Sum Quantity and LineItemTotalCost”的聚合转换在执行计算和将数据传递到下一转换期间共耗时 220 毫秒，其中有 141 毫秒用于 PrimeOutput，有 79 毫秒用于 ProcessInput。  
  
## <a name="related-tasks"></a>Related Tasks  
 下面的列表包含一些链接，这些链接指向的主题说明如何执行与日志记录功能相关的任务。  
  
-   [“配置 SSIS 日志”对话框](../configure-ssis-logs-dialog-box.md)  
  
-   [在 SQL Server Data Tools 中启用包日志记录](../enable-package-logging-in-sql-server-data-tools.md)  
  
-   [在 SSIS 服务器上启用包执行的日志记录](../enable-logging-for-package-execution-on-the-ssis-server.md)  
  
-   [在“日志事件”窗口中查看日志项](../view-log-entries-in-the-log-events-window.md)  
  
## <a name="related-content"></a>相关内容  
 [用于完整和详细日志记录的 DTLoggedExec 工具（CodePlex 项目）](https://go.microsoft.com/fwlink/?LinkId=150579)  
  
## <a name="see-also"></a>另请参阅  
 [在“日志事件”窗口中查看日志项](../view-log-entries-in-the-log-events-window.md)  
  
  
