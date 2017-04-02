---
title: "报表服务器服务跟踪日志 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "日志 [Reporting Services], 跟踪"
  - "跟踪 [Reporting Services]"
  - "系统信息 [Reporting Services]"
  - "版本 [Reporting Services]"
ms.assetid: 2fde08b2-137d-4f4b-88e5-216030216e0d
caps.latest.revision: 52
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 51
---
# 报表服务器服务跟踪日志
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器跟踪日志是 ASCII 文本文件，其中包含有关报表服务器服务操作的详细信息。  文件中的信息包括由报表服务器 Web 服务、Web 门户和后台处理执行的操作。 跟踪日志文件中包括其他日志文件中记录的冗余信息，还包括无法通过其他方式获得的附加信息。 如果要调试包括报表服务器的应用程序或调查已写入事件日志或执行日志中的特定问题，跟踪日志信息非常有用。 例如，排除订阅问题时。  
 
##  <a name="bkmk_view_log"></a> 报表服务器日志文件位于何处？  
 跟踪日志文件是 `ReportServerService_<timestamp>.log` 且位于以下文件夹：  
  
 `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`  
  
 跟踪日志每天进行创建，其中第一个条目发生在午夜（本地时间）之后，并且在每次重新启动该服务时都创建跟踪日志。 时间戳基于协调世界时 (UTC)。 该文件是 EN-US 格式。 默认情况下，跟踪日志大小限制为 32 MB，并在 14 天后删除。  
  
 查看演示使用 Microsoft Power Query 查看 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 日志文件的简短视频。  
  
