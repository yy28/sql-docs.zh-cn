---
description: 配置报表服务器 URL（报表服务器配置管理器）
title: 配置报表服务器 URL (Configuration Manager) | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Server Windows service, virtual directories
- report servers [Reporting Services], virtual directories
- virtual directories [Reporting Services]
ms.assetid: a0134ef0-086c-443e-93b9-7213a3d76393
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 70d112c5468929f41b6073c7f001edbad2f86eb7
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934764"
---
# <a name="configure-report-server-urls--report-server-configuration-manager"></a>配置报表服务器 URL（报表服务器配置管理器）
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，URL 用于访问报表服务器 Web 服务和 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]。 在可以使用任一应用程序之前，必须分别为 Web 服务和 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]至少配置一个 URL。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 为这两个应用程序 URL 提供了默认值，默认值在大多数部署方案中都能正常使用，包括与其他 Web 服务和应用程序的并行部署。  
  
-   如果安装了默认配置，则使用默认值自动创建 URL。  
  
-   如果使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具创建或修改 URL，则可以接受 URL 的默认值或指定自定义值。 定义 URL 时页面上会出现该 URL 的测试链接，以便可以立即确认指定的设置是否为有效连接。 有关如何配置和测试的 URL 的分布说明，请参阅[配置 URL（报表服务器配置管理器）](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)。  
  
## <a name="defining-a-report-server-url"></a>定义报表服务器 URL  
 URL 精确标识了网络上报表服务器应用程序实例的位置。 创建报表服务器 URL 时，必须指定以下部分。  
  
|组成部分|说明|  
|----------|-----------------|  
|主机名|TCP/IP 网络使用 IP 地址来唯一标识网络上的设备。 计算机中安装的每个网络适配器都有一个物理 IP 地址。 如果 IP 地址解析为主机标头，则可以指定主机标头。 如果要将报表服务器部署到企业网络上，则可以使用计算机的网络名称。|  
|端口|TCP 端口是设备上的端点。 报表服务器将侦听指定端口上的请求。|  
|虚拟目录|端口通常由多个 Web 服务或应用程序共享。 为此，报表服务器 URL 始终包括与获取请求的应用程序对应的虚拟目录。 您必须为侦听同一 IP 地址和端口的每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序都指定唯一的虚拟目录名称。|  
|SSL 设置|可以将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 URL 配置为，使用计算机中先前安装的现有 TLS/SSL 证书。 有关详细信息，请参阅[在本机模式报表服务器上配置 TLS 连接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。|  
  
## <a name="default-urls"></a>默认 URL  
 通过 URL 访问报表服务器或 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 时，该 URL 应包括主机名称而不是 IP 地址。 在 TCP/IP 网络上，IP 地址将解析为主机名称（或计算机的网络名称）。 如果使用了默认值配置 URL，则应可以使用将计算机名称或 localhost 指定为主机名的 URL 来访问报表服务器 Web 服务：  
  
-   `https://<computername>/reportserver`  
  
-   `https://localhost/reportserver`  
  
 下表中显示了使这些 URL 可用的设置。 该表显示了通过包含主机名的 URL 来启用报表服务器连接的默认值：  
  
|组成部分|值|说明|  
|----------|-----------|-----------------|  
|IP 地址|所有已分配的值|网络上的域名服务将 URL 上的主机名解析为计算机的 IP 地址。 只要定义的 URL 中指定了 IP 地址，发送到特定主机的请求便将到达其预期目标。|  
|端口|80|端口 80 是计算机上进行 TCP/IP 连接的默认端口。 因为报表服务器侦听的是端口 80，所以可以忽略 URL 中的端口号。 如果指定另一个端口，则必须在 URL 中指定该端口。|  
|虚拟目录|ReportServer|请注意，这两个示例 URL 都包括虚拟目录名称。 除非自定义 URL 定义，否则必须始终在 URL 中指定该应用程序的虚拟目录名称。|  
  
> [!NOTE]  
>  基本 URL 预留可启用将在 URL 中使用的任何有效主机名。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具可使用允许将主机名变体解析为特殊报表服务器实例的语法在 HTTP.SYS 中创建一个 URL 预留。 有关 URL 预留的详细信息，请参阅[关于 URL 预留和注册（报表服务器配置管理器）](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)。  
  
## <a name="server-side-permissions-on-a-report-server-url"></a>对报表服务器 URL 的服务器端权限  
 每个 URL 端点的权限都以独占方式授予报表服务器服务帐户。 只有此帐户有权接受定向到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 的请求。 通过安装程序或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具配置服务标识时，创建并维护该帐户的随机访问控制列表 (DACL)。 如果更改服务帐户，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具将更新你创建的所有 URL 预留以拾取新的帐户信息。 有关详细信息，请参阅 [URL 预留语法（报表服务器配置管理器）](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)。  
  
## <a name="authenticating-client-requests-sent-to-a-report-server-url"></a>对发送到报表服务器 URL 的客户端请求进行身份验证  
 默认情况下，URL 端点支持的身份验证类型为 Windows 身份验证。 这是默认的安全扩展插件。 如果要实现自定义或窗体身份验证提供程序，则必须修改报表服务器上的身份验证设置。 还可以选择更改 Windows 身份验证设置，使其与网络中使用的身份验证子系统匹配。 有关详细信息，请参阅 [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [配置 URL（报表服务器配置管理器）](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
 本主题提供了在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具中设置和修改 URL 预留的说明。  
  
 [关于 URL 预留和注册（报表服务器配置管理器）](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)  
 URL 用于访问应用程序和报表。 本主题说明了 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的应用程序 URL、默认 URL 以及 URL 预留和注册的工作方式。  
  
 [URL 预留语法（报表服务器配置管理器）](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用的默认 URL 预留对于大多数情况都是有效的。 但是，如果要限制访问权限或扩展部署以启用 Internet 或 Extranet 访问，则可能要自定义设置以适合您的要求。 本主题说明了 URL 预留的语法并为如何创建针对特定部署的自定义预留提供了建议。  
  
 [配置文件中的 URL（报表服务器配置管理器）](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)  
 RSReportServer.config 文件包含了 URL 预留的多个条目以及由 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 和报表服务器电子邮件传递使用的 URL。 本主题概述了 URL 配置设置以便您可以了解它们之间如何进行比较。  
  
 [多实例报表服务器部署的 URL 预留（报表服务器配置管理器）](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md)  
 当在一台计算机中安装多个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例时，如果已注册某个 URL，便会增加 URL 重复的可能性。 若要避免这些错误，请遵循本主题中针对创建特定于实例的 URL 预留的建议。  
  
## <a name="see-also"></a>另请参阅  
 [配置 URL（报表服务器配置管理器）](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 
