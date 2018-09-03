---
title: Reporting Services 配置文件 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4a9b35e25f5ef9c43c871b4c75437f5a1fbf9f93
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265175"
---
# <a name="reporting-services-configuration-files"></a>Reporting Services 配置文件
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 将组件信息存储在注册表和配置文件中，其中配置文件会在安装过程中复制到文件系统。 配置文件包含仅供内部使用的值和用户定义的值的组合。 可以通过安装程序、配置工具、命令行实用工具以及手动编辑配置文件的方式来指定用户定义的值。  
  
 仅在添加或配置高级设置时，才需要修改配置文件。 将配置设置指定为 XML 元素或属性。 如果您了解 XML 和配置文件，则可以使用文本编辑器或代码编辑器来修改可以由用户定义的设置。 有关如何修改配置文件的详细信息或了解报表服务器如何读取新的和更新后的配置设置的详细信息，请参阅[修改 Reporting Services 配置文件 (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
> [!NOTE]  
>  在早期版本中，报表管理器具有其自己的名为 RSWebApplication.config 的配置文件。现在，该文件已过时。 如果从以前的安装进行了升级，则不会删除该文件，但报表服务器不会读取其中的任何设置。 如果您的计算机上存在该文件，则应将其删除。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中，所有报表管理器配置设置都存储在 RSReportServer.config 文件中并从该文件中读取。 若要查看已删除或移动的设置列表，请参阅 [SQL Server 2016 的 SQL Server Reporting Services 中的重大更改](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)。  
  
 本主题内容：  
  
-   [配置文件摘要（本机模式）](#bkmk_config_file_Summary_native_mode)  
  
-   [配置文件摘要（SharePoint 模式）](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> 配置文件摘要（本机模式）  
 下表说明配置设置的存储位置。 大多数配置设置都存储在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]附带的配置文件中。 默认情况下，安装目录如下：  
  
```  
C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER  
```  
  
|存储位置：|描述|位置|  
|----------------|-----------------|--------------|  
|RSReportServer.config|存储报表服务器服务的功能区的配置设置：报表管理器、报表服务器 Web 服务和后台处理。 有关每项设置的详细信息，请参阅 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|存储服务器扩展插件的代码访问安全策略。 有关此文件的详细信息，请参阅 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)。|\<Installation directory> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|存储报表管理器的代码访问安全策略。 有关此文件的详细信息，请参阅 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)。|\<Installation directory> \Reporting Services \ReportManager|  
|报表服务器 Web 服务的 Web.config|仅包括 ASP.NET 所需的那些设置。|\<Installation directory> \Reporting Services \ReportServer|  
|报表管理器的 Web.config|仅包括 ASP.NET 所需的那些设置。|\<Installation directory> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|存储用于指定报表服务器服务的跟踪级别和日志记录选项的配置设置。 有关此文件中元素的详细信息，请参阅 [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md)。|\<Installation directory> \Reporting Services \ReportServer \Bin|  
|注册表设置|存储用于卸载 Reporting Services 的配置状态和其他设置。 如果要解决安装或配置问题，则可以查看这些设置以获取有关如何配置报表服务器的信息。<br /><br /> 不要直接修改这些设置，因为此操作会使安装无效。|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> **- 和 -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|存储报表设计器的配置设置。 有关详细信息，请参阅 [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)。|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies。|  
|RSPreviewPolicy.config|存储报表预览期间使用的服务器扩展插件的代码访问安全策略。 有关此文件的详细信息，请参阅 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)。|C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> 配置文件摘要（SharePoint 模式）  
 下表说明用于 SharePoint 模式报表服务器的配置文件。 大多数配置设置存储在 SharePoint 服务应用程序数据库中。 有关详细信息，请参阅 [Reporting Services SharePoint 服务和服务应用程序](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)。  
  
 默认情况下，SharePoint 模式的安装目录如下：  
  
```  
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|存储位置：|描述|位置|  
|----------------|-----------------|--------------|  
|RSReportServer.config|存储报表服务器服务的功能区的配置设置：报表管理器、报表服务器 Web 服务和后台处理。 有关每项设置的详细信息，请参阅 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|存储服务器扩展插件的代码访问安全策略。 有关此文件的详细信息，请参阅 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)。|\<Installation directory> \Reporting Services \ReportServer|  
|报表服务器 Web 服务的 Web.config|仅包括 ASP.NET 所需的那些设置。|\<Installation directory> \Reporting Services \ReportServer|  
|注册表设置|存储用于卸载 Reporting Services 的配置状态和其他设置。 另外还存储每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的信息。<br /><br /> 不要直接修改这些设置，因为此操作会使安装无效。|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> 示例实例 ID：MSSQL13.MSSQLSERVER<br /><br /> **- 和 -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|存储报表设计器的配置设置。 有关详细信息，请参阅 [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)。|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies。|  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 报表服务器（本机模式）](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Reporting Services 扩展插件](../../reporting-services/extensions/reporting-services-extensions.md)   
 [rsconfig 实用工具 (SSRS)](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
 [启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