[![观看演示 power query 和 ssrs 日志文件的视频](../../reporting-services/report-server/media/generic-video-thumbnail.png)](https://technet.microsoft.com/library/sql-server-reporting-services-log-files-and-microsoft-power-query.aspx) [使用 Microsoft Power Query 查看 Reporting Services 日志文件](https://technet.microsoft.com/library/sql-server-reporting-services-log-files-and-microsoft-power-query.aspx)
  
##  <a name="bkmk_trace_configuration_settings"></a> 跟踪配置设置  
 在配置文件 **ReportingServicesrService.exe.config**中管理跟踪日志行为。 可在以下文件夹路径中找到该配置文件：  
  
 `\Program Files\Microsoft SQL Server\MSRS13.<instance name>\Reporting Services\ReportServer\bin`。  
  
 下面的示例演示 **RStrace** 设置的 XML 结构。 **DefaultTraceSwitch** 的值确定添加到日志的信息种类。 除了 **Components** 属性以外，各个配置文件 **RStrace** 的值是相同的。  
  
```  
<system.diagnostics>  
      <switches>  
          <add name="DefaultTraceSwitch" value="3" />  
      </switches>  
</system.diagnostics>  
<RStrace>  
      <add name="FileName" value="ReportServerService_" />  
      <add name="FileSizeLimitMb" value="32" />  
      <add name="KeepFilesForDays" value="14" />  
      <add name="Prefix" value="tid, time" />  
      <add name="TraceListeners" value="file" />  
      <add name="TraceFileMode" value="unique" />  
      <add name="Components" value="all" />  
</RStrace>  
```  
  
 下表提供了有关每个设置的信息。  
  
|设置|Description|值|  
|-------------|-----------------|------------|  
|**RStrace**|指定用于错误和跟踪的命名空间。||  
|**DefaultTraceSwitch**|指定向 ReportServerService 跟踪日志报告的信息的级别。 每个级别都包含所有更低级别（用更小的数字表示）报告的信息。 建议您不要禁用跟踪。|有效值包括：<br /><br /> <br /><br /> 0= 禁用跟踪。 默认情况下，启用 ReportServerService 日志文件。 若要将其关闭，请将跟踪级别设为 0。<br /><br /> 1= 异常和重新启动<br /><br /> 2= 异常、重新启动、警告<br /><br /> 3= 异常、重新启动、警告、状态消息（默认值）<br /><br /> 4= 详细模式|  
|**FileName**|指定日志文件名的第一部分。 该名称的其余部分由 **Prefix** 指定的值完成。||  
|**FileSizeLimitMb**|指定跟踪日志大小的上限。 文件大小的单位为 MB。<br /><br /> 可通过设置跟踪级别（0 到 4）来控制要记录的内容的数量，从而控制文件的大小。 还可以指定要跟踪的组件。 如果在尚未达到 14 天过期时间之前日志文件已达到最大大小，将使用较新的项替换较旧的项。|有效值介于 0 到最大整数之间。 默认值为 32。 如果指定 0 或负数，报表服务器会将该值视为 1。|  
|**KeepFilesForDays**|指定多少天后删除跟踪日志文件。|有效值介于 0 到最大整数之间。 默认值为 14。 如果指定 0 或负数，报表服务器会将该值视为 1。|  
|**Prefix**|指定一个生成的值，该值可将日志实例彼此区分开。|默认情况下，跟踪日志文件名后面将附加时间戳值。 此值设置为“ tid, time ”。 请不要修改此设置。|  
|**TraceListeners**|指定输出跟踪日志内容的目标。 您可以通过使用逗号进行分隔来指定多个目标。|有效值包括：<br /><br /> <br /><br /> DebugWindow<br /><br /> File（默认值）<br /><br /> StdOut|  
|**TraceFileMode**|指定跟踪日志是否包含 24 小时时段内的数据。 每天应当为每个组件设置唯一的跟踪日志。|此值设置为“Unique”（默认值）。 不要修改此值。|  
|**组件类别**|按以下格式指定为其生成跟踪日志信息的组件以及跟踪级别：<br /><br /> \<组件类别>：\<tracelevel><br /><br /> 可以指定所有或部分组件 (**all**、**RunningJobs**、**SemanticQueryEngine**、**SemanticModelGenerator**)。 如果您不想生成特定组件的信息，则可以禁用其跟踪（例如“SemanticModelGenerator:0”）。 请不要禁用 **all**的跟踪。<br /><br /> 如果要查看为每个语义查询生成的 Transact-SQL 语句，则可以设置“SemanticQueryEngine:4”。 Transact-SQL 语句记录到跟踪日志中。 下例说明将 Transact-SQL 语句添加到日志的配置设置：<br /><br /> \<add name="Components" value="all,SemanticQueryEngine:4" />|组件类别可以设置为：<br /><br /> <br /><br /> **All** 用于跟踪未划分为特定类别的所有进程的常规报表服务器活动。<br /><br /> **RunningJobs** 用于跟踪正在进行中的报表或订阅操作。<br /><br /> **SemanticQueryEngine** 用于跟踪用户在基于模型的报表中执行即席数据浏览时处理的语义查询。<br /><br /> **SemanticModelGenerator** 用于跟踪模型生成。<br /><br /> **http** 用于启用报表服务器 HTTP 日志文件。 有关详细信息，请参阅 [Report Server HTTP Log](../../reporting-services/report-server/report-server-http-log.md)。|  
|组件类别的**tracelevel** 值|\<组件类别>：\<tracelevel><br /><br /> <br /><br /> 如果您不对组件追加跟踪级别，将使用为 **DefaultTraceSwitch** 指定的值。 例如，如果指定“all,RunningJobs,SemanticQueryEngine,SemanticModelGenerator”，所有组件将使用默认跟踪级别。|有效的跟踪级别值包括：<br /><br /> <br /><br /> 0= 禁用跟踪<br /><br /> 1= 异常和重新启动<br /><br /> 2= 异常、重新启动、警告<br /><br /> 3= 异常、重新启动、警告、状态消息（默认值）<br /><br /> 4= 详细模式<br /><br /> 报表服务器的默认级别为“all:3”。|  
  
##  <a name="bkmk_add_custom"></a> 添加自定义配置设置以指定转储文件位置  
 可以添加自定义设置来设置 Dr. Watson for Windows 工具用于存储转储文件的位置。 自定义设置为 **Directory**。 下例提供了如何在 **RStrace** 部分中指定此配置设置的说明：  
  
```  
<add name="Directory" value="U:\logs\" />  
```  
  
 有关详细信息，请参阅 [网站上的](http://support.microsoft.com/?kbid=913046) 知识库文章 913046 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
##  <a name="bkmk_log_file_fields"></a> 日志文件字段  
 跟踪日志中包括以下字段：  
  
-   系统信息，包括操作系统、版本、处理器个数和内存。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件和版本信息。  
  
-   记入应用程序日志的事件。  
  
-   报表服务器生成的异常。  
  
-   报表服务器记录的资源不足警告。  
  
-   入站 SOAP 信封和摘要式出站 SOAP 信封。  
  
-   HTTP 标头、堆栈跟踪和调试跟踪信息。  
  
 通过查阅跟踪日志信息，可以确定是否进行了报表传递、谁接收了报表以及进行了多少次传递尝试。 跟踪日志还会记录报表执行活动以及报表处理过程中的有效环境变量。 错误和异常也会记入跟踪日志中。 例如，可能会发现报表超时错误（如 **ThreadAbortExceptions** 项所示）。  

## 先前版本
在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 早期版本中，存在多个跟踪日志文件，每个应用程序一个跟踪日志文件。 以下文件已过时，并且 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本不会再创建它们：
+ ReportServerWebApp_*\<timestamp>*.log
+ ReportServer_*\<timestamp>*.log
+ ReportServerService_main_*\<timestamp>*.log
  
## 另请参阅  
 [Reporting Services 日志文件和来源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [错误和事件参考 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  