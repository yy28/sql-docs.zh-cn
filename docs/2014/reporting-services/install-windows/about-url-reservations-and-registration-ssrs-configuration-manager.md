---
title: 关于 URL 预留和注册（SSRS 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
- URL registration
- Report Server service, URL reservations
ms.assetid: c2c460c3-e749-4efd-aa02-0f8a98ddbc76
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f81ac60dbd6ea315bab70d2f65e4953b456f3034
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59968283"
---
# <a name="about-url-reservations-and-registration--ssrs-configuration-manager"></a>关于 URL 预留和注册（SSRS 配置管理器）
  Reporting Services 应用程序的 URL 在 HTTP.SYS 中定义为 URL 预留。 URL 预留定义了指向 Web 应用程序的 URL 端点的语法。 在报表服务器上配置应用程序时，将定义报表服务器 Web 服务和报表管理器的 URL 预留。 通过安装程序或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具配置 URL 时，会自动为你创建 URL 预留：  
  
-   安装程序将使用默认值创建 URL 预留。 如果安装程序安装默认配置，它将保留两个 URL；一个是报表服务器 Web 服务的 URL，另一个是为报表管理器保留的 URL。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具添加更多 URL 或修改安装程序创建的默认 URL。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具将根据你在此工具的 **“Web 服务 URL”** 或 **“报表管理器 URL”** 页中指定的 URL 创建 URL 预留。  
  
 安装程序和此工具都还会为报表服务器服务分配对 URL 的权限、检查有无重复实例并向 HTTP.SYS 添加 URL 预留。 切勿使用 HttpCfg.exe 或其他工具直接创建或修改 Reporting Services URL 预留。 如果您跳过了某一步骤或设置了无效的值，您将会遇到可能难以诊断或修复的问题。  
  
