---
title: "排除 Reporting Services 订阅和传递 |Microsoft 文档"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae1775f7-9919-48ca-8bd7-cc16df274e2c
caps.latest.revision: 16
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2c3031036636e8c2ba2e2a0487ea2092c882c3e0
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot-reporting-services-subscriptions-and-delivery"></a>对 Reporting Services 订阅和传递进行故障排除
  
    
利用本主题解决你在执行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] 报表订阅、计划和传递时遇到的问题。  
## <a name="log-information"></a>日志信息
 
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 中的订阅页包含订阅状态，如果订阅出现问题， [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 日志中将包含详细信息。 
![ssrs_tutorial_datadriven_subscription_status_ReportManager](../../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png)

**跟踪日志：** 跟踪日志是文本文件，将写入到： `\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`

以下是一个示例日志项：

```
   subscription WindowsService_10   4c7c    05/24/2016-01:05:06  e ERROR     Failure writing file \\ServerName\SalesReports\so71949.xls : Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider+NetworkErrorException: An impersonation error occurred using the security context of the current user. ---> System.ArgumentException: Value does not fall within the expected range.  05/24/2016
```
有关 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 跟踪日志的详细信息，请参阅： 
+ [报表服务器跟踪日志](../../reporting-services/report-server/report-server-service-trace-log.md)。
+ [Reporting Services 日志文件](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。

**执行日志视图：**

执行日志是 ReportServer SQL 数据库中的视图。有关 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 的详细信息，请参阅 [Reporting Services ExecutionLog 和 ExecutionLog3 视图](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)。  

----------
## <a name="unable-to-send-reports-using-e-mail-with-windows-server-2003-and-pop3"></a>无法在 Windows Server 2003 和 POP3 中使用电子邮件发送报表  
如果你正在 Microsoft Windows Server 2003 上运行具有邮局协议版本 3 (POP3) 的电子邮件应用程序，可能无法使用本地 POP3 服务器发送报表。 如果将报表服务器配置为使用本地 POP3 服务器发送电子邮件，并创建发送报表的订阅，则可能会收到以下错误消息：  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Failure sending mail: <error message>`  
  
其中\<错误消息 > 替换为返回从协作数据对象 (CDO) 的其他错误消息信息。  
  
### <a name="to-resolve-this-problem"></a>解决此问题：  
* 将 `SendUsing` 元素在 **Rsreportserver.config** 文件中的值设置为 1。  
* 清除 `SMTPServer` 属性的值，使其为空。 还需要为 `SMTPServerPickupDirectory` 属性提供值。   
  
有关使用本地 SMTP 服务传递报表电子邮件的详细信息，请参阅“配置报表服务器以进行电子邮件传递”。  
  
## <a name="failure-sending-mail-the-server-rejected-the-sender-address-the-server-response-was-454-573-client-does-not-have-permission-to-submit-mail-to-this-server"></a>无法发送邮件: 服务器拒绝了发件人地址。 服务器响应为: 454 5.7.3 客户端无权向本服务器提交邮件  
当 SMTP 服务器上的安全策略设置仅允许经过身份验证的用户提交邮件以进行后续传递时，会出现此错误。 如果 SMTP 服务器不接受匿名用户的电子邮件提交，则请与系统管理员联系以获取使用服务器的权限。  
> 将 Exchange 服务器名称指定为 SMTPServer 时也会发生这种错误。 若要使用 Exchange 服务器传递电子邮件，必须指定为 Exchange 服务器配置的 SMTP 网关的名称。 请与 Exchange 管理员联系获取此信息。  
  
## <a name="subscriptions-are-not-processing"></a>未处理订阅  
在以下情况下订阅可能会失败：   
* 用于触发报表的计划已过期。 对于触发报表快照更新的订阅，用于刷新快照的计划可能已过期。  
  
* 报表服务器、SQL Server 代理或电子邮件服务器应用程序没有运行。  
* 报表无法传递（例如，报表太大）。 若要确定是否因报表太大而导致传递失败，请将报表保存到文件中，然后通过电子邮件发送它。 请确保选择的呈现格式与您在订阅中指定的呈现格式相同。 如果收到传递错误，请使用文件共享传递扩展插件，而不是使用报表服务器电子邮件传递扩展插件。  
* 用于传递共享文件的计算机没有运行，或将文件共享配置为只读访问。  
* 订阅中指定的传递扩展插件已被卸载或禁用。  
* 凭据设置从存储值更改为集成值或提示值。  
* 参数名或数据类型在报表定义中已更改，并且重新发布了该报表。 如果订阅包括不再有效的参数，则订阅将变为不活动状态。  
  
有关详细信息，请参阅 TechNet Wiki 中的 [解决 Reporting Services 的问题](http://social.technet.microsoft.com/wiki/contents/articles/1633.ssrs-troubleshoot-issues-and-errors-with-reporting-services.aspx)。  
  
  
    
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]


