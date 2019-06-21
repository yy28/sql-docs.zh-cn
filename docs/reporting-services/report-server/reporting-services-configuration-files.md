---
title: Reporting Services 配置文件 | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25b695456bbac34e2c6ce8bf8c312c4108dd852e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506646"
---
# <a name="reporting-services-configuration-files"></a>Reporting Services 配置文件
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 将组件信息存储在注册表和配置文件中，其中配置文件会在安装过程中复制到文件系统。 配置文件包含仅供内部使用的值和用户定义的值的组合。 可以通过安装程序、配置工具、命令行实用工具以及手动编辑配置文件的方式来指定用户定义的值。  
  
 仅在添加或配置高级设置时，才需要修改配置文件。 将配置设置指定为 XML 元素或属性。 如果您了解 XML 和配置文件，则可以使用文本编辑器或代码编辑器来修改可以由用户定义的设置。 有关如何修改配置文件的详细信息或了解报表服务器如何读取新的和更新后的配置设置的详细信息，请参阅[修改 Reporting Services 配置文件 (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
> [!NOTE]  
> 在早期版本中，报表管理器具有其自己的名为 RSWebApplication.config 的配置文件。现在，该文件已过时。 如果从以前的安装进行了升级，则不会删除该文件，但报表服务器不会读取其中的任何设置。 如果您的计算机上存在该文件，则应将其删除。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更高版本中，所有报表管理器和 Web 门户配置设置都存储在 RSReportServer.config 文件中，并从中读取。 若要查看已删除或移动的设置列表，请参阅 [SQL Server 2016 的 SQL Server Reporting Services 中的重大更改](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)。  
  
 本文内容：  
  
-   [配置文件摘要（本机模式）](#bkmk_config_file_Summary_native_mode)  
  
-   [配置文件摘要（SharePoint 模式）](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> 配置文件摘要（本机模式）  
 下表说明配置设置的存储位置。 大多数配置设置都存储在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]附带的配置文件中。 默认情况下，安装目录如下：  
  
'' 安装路径  
C:\Program Files\Microsoft SQL Server\MSRSxx.MSSQLSERVER （其中 xx 是 MS SQL 版本号） 或  
C:\Program Files\Microsoft SQL Server Reporting Services\SSRS  
  具体取决于 SSRS 版本
```  
  
|Stored in:|Description|Location|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Stores configuration settings for feature areas of the Report Server service: Report Manager or the web portal, the Report Server Web service, and background processing. For more information about each setting, see [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Stores the code access security policies for the server extensions. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|Stores the code access security policies for the web portal. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportManager|  
|Web.config for the Report Server Web service|Includes only those settings that are required for ASP.NET.|\<Installation directory> \Reporting Services \ReportServer|  
|Web.config for Report Manager|Includes only those settings that are required for ASP.NET if applicable for the SSRS version.|\<Installation directory> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|Stores configuration settings that specify the trace levels and logging options for the Report Server service. For more information about the elements in this file, see [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer \Bin|  
|Registry settings|Stores configuration state and other settings used to uninstall Reporting Services. If you are troubleshooting an installation or configuration problem, you can view these settings to get information about how the report server is configured.<br /><br /> Do not modify these settings directly as this can invalidate your installation.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> **- And -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|Stores configuration settings for Report Designer. For more information, see [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
|RSPreviewPolicy.config|Stores the code access security policies for the server extensions used during report preview. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> Summary of configuration Files (SharePoint mode)  
 The following table provides a description of configuration files used for a SharePoint mode report server. Most configuration settings are stored in SharePoint service application databases. For more information, see [Reporting Services SharePoint Service and Service Applications](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
  
 By default, the installation directory for SharePoint mode is the following:  
  
```Install path
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|存储位置：|描述|位置|  
|----------------|-----------------|--------------|  
|RSReportServer.config|存储报表服务器服务的功能区域的配置设置：报表管理器或 Web 门户、报表服务器 Web 服务和后台处理。 有关每项设置的详细信息，请参阅 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|存储服务器扩展插件的代码访问安全策略。 有关此文件的详细信息，请参阅 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)。|\<Installation directory> \Reporting Services \ReportServer|  
|报表服务器 Web 服务的 Web.config|包括 ASP.NET 所需的如果适用于 SSRS 版本的这些设置。|\<Installation directory> \Reporting Services \ReportServer|  
|注册表设置|存储用于卸载 Reporting Services 的配置状态和其他设置。 另外还存储每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的信息。<br /><br /> 不要直接修改这些设置，因为此操作会使安装无效。|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> 示例实例 ID：MSSQL13.MSSQLSERVER<br /><br /> **- 和 -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|存储报表设计器的配置设置。 有关详细信息，请参阅 [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)。|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies。|  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 报表服务器（本机模式）](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Reporting Services 扩展插件](../../reporting-services/extensions/reporting-services-extensions.md)   
 [rsconfig 实用工具 (SSRS)](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
 [启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