> [!NOTE]  
>  HTTP.SYS 是一个操作系统组件，用于侦听网络请求并将它们路由至请求队列。 在此版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，HTTP.SYS 为报表服务器 Web 服务和报表管理器建立和维护请求队列。 Internet Information Services (IIS) 不再用于承载或访问 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序。 有关 HTTP.SYS 功能的详细信息，请参阅 MSDN 上的 [HTTP Server API](https://go.microsoft.com/fwlink/?LinkId=92652) （HTTP 服务器 API）。  
  
##  <a name="ReportingServicesURLs"></a> Reporting Services 中的 URL  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装中，可以通过 URL 访问以下工具、应用程序和项：  
  
-   报表服务器 Web 服务  
  
-   报表管理器  
  
-   报表生成器  
  
-   已发布到报表服务器的报表  
  
 不应通过 URL 将其他已发布的、可通过 URL 寻址的项（如模型和共享数据源）作为独立项进行访问。 当在浏览器窗口中查看这些项时，报表服务器不会以有意义的格式显示这些项。  
  
> [!NOTE]  
>  本主题不讨论对报表生成器或存储在报表服务器上的特定报表的 URL 访问。 有关通过 URL 对这些项进行访问的详细信息，请参阅 [联机丛书中的](../access-report-server-items-using-url-access.md) 使用 URL 访问报表服务器项 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
##  <a name="URLreservation"></a> URL 预留和注册  
 URL 预留定义了可用于访问 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序的 URL。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 将在 HTTP.SYS 中为报表服务器 Web 服务和报表管理器保留一个或多个 URL，然后在服务启动时注册它们。 指向报表生成器和报表的 URL 基于报表服务器 Web 服务 URL 预留。 通过向 URL 追加参数，可以通过 Web 服务打开报表生成器或报表。 预留和注册由 HTTP.SYS 实现。 有关详细信息，请参阅 MSDN 上的 [Namespace Reservations, Registration, and Routing](https://go.microsoft.com/fwlink/?LinkId=92653)（命名空间预留、注册和路由）。  
  
 *URL 预留*是指创建指向 Web 应用程序的 URL 端点并将其存储在 HTTP.SYS 中的过程。 HTTP.SYS 是计算机上定义的所有 URL 预留的公共存储库，它定义了一组保证 URL 预留唯一的公共规则。  
  
  URL 注册在服务启动时进行。 此时会创建请求队列，并且 HTTP.SYS 开始将请求路由到该队列。 必须先注册 URL 端点，然后再将定向至该端点的请求添加到该队列。 当报表服务器服务启动时，它将注册已为所有启用的应用程序保留的所有 URL。 也就是说，必须启用 Web 服务，才能进行注册。 如果在外围应用配置中，对于基于策略的管理的 Reporting Services 方面将 **WebServiceAndHTTPAccessEnabled** 属性设置为 **False**，则 Web 服务的 URL 在该服务启动时将不会注册。  
  
 如果停止服务或回收 Web 服务或报表管理器应用程序域，则会撤消注册 URL。 如果在服务正在运行时修改 URL 预留，报表服务器将会立即回收应用程序域，以便可以撤消注册旧的 URL，开始注册新的 URL。  
  
 下面几个简单的示例说明了 URL 预留的概念以及它与用于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序的 URL 地址之间的关联。 需要注意一个关键点，即 URL 预留与用于访问应用程序的 URL 具有不同的语法：  
  
|HTTP.SYS 中的 URL 预留|URL|解释|  
|---------------------------------|---------|-----------------|  
|http://+:80/reportserver|http://\<computername>/reportserver<br /><br /> http://\<IPAddress>/reportserver<br /><br /> http://localhost/reportserver|此 URL 预留针对端口 80 指定了一个通配符 (+)。 这会将指定主机（在端口 80 上解析为报表服务器计算机）的任何传入请求放入报表服务器队列中。 请注意，借助此 URL 预留，可以使用任意数目的 URL 访问报表服务器。<br /><br /> 对于大多数操作系统而言，这是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器的默认 URL 预留。|  
|http://123.45.67.0:80/reportserver|http://123.45.67.0/reportserver|此 URL 预留指定了一个 IP 地址，与通配符 URL 预留相比，其限制性要强很多。 只能使用包含此 IP 地址的 URL 连接到报表服务器。 给定此 URL 保留项，对 http:// 上报表服务器的请求\<计算机名 > / reportserver 或 http://localhost/reportserver会失败。|  
  
##  <a name="DefaultURLs"></a> 默认 URL  
 如果在默认配置中安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，安装程序将为报表服务器 Web 服务和报表管理器保留 URL。 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具中定义 URL 预留时，也可以接受这些默认值。 如果安装 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 或安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 作为命名实例，则默认 URL 将包含实例名称。  
  
> [!IMPORTANT]  
>  实例字符为下划线字符 (`_`)。  
  
 URL 预留包含一个端口号。 以下操作系统将允许多个 Web 应用程序共享一个端口：  
  
1.  [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
2.  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
3.  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
4.  [!INCLUDE[win7](../../includes/win7-md.md)]  
  
5.  [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]  
  
|实例类型|应用程序|默认 URL|HTTP.SYS 中的实际 URL 预留|  
|-------------------|-----------------|-----------------|----------------------------------------|  
|默认实例|报表服务器 Web 服务|http://\<servername>/reportserver|http://\<servername>:80/reportserver|  
|默认实例|报表管理器|http://\<servername>/reportserver|http://\<servername>:80/reportserver|  
|命名实例|报表服务器 Web 服务|http://\<servername>/reportserver_\<instancename>|http://\<servername>:80/reportserver_\<instancename>|  
|命名实例|报表管理器|http://\<servername>/reports_\<instancename>|http://\<servername>:80/reports_\<instancename>|  
|SQL Server Express|报表服务器 Web 服务|http://\<servername>/reportserver_SQLExpress|http://\<servername>:80/reportserver_SQLExpress|  
|SQL Server Express|报表管理器|http://\<servername>/reports_SQLExpress|http://\<servername>:80/reports_SQLExpress|  
  
##  <a name="URLPermissionsAccounts"></a> Reporting Services URL 的身份验证和服务标识  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 预留指定了报表服务器服务的服务帐户。 运行服务的帐户用于为运行在同一实例上的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序创建的所有 URL。 报表服务器实例的服务标识存储在 RSReportServer.config 文件中。  
  
 服务帐户没有默认值。 但是，在安装过程中需要指定服务帐户，即使以“仅文件”模式安装服务器，也会在 RSReportServer.config 中的 `URLReservation` 中指定服务帐户。 服务帐户的有效值包括域用户帐户、`LocalSystem` 或 `NetworkService`。  
  
 因为默认安全性为 `RSWindowsNegotiate`，所以匿名访问已禁用。 对于 Intranet 访问，报表服务器 URL 使用网络计算机名称。 如果要为 Internet 连接配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，必须使用其他设置。 有关身份验证的详细信息，请参阅 [联机丛书中的](../security/authentication-with-the-report-server.md) 使用报表服务器进行身份验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
##  <a name="URLlocalAdmin"></a> 用于本地管理的 URL  
 如果为 URL 预留指定了强通配符或弱通配符，则可使用 http://localhost/reportserver 或 http://localhost/reports。  
  
 http://localhost URL 将解释为 http://127.0.0.1。 如果你将 URL 预留限定为计算机名称或单个 IP 地址，则除非在本地计算机上为 127.0.0.1 创建附加预留，否则将无法使用 localhost。 同样，如果您的计算机上禁用 localhost 或 127.0.0.1，也无法使用该 URL。  
  
 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 和 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] 包括新的安全功能，可以将偶然使用提升的权限运行程序的风险降到最低。 还需要执行一些其他步骤，才能在这些操作系统上启用本地管理。 有关详细信息，请参阅 [为本地管理配置本机模式报表服务器 (SSRS)](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
##  <a name="URLSharePoint"></a> 在 SharePoint 集成模式下的报表服务器的 Url  
 如果独立报表服务器配置为在较大的 SharePoint 产品或技术部署中运行，则 URL 和虚拟目录构造将在以下几个方面受到影响：  
  
-   报表及其他项的 URL 通过 SharePoint Web 应用程序 URL 进行寻址。 如果通过 URL 访问特定报表，请始终使用包含站点路径、文档库、项名称和文件扩展名（例如，报表的扩展名为 .rdl）的完全限定的 URL。 在报表中引用共享数据源和模型以及在为对报表服务器的发布操作指定目标服务器和文件夹时，必须指定完全限定的 URL。  
  
-   文件扩展名用来区分不同类型的报表服务器项。 有效的扩展名包括用于报表定义的 .rdl、用于报表模型的 .smdl 以及用于为 SharePoint 站点创建的共享数据源的 .rsds。  
  
-   尽管 SharePoint 产品和技术具有为自身定义的 URL 预留，但在发布到服务器时你可以忽略这种预留。 对于 SharePoint Web 应用程序，URL 预留是内部操作。  
  
-   对于单服务器部署在同一台计算机安装的一个集成的报表服务器和 SharePoint 技术实例的位置，不能使用 http://localhost/reportserver。 如果 http://localhost是用于访问 SharePoint Web 应用程序，您必须使用非默认网站或唯一端口分配来访问报表服务器。 此外，如果报表服务器与 SharePoint 场集成在一起，则对于部署中安装在远程计算机上的节点，对报表服务器的 localhost 访问将无法解析。  
  
-   不能为在 SharePoint 集成模式下运行的报表服务器配置报表管理器的 URL 预留和端点。 如果配置了这些项，则在 SharePoint 集成模式下部署报表服务器后，报表管理器将不再工作。 此模式不支持报表管理器。  
  
 如果您集成了某个报表服务器扩展部署以便在较大的 SharePoint 产品或技术部署中运行，请对各报表服务器节点进行负载平衡，并定义指向该扩展部署的单个虚拟服务器 URL。 报表服务器集成设置只允许您指定单个报表服务器 URL。 如果是扩展部署，则此 URL 必须是该扩展部署中各服务器节点的访问点。  
  
## <a name="see-also"></a>请参阅  
 [配置 URL（SSRS 配置管理器）](configure-a-url-ssrs-configuration-manager.md)   
 [URL 预留语法（SSRS 配置管理器）](url-reservation-syntax-ssrs-configuration-manager.md)  
  
  
