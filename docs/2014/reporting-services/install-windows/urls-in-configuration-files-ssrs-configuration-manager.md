---
title: 配置文件中的 URL（SSRS 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL configuration [Reporting Services]
ms.assetid: 4f5e7fe0-b5b1-4665-93d4-80dce12d6b14
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 528df24b3963d83a236f198055614d15ab66a5c4
ms.sourcegitcommit: 553ecea0427e4d2118ea1ee810f4a73275b40741
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65619785"
---
# <a name="urls-in-configuration-files--ssrs-configuration-manager"></a>配置文件中的 URL（SSRS 配置管理器）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在 RSReportServer.config 文件中存储应用程序设置。 在此文件内，有一些既用于 URL 又用于 URL 预留的配置设置。 这些配置设置的用途和修改规则大不相同。 如果您习惯于通过修改配置文件来优化部署，则本主题可帮助您了解每项 URL 设置的用法。  
  
## <a name="url-settings-in-rsreportserverconfig-file"></a>RSReportServer.config 文件中的 URL 设置  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 存储用于进行应用程序和报表访问的 URL，以及将 Web 前端组件连接到后端报表服务器的 URL。  
  
#### <a name="urls-for-application-access"></a>用于进行应用程序访问的 URL  
 URL 用于访问报表服务器 Web 服务和报表管理器。 若要配置 URL，必须使用 Reporting Services 配置工具。 该工具用于为 HTTP.SYS 中的每个应用程序创建 URL 预留，并为 RSReportServer.config 的 `URLReservations` 部分中的 URL 添加条目。  
  
