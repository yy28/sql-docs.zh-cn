---
title: 修改 Reporting Services 配置文件 (RSreportserver.config) | Microsoft Docs
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 958ef51f-2699-4cb2-a92e-3b4322e36a30
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b3bcc1ef9a96baae8f0a98b0b57488b3fb4dcd76
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43268354"
---
# <a name="modify-a-reporting-services-configuration-file-rsreportserverconfig"></a>修改 Reporting Services 配置文件 (RSreportserver.config)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 将应用程序设置存储在一组配置文件中。 安装程序会为您安装的每个报表服务器实例创建配置文件。 每个文件中的值要么在安装过程中设置，要么在您使用工具和应用程序将服务器配置为执行某个操作时设置。 在某些情况下，必须直接修改文件来添加或配置高级设置。 将配置设置指定为 XML 元素或属性。 如果您了解 XML 和配置文件，则可以使用文本编辑器或代码编辑器来修改可以由用户定义的设置。  
  
 某些配置设置只能通过工具来设置。 包含加密值的设置必须通过 Reporting Services 配置工具、安装程序或 **rsconfig** 命令行实用工具来修改。 若要运行这些工具，您必须是本地 Administrators 组的成员。  
  
> [!IMPORTANT]  
>  在修改配置文件时一定要格外小心。 如果要修改供内部使用而保留的设置，则可能会禁用您的安装。 通常，除非试图解决的是特定问题，否则建议您不要修改配置设置。 有关可安全更改的设置的详细信息，请参阅 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 或 [RSReportDesigner 配置文件](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)。 有关配置文件的详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 产品文档。  
  
 本主题内容：  
  
-   [读取和使用配置值](#bkmk_read_values)  
  
-   [关于默认值](#bkmk_default_values)  
  
-   [删除配置设置](#bkmk_delete_config_settings)  
  
-   [编辑 Reporting Services 配置文件](#bkmk_edit_configuation_file)  
  
##  <a name="bkmk_read_values"></a> 读取和使用配置值  
 当启动服务时或保存配置文件时，报表服务器会读取配置文件。 在当前的应用程序域过期之后，新值和修订后的值会在新应用程序域中生效。 如有可能，仍在当前应用程序域中处理的请求将能够完成。 但是，有几个设置要求立即执行应用程序域回收操作。 在这种情况下，所有正在进行的请求都将在新的应用程序域中重新启动。  
  
 如果报表服务器检测到无效值，则报表服务器会在 Windows 应用程序日志中记录一个错误，报表服务器将无法启动或者将使用默认值，具体取决于错误的类型：  
  
-   如果错误类型为 XML 格式不正确，则报表服务器将不启动。 如果当引入错误时报表服务器正在运行，则报表服务器将忽略无效的配置文件，直到报表服务器重新启动或回收了应用程序域为止。 一旦检测到错误，报表服务器将不再启动。  
  
-   如果该错误是无效的配置值，则服务器将使用内部默认值并在跟踪日志文件中记录一个错误。 在少数情况下，内部默认值不可用，如果无效的配置设置对于服务器操作至关重要，则服务器将返回 rsServerConfigurationError 错误。 有关缺少或无效的关键设置的错误将以 HTML 错误页的形式返回到客户端应用程序，并且将记录到事件日志中。  
  
 所有的配置文件更改（包括成功的更改）都将记录在报表服务器的跟踪日志文件中。 仅将错误记录到应用程序事件日志中。  
  
##  <a name="bkmk_default_values"></a> 关于默认值  
 大多数配置设置都具有在报表服务器内部指定的默认值。 如果用户定义的值无效或者未指定，报表服务器将使用这些默认值。 如果由于配置设置无效而必须使用默认值，则错误将写入跟踪日志文件中。  
  
##  <a name="bkmk_delete_config_settings"></a> 删除配置设置  
 对于具有默认值的配置设置，从配置文件中删除该设置将没有任何效果。 大多数配置设置实际上都是在内部定义和配置的。 如果从配置文件中删除项目，则内部副本仍将可用并使用为其定义的默认值。  
  
##  <a name="bkmk_edit_configuation_file"></a> 编辑 Reporting Services 配置文件  
  
1.  查找要编辑的配置文件：  
  
    -   **RSReportServer.config** 位于以下文件夹中：  
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
        ```  
        
        ||  
        |-|  
        |**[!INCLUDE[applies](../../includes/applies-md.md)]**  SQL Server Reporting Services 中 2017 年 1 月的 Power BI 技术预览版报表|
        
        ```  
        C:\Program Files\Microsoft SQL Server Reporting Services\RSServer\ReportServer
        ```
  
    -   **RSReportServerServices.exe.config** 位于以下文件夹中：  
    
        > [!NOTE] 
        > SQL Server Reporting Services 中 2017 年 1 月的 Power BI 技术预览版报表不支持此配置文件。
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin  
        ```  
  
    -   **RSReportDesigner.config** 位于以下文件夹中：  
  
        ```  
        C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
        ```  
  
2.  如果需要回滚所做的更改，请保存该文件的副本。  
  
3.  在“记事本”或代码编辑器中打开原始文件。 请不要使用 Textpad，因为它会在保存文件之前设置文件长度，从而导致向跟踪日志文件中写入无效字符的错误。  
  
4.  键入要添加或使用的元素或值。 元素是区分大小写的。 如果要添加元素，请确保使用大小写正确的字母。 如果要自定义呈现扩展插件、身份验证扩展插件或数据处理扩展插件，则可以使用配置文件的具体编辑说明：  
  
    -   [针对报表服务器的身份验证](../../reporting-services/security/authentication-with-the-report-server.md)  
  
    -   [配置 Web 门户以传递自定义身份验证 Cookie](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)
  
    -   [在 RSReportServer.Config 中自定义呈现扩展插件参数](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
5.  保存该文件。  
  
6.  检查跟踪日志文件，确认没有错误发生。 如果看到错误情况，则说明错误地指定了某个设置或它的值。 请检查 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) ，了解引起错误的任何设置的有效值。 有关查看跟踪日志的详细信息，请参阅 [报表服务器服务跟踪日志](../../reporting-services/report-server/report-server-service-trace-log.md)。  
  
## <a name="see-also"></a>另请参阅  
 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [ReportingServicesService 配置文件](../../reporting-services/report-server/reportingservicesservice-configuration-file.md)   
 [RSReportDesigner 配置文件](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [部署数据处理扩展插件](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [部署传递扩展插件](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)   
 [部署呈现扩展插件](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)   
 [Reporting Services 配置文件](../../reporting-services/report-server/reporting-services-configuration-files.md)  
  
  
