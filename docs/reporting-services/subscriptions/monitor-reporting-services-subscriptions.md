---
title: "监视 Reporting Services 订阅 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "订阅 [Reporting Services], 非活动"
  - "订阅 [Reporting Services], 状态"
  - "监视 [Reporting Services], 订阅"
  - "状态信息 [Reporting Services]"
  - "不活动的订阅 [Reporting Services]"
ms.assetid: 054c4a87-60bf-4556-9a8c-8b2d77a534e6
caps.latest.revision: 36
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 36
---
# 监视 Reporting Services 订阅
  你可以从用户界面、Windows PowerShell 或日志文件监视 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 订阅。 可用于监视的选项取决于你正在运行的报表服务器的模式。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
 **本主题内容：**  
  
-   [本机模式用户界面](#bkmk_native_mode)  
  
-   [SharePoint 模式](#bkmk_sharepoint_mode)  
  
-   [使用 PowerShell 监视订阅](#bkmk_use_powershell)  
  
-   [管理不活动的订阅](#bkmk_manage_inactive)  
  
##  <a name="bkmk_native_mode"></a> 本机模式用户界面  
 单个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 用户可以使用  “我的订阅”页面或报表管理器中的  “订阅”选项卡来监视订阅状态。 “订阅”页中包括指示订阅最后运行的时间和订阅状态的列。 如果已安排订阅处理计划，则将会更新状态消息。 如果从未引发触发器（例如，从未刷新报表执行快照或计划从未运行），则不会更新状态消息。  
  
 下表描述了  “状态”列的可能的值。  
  
|状态|Description|  
|------------|-----------------|  
|新建订阅|在您首次创建订阅时显示。|  
|Inactive|无法处理订阅时显示。 有关详细信息，请参阅本主题后面的“管理不活动订阅”部分。|  
|已完成: 已处理 \<*number*> 个，共 \<*number*> 个；\<*number*> 个错误。|显示数据驱动订阅执行的状态；此消息来自计划和传递处理器。|  
|\<已处理 *number*> 个|计划和传递处理器成功传递或不再试图传递的通知数。 当数据驱动传递完成后，已处理通知数应等于已生成通知的总数。|  
|\<总计 *number*> 个|最后一次传递订阅生成的通知总数。|  
|\<*number*> 个错误|计划和传递处理器无法传递或不再试图传递的通知数。|  
|无法发送邮件：传输无法连接到服务器。|表示报表服务器未连接到邮件服务器；此消息来自电子邮件传递扩展插件。|  
|文件 \<*filename*> 已写入 \<path>。|表示已成功传递到文件共享位置；此消息来自文件共享传递扩展插件。|  
|写入文件时出现未知错误。|表示未能成功传递到文件共享位置；此消息来自文件共享传递扩展插件。|  
|连接到目标文件夹 \<path> 时出错。 请验证目标文件夹或文件共享是否存在。|表示无法找到指定的文件夹；此消息来自文件共享传递扩展插件。|  
|文件 \<filename> 无法写入 \<path>。 请重试。|表示无法用新版本更新文件；此消息来自文件共享传递扩展插件。|  
|写入文件 \<filename> 时出错：\<message>|表示未能成功传递到文件共享位置；此消息来自文件共享传递扩展插件。|  
|\<自定义状态消息>|与传递成功和失败有关的状态消息，由传递扩展插件提供。 如果使用的是第三方传递扩展插件或自定义传递扩展插件，可能出现其他状态消息。|  
  
 报表服务器管理员还可以监视当前处理的标准订阅。 但不能监视数据驱动订阅。 有关详细信息，请参阅[管理运行中的进程](../../reporting-services/subscriptions/manage-a-running-process.md)。  
  
 如果无法传递订阅（例如，如果邮件服务器不可用），传递扩展插件将重试传递。 可以通过配置设置指定重试的次数。 默认值为不重试。 在某些情况下，处理的报表中可能未包含数据（例如，如果数据源处于脱机状态），这时消息正文中会有相关的内容说明这种情况。  
  
### 本机模式日志文件  
 如果在传递过程中出现错误，将在报表服务器跟踪日志中记录一个条目。  
  
 报表服务器管理员可以查看 **reportserverservice_\*.log** 文件来确定订阅传递的状态。 对于电子邮件传递，报表服务器日志文件包括针对特定电子邮件帐户的处理和传递记录。 以下是日志文件的默认位置：  
  
 `C:\Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\LogFiles`  
  
 以下是一个示例日志文件名：  
  
 `ReportServerService__05_21_2014_00_05_07.log`  
  
 以下是与订阅相关的跟踪日志文件错误消息示例：  
  
-   library!WindowsService_7!b60!05/20/2014-22:34:36:: i INFO: Initializing EnableExecutionLogging to 'True'  as specified in Server system properties.emailextension!WindowsService_7!b60!05/20/2014-22:34:41:: e ERROR: **Error sending email**. Exception: System.Net.Mail.SmtpException: The SMTP server requires a secure connection or the client was not authenticated. The server response was: 5.7.1 Client was not authenticated   at System.Net.Mail.MailCommand.CheckResponse(SmtpStatusCode statusCode, String response)  
  
 日志文件不包括有关是否打开报表或传递是否真正成功的信息。 成功传递意味着计划和传递处理器未生成任何错误，并且报表服务器已连接到邮件服务器。 如果电子邮件在用户邮箱中产生无法传递的消息错误，该信息不会包括在日志文件中。 有关日志文件的详细信息，请参阅 [Reporting Services 日志文件和源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。  
  
##  <a name="bkmk_sharepoint_mode"></a> SharePoint 模式  
 若要在 SharePoint 模式下监视订阅：可以从“管理订阅”  页面监视订阅状态。  
  
1.  浏览到包含该报表的文档库  
  
2.  打开报表的上下文菜单 (**…**)。  
  
3.  选择展开的菜单选项 (**…**)。  
  
4.  选择   
  
### SharePoint ULS 日志文件  
 订阅相关信息被写入 SharePoint ULS 日志。 有关为 ULS 日志配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 事件的详细信息，请参阅[为 SharePoint 跟踪日志 (ULS) 开启 Reporting Services 事件](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)。  以下是一个与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 订阅相关的 ULS 日志条目的示例。  
  
||||||||  
|-|-|-|-|-|-|-|  
|日期|处理|区域|类别|Level|Correlation|消息|  
|5/21/2014 14:34:06:15|应用池：a0ba039332294f40bc4a81544afde01d|SQL Server Reporting Services|报表服务器电子邮件扩展插件|意外|（空）|**发送邮件时出错。** Exception: System.Net.Mail.SmtpException: Mailbox unavailable. The server response was: 5.7.1 Client does not have permissions to send as this sender  at System.Net.Mail.DataStopCommand.CheckResponse(SmtpStatusCode statusCode, String serverResponse)  at System.Net.Mail.DataStopCommand.Send(SmtpConnection conn)  at System.Net.Mail.SmtpClient.Send(MailMessage message)  at Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider.Deliver(Notification notification)|  
  
##  <a name="bkmk_use_powershell"></a> 使用 PowerShell 监视订阅  
 如需查看可用于检查本机模式或 SharePoint 模式订阅的状态的 PowerShell 脚本的示例，请参见 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage subscription owners and run subscription - powershell.md)。  
  
##  <a name="bkmk_manage_inactive"></a> 管理不活动的订阅  
 如果订阅处于不活动状态，则应将其删除，或者通过消除阻止对其进行处理的基本条件将其重新激活。 如果发生阻止处理订阅的条件，订阅会变为不活动状态。 这些条件包括：  
  
-   删除或卸载订阅中指定的传递扩展插件。  
  
-   将凭据设置从存储值更改为集成值或提示值。  
  
-   在报表定义中更改参数名称或数据类型，然后重新发布报表。 如果订阅包括不再有效的参数，则订阅将变为不活动状态。  
  
-   更改报表的执行模式（例如，修改按需运行报表，使其作为报表执行快照运行）。 有关详细信息，请参阅[设置报表处理属性](../../reporting-services/report-server/set-report-processing-properties.md)。  
  
 不活动的订阅由订阅本身所包含的消息来表示。 该消息包括有关原因以及重新激活订阅所应采取的步骤的信息。  
  
 如果存在导致订阅变为不活动的条件，当报表服务器运行订阅时，订阅会反映此情况。 如果安排订阅在每周五早上 2:00 传递报表，而订阅使用的传递扩展插件在周一上午 9:00 被卸载，则订阅直到周五早上 2:00 才会反映其不活动状态。  
  
## 另请参阅  
 [（旧）创建和管理本机模式报表服务器的订阅](http://msdn.microsoft.com/zh-cn/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)   
 [订阅和传递 (Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
  