---
title: 错误和事件参考 (Reporting Services) | Microsoft Docs
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: troubleshooting
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- messages [Reporting Services]
- errors [Reporting Services]
- Reporting Services, errors and events
- troubleshooting [Reporting Services], errors
- events [Reporting Services]
ms.assetid: 818b4cc1-e65d-4f1a-bf7d-fe269e6dd739
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8fe13ac523188d0cc389176635db43fbdc5eb36f
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43274567"
---
# <a name="errors-and-events-reference-reporting-services"></a>错误和事件参考 (Reporting Services)
  本主题提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的错误和事件的信息。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 日志文件中也包含错误信息。 有关可用日志文件类型以及如何查看日志的详细信息，请参阅 [Reporting Services 日志文件和来源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。  
  
## <a name="cause-and-resolution-for-reporting-services-error-messages"></a>Reporting Services 错误消息的原因和解决方法  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 网站上提供了有关最经常搜索的错误的原因和解决方法信息。 有关详细信息，请参阅 [Cause and Resolution of Reporting Services Errors](../../reporting-services/troubleshooting/cause-and-resolution-of-reporting-services-errors.md)。  
  
## <a name="report-server-events"></a>报表服务器事件  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 应用程序日志中记录了下列报表服务器事件。  
  
|事件 ID|类型|类别|数据源|描述|  
|--------------|----------|--------------|------------|-----------------|  
|106|错误|计划|报表服务器|在定义计划操作（如报表订阅和传递）时，SQL Server 代理必须处于运行状态。|  
|[107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)|错误|启动/关闭|报表服务器<br /><br /> 计划和传递处理器|\<Source> 无法连接到报表服务器数据库。 有关详细信息，请参阅[报表服务器 Windows 服务 (MSSQLServer) 107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)。|  
|108|错误|扩展名|报表服务器<br /><br /> 报表管理器|\<Source> 无法加载传递扩展插件、数据处理扩展插件或呈现扩展插件。<br /><br /> 这很可能是部署不完全或删除扩展插件的结果。 有关详细信息，请参阅 [Deploying a Data Processing Extension](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md) 和 [Deploying a Delivery Extension](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)。|  
|109|信息|管理|报表服务器<br /><br /> 报表管理器|配置文件已修改。 有关详细信息，请参阅 [Reporting Services Configuration Files](../../reporting-services/report-server/reporting-services-configuration-files.md)。|  
|110|警告|管理|报表服务器<br /><br /> 报表管理器|其中一个配置文件中的设置已修改，导致该设置不再有效。 此时将使用默认值。 有关详细信息，请参阅 [Reporting Services Configuration Files](../../reporting-services/report-server/reporting-services-configuration-files.md)。|  
|111|错误|日志记录|报表服务器<br /><br /> 报表管理器|\<Source> 无法创建跟踪日志。 有关详细信息，请参阅 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)。|  
|112|警告|Security|报表服务器|报表服务器已检测到可能存在拒绝服务攻击。 有关详细信息，请参阅 [Reporting Services 安全性和保护](../../reporting-services/security/reporting-services-security-and-protection.md)。|  
|113|错误|日志记录|报表服务器|报表服务器无法创建性能计数器。|  
|114|错误|启动/关闭|报表管理器|报表管理器无法连接到报表服务器服务。|  
|115|警告|计划|计划和传递处理器|SQL Server 代理队列中的计划任务已修改或已删除。|  
|116|错误|内部|报表服务器<br /><br /> 报表管理器<br /><br /> 计划和传递处理器|发生内部错误。|  
|117|错误|启动/关闭|报表服务器|报表服务器数据库版本无效。|  
|118|警告|日志记录|报表服务器<br /><br /> 报表管理器|跟踪日志不在预期的目录位置；此时将在默认目录中创建新的跟踪日志。 有关详细信息，请参阅 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)。|  
|119|错误|激活|报表服务器<br /><br /> 计划和传递处理器|\<Source> 未获取访问报表服务器数据库内容的权限。|  
|120|错误|激活|报表服务器|无法解密对称密钥。 运行该服务所使用的帐户很可能已更改。 有关详细信息，请参阅[配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。|  
|121|错误|启动/关闭|报表服务器|远程过程调用 (RPC) 服务无法启动。|  
|122|警告|传递|计划和传递处理器|计划和传递处理器无法连接到用于电子邮件传递的 SMTP 服务器。 若要详细了解 SMTP 服务器连接，请参阅[为报表服务器配置电子邮件传递（SSRS 配置管理器）](http://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83)。|  
|123|警告|日志记录|报表服务器<br /><br /> 报表管理器|报表服务器无法对跟踪日志进行写入操作。 有关跟踪日志的详细信息，请参阅 [报表服务器服务跟踪日志](../../reporting-services/report-server/report-server-service-trace-log.md)。|  
|124|信息|激活|报表服务器|报表服务器服务已初始化。 有关详细信息，请参阅[初始化报表服务器（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)。|  
|125|信息|激活|报表服务器|用于加密数据的密钥已成功提取。 有关密钥的详细信息，请参阅[配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。|  
|126|信息|激活|报表服务器|用于加密数据的密钥已成功应用。 有关密钥的详细信息，请参阅[配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。|  
|127|信息|激活|报表服务器|加密内容已从报表服务器数据库中成功删除。 有关删除不可恢复的加密数据的详细信息，请参阅[配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。|  
|128|错误|激活|报表服务器|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件。|  
|129|错误|管理|报表服务器<br /><br /> 计划和传递处理器|无法解密已加密的配置文件设置。|  
|130|错误|管理|报表服务器<br /><br /> 计划和传递处理器|\<Source> 找不到配置文件。 报表服务器要求有配置文件。|  
|131|错误|Security|报表服务器<br /><br /> 计划和传递处理器|无法解密已加密的用户数据值。|  
|132|错误|Security|报表服务器|加密用户数据时出现错误。 无法保存该值。|  
|133|错误|管理|报表服务器<br /><br /> 报表管理器<br /><br /> 计划和传递处理器|无法加载配置文件。 如果 XML 无效，则可能发生这一错误。|  
|134|错误|管理|报表服务器|报表服务器无法加密配置文件中某个设置的值。|  
  
## <a name="see-also"></a>另请参阅  
 [监视 Reporting Services 订阅](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)   
 [Reporting Services 日志文件和来源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]
