---
title: 报表服务器 HTTP 日志 | Microsoft Docs
ms.date: 06/12/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- HTTP [Reporting Services]
ms.assetid: 6cc433b7-165c-4b16-9034-79256dd6735f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7fb733325b09c189221729a3edc0dd12cf33b283
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67140453"
---
# <a name="report-server-http-log"></a>报表服务器 HTTP 日志
  报表服务器 HTTP 日志记录报表服务器所处理的所有 HTTP 请求和响应。 由于请求溢出和超时错误不会到达报表服务器，因此这些错误不会记录在日志文件中。  
  
 默认情况下，不启用 HTTP 日志记录。 若要在安装中使用此功能，必须修改 ReportingServicesService.exe 配置文件。  
  
## <a name="viewing-log-information"></a>查看日志信息  
 该日志为 ASCII 文本文件。 可以使用任何文本编辑器查看该文件。 报表服务器 HTTP 日志文件等同于 IIS 中的 W3C 扩展日志文件，并且使用与其类似的字段，因此可以使用现有的 IIS 日志文件查看器来读取报表服务器 HTTP 日志文件。 下表提供有关 HTTP 日志文件的其他信息：  
  
|||  
|-|-|  
|文件名|默认情况下，文件名为 ReportServerService_HTTP_\<timestamp>.log。 您可以通过在 ReportingServicesService.exe.config 文件中修改 HttpTraceFileName 属性来自定义文件名的前缀。 时间戳基于协调世界时 (UTC)。|  
|文件位置|该文件位于 \Microsoft SQL Server\\*SQL Server Instance>\Reporting Services\LogFiles 中\<* 。|  
|文件格式|该文件是 EN-US 格式。 它是 ASCII 文本文件。|  
|创建和保留文件|当您在配置文件中启用了日志、重新启动服务以及报表服务器处理 HTTP 请求时，会创建 HTTP 日志。 如果配置了相应设置但没有看到日志文件，请打开报表或启动报表服务器应用程序（如 Web 门户），以生成创建日志文件的 HTTP 请求。<br /><br /> 在各服务重新启动并且随后发生对报表服务器的 HTTP 请求时，会创建日志文件的新实例。<br /><br /> 默认情况下，跟踪日志大小限制为 32 MB，并在 14 天后删除。|  
  
## <a name="configuration-settings-for-report-server-http-log"></a>报表服务器 HTTP 日志的配置设置  
 若要配置报表服务器 HTTP 日志，请使用记事本来修改 ReportingServicesService.exe.config 文件。 此配置文件位于 \Program Files\Microsoft SQL Server\MSSQL.n\Reporting Services\ReportServer\Bin 文件夹。  
  
 若要启用 HTTP 服务器，必须将 **http:4** 添加到 ReportingServicesService.exe.config 文件的 RStrace 部分。 所有其他 HTTP 日志文件项都是可选的。 下面的示例包括所有设置，因此您可以将整个内容都粘贴到 RStrace 部分，然后删除您不需要的设置。
  
```  
   <RStrace>  
         <add name="FileName" value="ReportServerService_" />  
         <add name="FileSizeLimitMb" value="32" />  
         <add name="KeepFilesForDays" value="14" />  
         <add name="Prefix" value="tid, time" />  
         <add name="TraceListeners" value="debugwindow, file" />  
         <add name="TraceFileMode" value="unique" />  
         <add name="HttpTraceFileName" value="ReportServerService_HTTP_" />  
         <add name="HttpTraceSwitches" value="date,time,clientip,username,serverip,serverport,host,method,uristem,uriquery,protocolstatus,bytesreceived,timetaken,protocolversion,useragent,cookiereceived,cookiesent,referrer" />  
         <add name="Components" value="all:3,http:4" />  
   </RStrace>  
```  
  
## <a name="log-file-fields"></a>日志文件字段  
 下表对在日志中可用的字段进行了说明： 该字段列表是可配置的；您可以通过 **HTTPTraceSwitches** 配置设置来指定要包括哪些字段。 如果您不指定 **HTTPTraceSwitches** ，则“默认”  列会指定日志文件是否自动包含某个字段。  
  
|字段|说明|默认|  
|-----------|-----------------|-------------|  
|HttpTraceFileName|此值是可选的。 默认值为 ReportServerServiceHTTP_。 如果您想要使用其他文件命名约定（例如，在将日志文件保存到中央位置时要包括服务器名），则可指定不同的值。|是|  
|HTTPTraceSwitches|此值是可选的。 如果指定该字段，则可以逗号分隔的格式配置要在日志文件中使用的字段。|否|  
|Date|活动发生的日期。|否|  
|时间|活动发生的时间。|否|  
|ClientIp|访问报表服务器的客户端的 IP 地址。|是|  
|UserName|访问报表服务器的用户的名称。|否|  
|ServerPort|连接使用的端口号。|否|  
|主机|主机标头的内容。|否|  
|方法|从客户端调用的操作或 SOAP 方法。|是|  
|UriStem|访问的资源。|是|  
|UriQuery|用于访问资源的查询。|否|  
|ProtocolStatus|HTTP 状态代码。|是|  
|BytesReceived|服务器接收的字节数。|否|  
|TimeTaken|从即时 HTTP.SYS 返回请求数据到服务器完成最后一次发送所用的时间（以毫秒计），不包括网络传输时间。|否|  
|ProtocolVersion|客户端使用的协议版本。|否|  
|UserAgent|客户端使用的浏览器类型。|否|  
|CookieReceived|服务器接收的 cookie 的内容。|否|  
|CookieSent|服务器发送的 cookie 的内容。|否|  
|Referrer|客户端以前访问过的站点。|否|  
  
## <a name="see-also"></a>另请参阅  
 [报表服务器服务跟踪日志](../../reporting-services/report-server/report-server-service-trace-log.md)   
 [Reporting Services 日志文件和来源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [错误和事件参考 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  