-   若要查看的每个元素中的说明`URLReservations`部分中，请参阅[RSReportServer 配置文件](../report-server/rsreportserver-config-configuration-file.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
-   有关语法的详细信息`UrlString`元素，请参阅[URL 保留语法&#40;SSRS 配置管理器&#41;](url-reservation-syntax-ssrs-configuration-manager.md)。  
  
-   有关如何配置用于应用程序访问的 URL 的说明，请参阅 [配置 URL（SSRS 配置管理器）](configure-a-url-ssrs-configuration-manager.md)。  
  
#### <a name="urls-for-report-access"></a>用于进行报表访问的 URL  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包括可用于发送报表链接或附件的报表服务器电子邮件传递扩展插件。 传递报表时将构造报表链接。 报表服务器电子邮件传递扩展插件使用配置文件中的 `UrlRoot` 设置来创建链接。 `UrlRoot` 还用于解析通过无人参与的报表处理生成的呈现报表中的链接。  
  
 当您配置用于应用程序访问的 URL 时，将在 RSReportServer.config 文件中自动指定 `UrlRoot`。 如果在配置文件中修改该值，则必须指定连接到报表服务器数据库（包含要传递的报表）的报表服务器 Web 服务的有效 URL 地址。 您只可以为一个报表服务器实例指定一个 `UrlRoot`；对于任何给定的报表服务器实例，RSReportServer.config 文件中只能存在一个 `UrlRoot` 条目。 如果您为报表服务器 Web 服务保留了多个 URL，则必须为 `UrlRoot` 选择其中一个可用值。  
  
 在大多数情况下，您无需修改 `UrlRoot`。 但是，如果将通过完全限定的 URL 访问报表服务器，并且未配置使用主机标头为完全限定的站点名称的 URL，则必须编辑 RSReportServer.config 手动以设置`UrlRoot`到完全限定报表服务器将用于呈现报表的 URL (例如， https://www.adventure-works.com/mywebapp/reportserver)。  
  
#### <a name="urls-connecting-report-manager-and-web-parts-to-the-report-server-web-service"></a>用于将报表管理器和 Web 部件连接到报表服务器 Web 服务的 URL  
 报表管理器和 Reporting Services 的 SharePoint 2.0 Web 部件是连接到报表服务器的 Web 前端组件。 用于连接到后端报表服务器的 URL 包括：  
  
-   `ReportServerUrl`（由报表管理器使用）  
  
-   `ReportServerExternalUrl`（由 Web 部件使用）  
  
> [!NOTE]  
>  Reporting Services 的早期版本包括 `ReportServerVirtualDirectory` 元素。 此值在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中过时了。 如果您已升级现有安装并正在使用包含此设置的配置文件，则报表服务器不再读取该值。  
  
 下表简要概括了所有可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置文件中指定的 URL。  
  
|设置|用法|Description|  
|-------------|-----------|-----------------|  
|`ReportServerUrl`|可选。 除非您自己添加此元素，否则此元素不包含在 RSReportServer.config 文件中。 仅当您配置以下方案之一时才应设置此元素：<br /><br /> 报表管理器提供对在另一台计算机上运行或在同一台计算机上的另一实例上运行的报表服务器 Web 服务的 Web 前端访问。<br /><br /> 当您有指向一个报表服务器的多个 URL，并且您希望报表服务器使用特定的 URL 时。<br /><br /> 您有特定的报表服务器 URL，您希望所有报表管理器连接均使用此 URL。<br /><br /> 例如，您可能为网络中的所有计算机都启用报表管理器访问，但需要报表管理器通过一个本地连接连接到报表服务器。 在这种情况下，你可以配置`ReportServerUrl`到"http://localhost/reportserver"。<br /><br /> <br /><br /> 有关如何实现这些方案的说明，请参阅[配置报表管理器&#40;本机模式&#41;](../report-server/configure-web-portal.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。|该值指定一个指向报表服务器 Web 服务的 URL。 此值由报表管理器在启动时读取。 如果已设置该值，则报表管理器将连接到此 URL 中指定的报表服务器。<br /><br /> 默认情况下，报表管理器提供对与报表管理器运行在同一报表服务器实例中的报表服务器 Web 服务的 Web 前端访问。 然而，如果希望将报表管理器与作为另一实例一部分或在另一台计算机的实例上运行的报表服务器 Web 服务一起使用，则可以将此 URL 设置为定向报表管理器使之连接到外部报表服务器 Web 服务。<br /><br /> 如果安全套接字层 (SSL) 证书安装在您要连接的报表服务器上，则 `ReportServerUrl` 值必须是为获得此证书而注册的服务器的名称。 如果收到错误，"基础连接已关闭：无法建立信任关系为 SSL/TLS 安全通道"，设置`ReportServerUrl`到为其颁发 SSL 证书的服务器的完全限定的域名。 例如，如果证书注册到**https:\//adventure-works.com.onlinesales**，则报表服务器 URL 将为**https:\//adventure-works.com.onlinesales/reportserver**。|  
|`ReportServerExternalUrl`|可选。 除非您自己添加此元素，否则此元素不包含在 RSReportServer.config 文件中。<br /><br /> 仅当您使用的是 SharePoint 2.0 Web 部件且希望用户能够检索报表并在新的浏览器窗口中打开该报表时，才应设置此元素。<br /><br /> 添加 <`ReportServerExternalUrl`> 下 <`ReportServerUrl`> 元素，然后将设置为完全限定的报表服务器名称解析为报表服务器实例时在单独的浏览器窗口中访问。 不要删除 <`ReportServerUrl`>。<br /><br /> 下面的示例说明了相应的语法：<br /><br /> `<ReportServerExternalUrl>http://myserver/reportserver</ReportServerExternalUrl>`|该值由 SharePoint 2.0 Web 部件使用。<br /><br /> 在早期版本中，建议您设置该值以在面向 Internet 的报表服务器上部署报表生成器。 这是未经测试的部署方案。 如果您在过去使用此设置支持对报表生成器的 Internet 访问，那么现在您应考虑使用替代策略。|  
  
## <a name="see-also"></a>请参阅  
 [配置报表服务器 URL（SSRS 配置管理器）](configure-report-server-urls-ssrs-configuration-manager.md)   
 [配置 URL（SSRS 配置管理器）](configure-a-url-ssrs-configuration-manager.md)  
  
  
