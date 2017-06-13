---
title: "RsReportServer.config 配置文件 |Microsoft 文档"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 60e0a0b2-8a47-4eda-a5df-3e5e403dbdbc
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 64cab4cc760ee1af2c3777bca88be2663d8039a4
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="rsreportserverconfig-configuration-file"></a>RsReportServer.config 配置文件
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **RsReportServer.config**文件存储报表服务器 Web 服务所使用的设置和后台处理。 所有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序都在一个进程中运行，该进程读取 RSReportServer.config 文件中存储的配置设置。 本机模式和 SharePoint 模式的报表服务器都使用 RSReportServer.config，但是这两个模式并不使用配置文件中的所有相同设置。 文件的 SharePoint 模式版本较小，因为针对 SharePoint 模式的许多设置都存储于 SharePoint 配置数据库中，而非存储于文件中。 本主题介绍为本机模式和 SharePoint 模式安装的默认配置文件，以及该配置文件控制的一些重要设置和行为。  

在 SharePoint 模式下，该配置文件中包含适用于在该计算机上运行的所有服务应用程序实例的那些设置。 SharePoint 配置数据库包含适用于特定服务应用程序的配置设置。 对于每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序，在配置数据库中存储并且通过 SharePoint 管理页进行管理的设置可能会有所不同。  
  
 在以下内容中将按照这些设置在默认安装的配置文件中出现的顺序展示。 有关如何编辑此文件的说明，请参阅 [修改 Reporting Services 配置文件 (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
 
##  <a name="bkmk_file_location"></a> 文件位置  

根据报表服务器模式，RSReportServer.config 位于以下文件夹中：  


  
### <a name="native-mode-report-server"></a>本机模式下的报表服务器  

 
**[!INCLUDE[applies](../../includes/applies-md.md)]**  SQL Server 2016
```  
C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
```

**[!INCLUDE[applies](../../includes/applies-md.md)]**  SQL Server Reporting Services 中 2017 年 1 月的 Power BI 技术预览版报表
```  
C:\Program Files\Microsoft SQL Server Reporting Services\RSServer\ReportServer
```  
  
### <a name="sharepoint-mode-report-server"></a>SharePoint 模式报表服务器

> [!NOTE]
> SharePoint 集成模式下不可用 2017 年 1 月 Power BI 技术预览中 SQL Server Reporting Services 的报表。
  
```  
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
 
有关编辑此文件的详细信息，请参阅 [修改 Reporting Services 配置文件 (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
##  <a name="bkmk_generalconfiguration"></a> 常规配置设置 (rsreportserver.config)  
 下表提供有关在文件的第一部分显示的常规配置设置的信息。 将按设置在配置文件中的显示顺序依次列出： 表的最后一列指示设置是适用于本机模式报表服务器 **(N)** 还是 SharePoint 模式报表服务器 **(S)** 或两者均适用。  
  
> [!NOTE]  
>  在本主题中，“最大整数”是指 INT_MAX 值 2147483647。  有关详细信息，请参阅 [整数限制](http://msdn.microsoft.com/library/296az74e\(v=vs.110\).aspx) (http://msdn.microsoft.com/library/296az74e(v=vs.110).aspx)。  
  
|设置|Description|模式|  
|-------------|-----------------|----------|  
|**Dsn**|指定承载报表服务器数据库的数据库服务器的连接字符串。 在创建报表服务器数据库时，此值会进行加密并添加到配置文件中。 对于 SharePoint，从 SharePoint 配置数据库获取数据库连接信息。|N,S|  
|**ConnectionType**|指定报表服务器用来连接报表服务器数据库的凭据类型。 有效值为 **Default** 和 **Impersonate**。 如果将报表服务器配置为使用**登录帐户或服务帐户连接至报表服务器数据库，则指定** Default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果报表服务器使用一个 Windows 帐户连接到报表服务器数据库，则指定**Impersonate** 。|否|  
|**LogonUser、LogonDomain、LogonCred**|存储报表服务器连接到报表服务器数据库时所使用的域帐户的域、用户名和密码。 将报表服务器连接配置为使用域帐户时，会创建 **LogonUser**、 **LogonDomain**和 **LogonCred** 的值。 有关报表服务器连接的详细信息，请参阅[配置报表服务器数据库连接（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。|否|  
|**InstanceID**|报表服务器实例的标识符。 报表服务器实例的名称取决于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。 此值指定了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称。 默认情况下，此值是**MSRS12***\<instancename >*。 请不要修改此设置。 以下是完整值的一个示例： `<InstanceId>MSRS13.MSSQLSERVER</InstanceId>`<br /><br /> 以下是 SharePoint 模式的示例：<br /><br /> `<InstanceId>MSRS12.@Sharepoint</InstanceId>`|N,S|  
|**InstallationID**|安装程序创建的报表服务器安装的标识符。 此值设置为 GUID。 请不要修改此设置。|否|  
|**SecureConnectionLevel**|指定 Web 服务调用必须使用的安全套接字层 (SSL) 的级别。 此设置适用于报表服务器 Web 服务和 web 门户。 当您在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具中配置 URL 以使用 HTTP 或 HTTPS 时将设置此值。 有效值的范围为 0 到 3 之间，其中 0 的安全性最低。 有关详细信息，请参阅 [使用安全 Web 服务方法](../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md) 和 [配置本机模式报表服务器上的 SSL 连接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。|N,S|  
|**DisableSecureFormsAuthenticationCookie**|默认值为 False。<br /><br /> 指定是否禁止将用于窗体和自定义身份验证 cookie 强制标记为安全的。 从 SQL Server 2012 开始， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 将在发送到客户端时将用于自定义身份验证扩展插件的窗体身份验证 cookie 标记为安全 cookie。 通过更改此属性，报表服务器管理员和自定义安全扩展插件作者可以恢复以前的行为，即允许自定义安全扩展插件作者确定是否将 cookie 标记为安全 cookie。 建议将安全 cookie 用于窗体身份验证，以便帮助防止网络截取和重播攻击。|否|  
|**CleanupCycleMinutes**|指定多少分钟后从报告服务器数据库删除旧会话和过期快照。 有效值的范围为 0 到最大整数之间。 默认值为 10。 如果将值设置为 0，将禁止数据库清除进程。|N,S|  
|**MaxActiveReqForOneUser**|指定一个用户可以同时处理的报表的最大数目。 达到此限制之后，将拒绝进一步的报表处理请求。 有效值介于 1 和最大整数之间。 默认值为 20。<br /><br /> 注意，大多数请求都处理得非常快，因此单个用户在任意给定时间都不太可能拥有 20 个以上的打开连接。 如果用户同时打开了 15 个以上的占用大量进程的报表，则最好增大此值。<br /><br /> 对于在 SharePoint 集成模式下运行的报表服务器，将忽略此设置。|N,S|  
|**DatabaseQueryTimeout**|指定多少秒后与报表服务器数据库的连接超时。 此值将传递到 System.Data.SQLClient.SQLCommand.CommandTimeout 属性。 有效值的范围为 0 到 2147483647。 默认值为 120。 值 0 表示等待时间无限制，因此并不推荐使用该值。|否|  
|**AlertingCleanupCycleMinutes**|默认值为 20。<br /><br /> 确定清理在警报数据库中存储的临时数据的频率。|S|  
|**AlertingDataCleanupMinutes**|默认值为 360。<br /><br /> 确定用于创建或编辑警报定义的会话数据在警报数据库内保留多长时间。 默认值为 6 小时。|S|  
|**AlertingExecutionLogCleanup**Minutes|默认值为 10080。<br /><br /> 确定保留多长时间的警报执行日志值。 默认值为 7 天。|S|  
|**AlertingMaxDataRetentionDays**|默认值为 180。<br /><br /> 确定为防止在警报数据尚未更改时出现重复的警报消息而保留多长时间的警报数据。|S|  
|**RunningRequestsScavengerCycle**|指定取消孤立请求和过期请求的频率。 以秒为单位指定此值。 有效值的范围为 0 到最大整数之间。 默认值为 60。|N,S|  
|**RunningRequestsDbCycle**|指定报表服务器评估到存在正在运行的作业信息中 web 门户的管理作业页上检查是否已超过了报表执行超时，并运行中作业的频率。 以秒为单位指定此值。 有效值的范围为 0 到 2147483647。 默认值为 60。|N,S|  
|**RunningRequestsAge**|指定间隔多长时间后正在运行的作业的状态将从“新建”更改到“正在运行”（秒）。 有效值的范围为 0 到 2147483647。 默认值为 30。|N,S|  
|**MaxScheduleWait**|指定在请求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] “下次运行时间” **时报表服务器 Windows 服务等待** 代理服务更新计划的秒数。 有效值为 1 到 60。<br /><br /> 在默认配置文件中，MaxScheduleWait 设置为 **5**。<br /><br /> 如果报表服务器无法找到或读取该配置文件，则服务器默认为 MaxScheduleWait 设置为 1。|N,S|  
|**DisplayErrorLink**|指示发生错误时是否显示 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 帮助和支持站点的链接。 此链接将显示在错误消息中。 用户单击此链接可以打开此站点上的更新的错误消息内容。 有效值包括 **True** （默认值）和 **False**。|N,S|  
|**WebServiceuseFileShareStorage**|指定是否在文件系统中存储缓存报表和临时快照（由报表服务器 Web 服务在用户会话期间创建）。 有效值为 **True** 和 **False** （默认值）。 如果该值设置为 False，临时数据将存储在 reportservertempdb 数据库中。|N,S|  
|**WatsonFlags**|指定对于报告给 [!INCLUDE[msCoName](../../includes/msconame-md.md)]的错误情况记录多少信息。<br /><br /> 0x0430 = 全部转储<br /><br /> 0x0428 = 小型转储<br /><br /> 0x0002 = 无转储|N,S|  
|**WatsonDumpOnExceptions**|指定您要在错误日志中报告的异常列表。 如果存在重复问题并希望为要发送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 以进行分析的信息创建转储，此设置会非常有用。 创建转储会影响性能，因此仅在诊断问题时才需更改此设置。|N,S|  
|**WatsonDumpExcludeIfContainsExceptions**|指定您希望不要在错误日志中报告的异常列表。 在诊断问题并且不希望服务器为特定异常创建转储时，此设置非常有用。|N,S|  
  
##  <a name="bkmk_URLReservations"></a> URLReservations（RSReportServer.config 文件）  
 **URLReservations**定义对报表服务器 Web 服务和当前实例的 web 门户 HTTP 访问权限。 URL 会在配置报表服务器时保留和存储在 HTTP.SYS 中。  
  
> [!WARNING]  
>  对于 SharePoint 模式，在 SharePoint 管理中心中配置 URL 保留项。 有关详细信息，请参阅 [配置备用访问映射 (http://technet.microsoft.com/library/cc263208(office.12).aspx)](http://technet.microsoft.com/library/cc263208\(office.12\).aspx)。  
  
 请不要直接在该配置文件中修改 URL 保留。 请始终使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器或报表服务器 WMI 提供程序创建或修改用于本机模式报表服务器的 URL 保留。 如果在配置文件中修改此值，则可能会破坏保留，这将导致服务器运行时错误或在卸载软件时将孤立的保留留在未删除的 HTTP.SYS 中。 有关详细信息，请参阅[配置报表服务器 URL（SSRS 配置管理器）](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)和[配置文件中的 URL（SSRS 配置管理器）](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)。  
  
 **URLReservations** 是可选元素。 如果在 RSReportServer.config 文件中没有显示该元素，则可能不用配置服务器。 如果指定了该元素，则必须指定除 **AccountName** 以外的所有子元素。  
  
 表的最后一列指示设置是适用于本机模式报表服务器 (N) 还是 SharePoint 模式报表服务器 (S) 或两者均适用。  
  
|设置|Description|模式|  
|-------------|-----------------|----------|  
|**应用程序**|包含 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序的设置。|否|  
|**名称**|指定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序。 有效值为 ReportServerWebService 或 ReportManager。|否|  
|**VirtualDirectory**|指定应用程序的虚拟目录名称。|否|  
|**URLs，URL**|包含应用程序的一个或多个 URL 保留。|否|  
|**UrlString**|指定适用于 HTTP.SYS 的 URL 语法。 有关语法的详细信息，请参阅 [URL 保留语法（SSRS 配置管理器）](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)。|否|  
|**AccountSid**|指定已为其创建 URL 保留项的帐户的安全标识符 (SID)。 该帐户应为报表服务器服务运行时所使用的帐户。 如果 SID 与服务帐户不匹配，则报表服务器可能无法侦听相应 URL 上的请求。|否|  
|**AccountName**|指定与 **AccountSid**对应的可读帐户名称。 该名称不会被使用，但它会显示在文件中，这样您便可以轻松确定用于相应 URL 保留项的帐户的服务帐户。|否|  
  
##  <a name="bkmk_Authentication"></a> 身份验证（RSReportServer.config 文件）  
 **Authentication** 指定报表服务器所接受的一个或多个身份验证类型。 默认设置和值是本节中介绍的设置和值的子集。 只会自动添加默认设置。 若要添加其他设置，必须使用文本编辑器将相应的元素结构添加到 RSReportServer.config 文件中并设置其值。  
  
 默认值包括 **RSWindowsNegotiate** 和 **RSWindowsNTLM** ，其中 **EnableAuthPersistance** 设置为 **True**：  
  
```  
   <Authentication>  
      <AuthenticationTypes>  
         <RSWindowsNegotiate/>  
         <RSWindowsNTLM/>  
      </AuthenticationTypes>  
      <EnableAuthPersistence>true</EnableAuthPersistence>  
   </Authentication>  
```  
  
 必须手动添加所有其他值。 有关详细信息和示例，请参阅 [针对报表服务器的身份验证](../../reporting-services/security/authentication-with-the-report-server.md)。  
  
 以下表的最后一列指示设置是适用于本机模式报表服务器 (N) 还是 SharePoint 模式报表服务器 (S) 或两者均适用。  
  
|设置|Description|模式|  
|-------------|-----------------|----------|  
|**AuthenticationTypes**|指定一个或多个身份验证类型。 有效值为 **RSWindowsNegotiate**、 **RSWindowsKerberos**、 **RSWindowsNTLM**、 **RSWindowsBasic**和 **Custom**。<br /><br /> 类型**RSWindows** 和 **Custom** 是互斥的。<br /><br /> **RSWindowsNegotiate**、 **RSWindowsKerberos**、 **RSWindowsNTLM**和 **RSWindowsBasic** 是累积的并且可以一起使用，如本节前面的默认值示例所示。<br /><br /> 如果预期会收到来自使用不同类型的身份验证的各种客户端应用程序和浏览器的请求，则必须指定多个身份验证类型。<br /><br /> 不要删除 **RSWindowsNTLM**，否则会将浏览器支持限制为部分受支持的浏览器类型。 有关详细信息，请参阅 [Reporting Services 和 Power View 的浏览器支持](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)。|否|  
|**RSWindowsNegotiate**|报表服务器接受 Kerberos 或 NTLM 安全令牌。 如果报表服务器在本机模式下运行并且服务帐户为 Network Service，这便是默认设置。 如果报表服务器在本机模式下运行并且服务帐户已配置为域用户帐户，将忽略该设置。<br /><br /> 如果为报表服务器服务帐户配置了域帐户但未为报表服务器配置服务主体名称 (SPN)，则该设置可能会阻止用户登录该服务器。|否|  
|**RSWindowsNTLM**|服务器接受 NTLM 安全令牌。<br /><br /> 如果删除此设置，则会将浏览器支持限制为部分受支持的浏览器类型。 有关详细信息，请参阅 [Reporting Services 和 Power View 的浏览器支持](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)。|N, S|  
|**RSWindowsKerberos**|服务器接受 Kerberos 安全令牌。<br /><br /> 如果在约束委派身份验证方案中使用 Kerberos 身份验证，则将使用此设置或 RSWindowsNegotiate。|否|  
|**RSWindowsBasic**|如果建立连接时没有使用凭据，则服务器会接受基本凭据，并发出质询/响应。<br /><br /> 基本身份验证以明文形式在 HTTP 请求中传递凭据。 如果使用基本身份验证，则使用 SSL 对进出报表服务器的网络通信进行加密。 若要查看 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中基本身份验证的示例配置语法，请参阅 [针对报表服务器的身份验证](../../reporting-services/security/authentication-with-the-report-server.md)。|否|  
|**Custom**|如果在报表服务器计算机上部署了自定义的安全扩展插件，请指定此值。 有关详细信息，请参阅 [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)。|否|  
|**LogonMethod**|该值指定 **RSWindowsBasic**的登录类型。 如果指定 **RSWindowsBasic**，则此值是必需的。 有效值为 2 或 3，每个值的含义如下：<br /><br /> **2** = 网络登录，针对要对纯文本密码进行身份验证的高性能服务器<br /><br /> **3** = 明文登录，在此情况下，登录凭据保留在随各 HTTP 请求一起发送的身份验证包中，这样，该服务器在连接到网络中的其他服务器时可以模拟该用户。<br /><br /> <br /><br /> 注意： [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]不支持值 0（针对交互登录）和 1（针对批处理登录）。|否|  
|**Realm**|此值用于 **RSWindowsBasic**。 它指定包含授权和身份验证功能的资源分区，这些功能用于控制对组织中受保护资源的访问。|否|  
|**DefaultDomain**|此值用于 **RSWindowsBasic**。 它用于确定服务器用来对用户进行身份验证的域。 此值是可选的。但如果忽略此值，报表服务器会将计算机名称用作域。 如果在域控制器上安装了报表服务器，则所用的域为该计算机控制的域。|否|  
|**RSWindowsExtendedProtectionLevel**|默认值为 **off**。 有关详细信息，请参阅 [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)|否|  
|**RSWindowsExtendedProtectionScenario**|默认值为 **Proxy**。|否|  
|**EnableAuthPersistence**|确定针对连接还是针对各个请求执行身份验证。<br /><br /> 有效值为 **True** （默认值）或 **False**。 如果设置为 **True**，则从同一连接发出的后续请求会采用第一个请求的模拟上下文。<br /><br /> 如果使用代理服务器软件（如 ISA 服务器）访问报表服务器，则此值必须设置为 **False** 。 如果使用代理服务器，则允许多个用户使用来自代理服务器的单个连接。 对于这种情况，您应禁用身份验证持久性，以便可以对各个用户请求单独进行身份验证。 如果不将 **EnableAuthPersistence** 设置为 **False**，则所有用户都将使用第一个请求的模拟上下文进行连接。|N,S|  
  
##  <a name="bkmk_service"></a> 服务（RSReportServer.config 文件）  
 **Service** 指定作为一个整体应用于服务的应用程序设置。  
  
 以下表的最后一列指示设置是适用于本机模式报表服务器 (N) 还是 SharePoint 模式报表服务器 (S) 或两者均适用。  
  
|设置|Description|模式|  
|-------------|-----------------|----------|  
|**IsSchedulingService**|指定报表服务器是否维护一组与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户创建的计划和订阅相对应的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 代理作业。 有效值包括 **True** （默认值）和 **False**。<br /><br /> 在使用基于策略的管理的 Reporting Services 的外围应用配置器方面启用或禁用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能时，此设置将受到影响。 有关详细信息，请参阅 [启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)。|N,S|  
|**IsNotificationService**|指定报表服务器是否处理通知和传递。 有效值包括 **True** （默认值）和 **False**。 如果该值为 **False**，则不传递订阅。<br /><br /> 在使用基于策略的管理的 Reporting Services 的外围应用配置器方面启用或禁用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能时，此设置将受到影响。 有关详细信息，请参阅 [启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)。|N,S|  
|**IsEventService**|指定服务是否处理事件队列中的事件。 有效值包括 **True** （默认值）和 **False**。 如果该值为 **False**，则报表服务器不会执行针对计划或订阅的操作。<br /><br /> 在使用基于策略的管理的 Reporting Services 的外围应用配置器方面启用或禁用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能时，此设置将受到影响。 有关详细信息，请参阅 [启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)。|N,S|  
|**IsAlertingService**|默认值是 **True**秒|S|  
|**PollingInterval**|指定报表服务器轮询事件表的间隔（秒）。 有效值的范围为 0 到最大整数之间。 默认值为 10。|N,S|  
|**WindowsServiceUseFileShareStorage**|指定是否在文件系统中存储缓存报表和临时快照（由报表服务器服务为用户会话的持续期间创建）。 有效值为 **True** 和 **False** （默认值）。|N,S|  
|**MemorySafetyMargin**|指定 **WorkingSetMaximum** 的百分比，该百分比用于定义中压情况和低压情况之间的边界。 默认值为 80。 有关 **WorkingSetMaximum** 和配置可用内存的详细信息，请参阅 [为报表服务器应用程序配置可用内存](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)。|N,S|  
|**MemoryThreshold**|指定 **WorkingSetMaximum** 的百分比，该百分比用于定义高压情况和中压情况之间的边界。 默认值为 **90**。 此值应大于为 **MemorySafetyMargin**设置的值。 有关详细信息，请参阅 [为报表服务器应用程序配置可用内存](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)。|N,S|  
|**RecycleTime**|指定应用程序域的回收时间（分钟）。 有效值的范围为 0 到最大整数之间。 默认值为 720。|N,S|  
|**MaxAppDomainUnloadTime**|指定在回收操作期间允许卸载应用程序域的时间间隔。 如果在该时间段内没有完成回收，则应用程序域中的所有处理将会停止。 有关详细信息，请参阅 [Application Domains for Report Server Applications](../../reporting-services/report-server/application-domains-for-report-server-applications.md)。<br /><br /> 以分钟为单位指定此值。 有效值的范围为 0 到最大整数之间。 默认值为 **30**。|N,S|  
|**MaxQueueThreads**|指定报表服务器 Windows 服务同时处理订阅和通知所用的线程数。 有效值的范围为 0 到最大整数之间。 默认值为 0。 如果选择了 0，报表服务器将确定最大的线程数。 如果指定了某个整数，则所指定的值将设置可以同时创建的线程数的上限。 有关报表服务器 Windows 服务如何针对运行中的进程管理内存的详细信息，请参阅 [为报表服务器应用程序配置可用内存](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)。|N,S|  
|**UrlRoot**|此设置由报表服务器传递扩展插件使用，用来编写在电子邮件和文件共享订阅中传递的报表使用的 URL。 它必须是有效的指向报表服务器的 URL 地址，通过该地址可以访问已发布的报表。 报表服务器使用此设置生成供脱机访问或以无人参与方式访问的 URL。 这些 URL 用于导出的报表中，传递扩展插件使用它们来编写包含在传递消息（例如电子邮件中的链接）中的 URL。 报表服务器基于以下行为确定报表中的 URL：<br /><br /> 如果 **UrlRoot** 为空（默认值）且存在 URL 保留项，则报表服务器会自动确定 URL，其方式与 ListReportServerUrls 方法生成 URL 的方式相同。 将使用 ListReportServerUrls 方法返回的第一个 URL。 或者，如果 SecureConnectionLevel 大于零 (0)，则使用第一个 SSL URL。<br /><br /> 如果将 **UrlRoot** 设置为一个特定值，则会使用显式值。<br /><br /> 如果 **UrlRoot** 为空且未配置任何 URL 保留，则所呈现的报表和电子邮件链接中的 URL 是不正确的。|N,S|  
|**UnattendedExecutionAccount**|指定报表服务器运行报表时所使用的用户名、密码和域。 这些值已经过加密。 可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具或 **rsconfig** 实用工具来设置这些值。 有关详细信息，请参阅[配置无人参与的执行帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。<br /><br /> 对于 SharePoint 模式，您使用 SharePoint 管理中心设置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的执行帐户。 有关详细信息，请参阅 [管理 Reporting Services SharePoint 服务应用程序](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)|否|  
|**PolicyLevel**|指定安全策略配置文件。 有效的值为 Rssrvrpolicy.config。 有关详细信息，请参阅 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)。|N,S|  
|**IsWebServiceEnabled**|指定报表服务器 Web 服务是否响应 SOAP 和 URL 访问请求。 在使用基于策略的管理的 Reporting Services 的外围应用配置器方面启用或禁用服务时，设置此值。|N,S|  
|**IsReportManagerEnabled**|从 SQL Server 2016 Reporting Services 累积更新 2 开始已弃用此设置。 Web 门户将始终启用。|否|  
|**FileShareStorageLocation**|指定文件系统中用于存储临时快照的单个文件夹。 尽管可以将文件夹路径指定为 UNC 路径，但不建议您这样做。 默认值为空。<br /><br /> `<FileShareStorageLocation>`<br /><br /> `<Path>`<br /><br /> `</Path>`<br /><br /> `</FileShareStorageLocation>`|N,S|  
|**IsRdceEnabled**|指定是否已启用报表定义自定义扩展插件 (RDCE)。 有效值为 **True** 和 **False**。|N,S|  
  
##  <a name="bkmk_UI"></a> UI（RSReportServer.config 文件）  
 **UI**指定适用于 web 门户应用程序的配置设置。  
  
 以下表的最后一列指示设置是适用于本机模式报表服务器 (N) 还是 SharePoint 模式报表服务器 (S) 或两者均适用。  
  
|设置|Description|模式|  
|-------------|-----------------|----------|  
|**ReportServerUrl**|指定的 web 门户将连接到报表服务器的 URL。 如果你要配置 web 门户来连接到另一个实例中或远程计算机上的报表服务器，仅修改此值。|N,S|  
|**ReportBuilderTrustLevel**|请不要修改此值，它是不可配置的。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以及更高版本中，报表生成器仅在 **FullTrust**下运行。 有关详细信息，请参阅 [配置报表生成器访问权限](../../reporting-services/report-server/configure-report-builder-access.md) 。 有关不再使用的部分信任模式的详细信息，请参阅 [SQL Server 2016 的 SQL Server Reporting Services 中停止使用的功能](../../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)。|N,S|  
|**PageCountMode**|对于仅限 web 门户，此设置指定呈现报表之前，或在查看报表，报表服务器是否计算页计数值。 有效值为 **Estimate** （默认值）和 **Actual**。 在用户查看报表时，使用 **Estimate** 计算页计数信息。 最初，页计数设置为 2（指当前页再加上一页），而当用户在报表中翻页时会上调。 如果您想在显示报表之前提前计算页计数，请使用 **Actual** 。 提供**Actual** 是为了向后兼容。 请注意，如果将 **PageCountMode** 设置为 **Actual**，则系统必须对整个报表进行处理后才能得到有效的页计数，这会增加报表显示之前所需等待的时间。|N,S|  
  
##  <a name="bkmk_extensions"></a> 扩展插件（RSReportServer.config 文件）本机模式  
 **仅对于本机模式** 的报表服务器，“扩展插件”部分才显示在 rsreportserver.config 文件中。 SharePoint 模式的报表服务器的扩展插件信息存储在 SharePoint 配置数据库中，并针对每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序进行配置。  
  
 **扩展插件** 指定以下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装的可扩展模块的配置设置：  
  
-   传递扩展插件  
  
-   DeliveryUI 扩展插件  
  
-   呈现扩展插件  
  
-   数据处理扩展插件  
  
-   语义查询扩展插件（仅内部使用）  
  
-   模型生成扩展插件（仅内部使用）  
  
-   安全扩展插件  
  
-   身份验证扩展插件  
  
-   事件处理扩展插件（仅内部使用）  
  
-   报表定义自定义扩展插件  
  
 上述某些扩展插件严格控制为供报表服务器内部使用。 本文不介绍仅内部使用的扩展插件的配置设置。 以下各节将介绍默认扩展插件的配置设置。 如果您所使用的报表服务器具有自定义的扩展插件，则您的配置文件可能包含此处未介绍的设置。 下面将按扩展插件的显示顺序依次列出。 对于反复出现在同一种扩展插件的多个实例中的设置，我们只介绍一次。  
  
###  <a name="bkmk_extensionsgeneral"></a> 传递扩展插件常规配置  
 指定用于通过订阅传递报表的默认（可能为自定义）传递扩展插件。 RSReportServer.config 文件包含四个传递扩展插件的应用程序设置：  
  
1.  报表服务器电子邮件  
  
2.  文件共享传递。  
  
3.  报表服务器文档库用于在 SharePoint 集成模式下运行的报表服务器。  
  
4.  Null 传递提供程序用于预加载报表缓存。  
  
 有关传递扩展插件的详细信息，请参阅[订阅和传递 (Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
 所有传递扩展插件都具有 **Extension Name**、 **MaxRetries**、 **SecondsBeforeRetry**以及 **Configuration**。 下面首先介绍这些通用的设置， 在第二个表中将介绍特定于扩展插件的设置。  
  
|设置|Description|  
|-------------|-----------------|  
|**Extension Name**|指定传递扩展插件的友好名称和程序集。 不要修改此值。|  
|**MaxRetries**|指定当首次传递尝试操作没有成功时报表服务器进行重试的次数。 默认值为 3。|  
|**SecondsBeforeRetry**|指定每次重试尝试之间的时间间隔（秒）。 默认值为 900。|  
|**Configuration**|包含特定于各传递扩展插件的配置设置。|  
  
####  <a name="bkmk_fileshare_extension"></a> 文件共享传递扩展插件配置设置  
 文件共享传递会将已导出为应用程序文件格式的报表发送到网络上的共享文件夹中。 有关详细信息，请参阅 [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)。  
  
|设置|Description|  
|-------------|-----------------|  
|**ExcludedRenderFormats**， **RenderingExtension**|这些设置用于特意排除那些无法与文件共享传递协同工作的导出格式。 这些格式通常用于交互式报表、预览或预加载报表缓存。 它们无法生成便于桌面应用程序查看的应用程序文件。<br /><br /> HTMLOWC<br /><br /> RGDI<br /><br /> Null|  
  
####  <a name="bkmk_email_extension"></a> 报表服务器电子邮件扩展插件配置设置  
 报表服务器电子邮件使用 SMTP 网络设备向电子邮件地址发送报表。 必须对此传递扩展插件进行配置才能使用。 有关详细信息，请参阅 [针对电子邮件传递配置报表服务器（SSRS 配置管理器）](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83) 和 [Reporting Services 中的电子邮件传递](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)。  
  
|设置|Description|  
|-------------|-----------------|  
|**SMTPServer**|指定用于指示远程 SMTP 服务器或转发器的地址的字符串值。 对于远程 SMTP 服务，必须指定此值。 它可以是 IP 地址、企业 Intranet 上计算机的 UNC 名称或者完全限定域名。|  
|**SMTPServerPort**|指定一个整数值，该值指示 SMTP 服务用来发送外发邮件的端口。 端口 25 通常用于发送电子邮件。|  
|**SMTPAccountName**|包含用于分配 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook Express 帐户名的字符串值。 如果已将 SMTP 服务器配置为以某种方式使用该帐户名，则可设置此值，否则可将此项保留为空白。 使用 **From** 指定用于发送报表的电子邮件帐户。|  
|**SMTPConnectionTimeout**|指定一个整数值，表示与 SMTP 服务的有效套接字连接等待多少秒后才会超时。 默认值为 30 秒，但如果 **SendUsing** 设置为 2，则将忽略此值。|  
|**SMTPServerPickupDirectory**|指定表示本地 SMTP 服务的拾取目录的字符串值。 此值必须为完全限定的本地文件夹路径（例如，d:\rs-emails）。|  
|**SMTPUseSSL**|指定一个布尔值，通过设置该值可以在通过网络发送 SMTP 消息时使用安全套接字层 (SSL)。 默认值为 0（或 False）。 当 **SendUsing** 元素设置为 2 时可以使用此设置。|  
|**SendUsing**|指定发生消息所使用的方法。 有效值为<br /><br /> 1=通过本地 SMTP 服务拾取目录发送消息。<br /><br /> 2=通过网络 SMTP 服务发送消息。|  
|**SMTPAuthenticate**|指定一个整数，表示通过 TCP/IP 连接向 SMTP 服务发送消息时使用的身份验证类型。 有效值为<br /><br /> 0=无身份验证。<br /><br /> 1=（不支持）。<br /><br /> 2= NTLM (NT LanMan) 身份验证。 使用报表服务器 Windows 服务的安全上下文连接到网络 SMTP 服务器。|  
|**From**|指定从其报表格式发送电子邮件地址 *abc@host.xyz* 。 该地址显示在外发电子邮件的“发件人”行中。 如果使用远程 SMTP 服务器，则必须指定此值。 它应该是有权发送邮件的有效电子邮件帐户。|  
|**EmbeddedRenderFormats，RenderingExtension**|指定在电子邮件正文中嵌入报表时所使用的呈现格式。 报表中的图像将随后嵌入报表中。 有效值为 MHTML 和 HTML4.0。|  
|**PrivilegedUserRenderFormats**|指定当通过“管理所有订阅”任务启用订阅时，用户可以从中为报表订阅选择的呈现格式。 如果未设置此值，则可以使用所有未特意排除的呈现格式。|  
|**ExcludedRenderFormats，RenderingExtension**|特意排除无法与给定的传递扩展插件协同工作的格式。 但不能排除同一个呈现扩展插件的多个实例。 如果排除多个实例，则在报表服务器读取配置文件时将出现错误。 默认情况下，排除将下列扩展插件用于电子邮件传递：<br /><br /> HTMLOWC<br /><br /> Null<br /><br /> RGDI|  
|**SendEmailToUserAlias**|此值与 **DefaultHostName**一起使用。<br /><br /> 如果将 **SendEmailToUserAlias** 设置为 **True**，则自动将定义各个订阅的用户指定为报表的收件人。 并隐藏 **“收件人”** 字段。 如果此值为 **False**，则 **“收件人”** 字段可见。 若要最大限度地控制报表分发，请将此值设置为 **True** 。 有效值包括：<br /><br /> **True**= 使用创建订阅的用户的电子邮件地址。 这是默认值。<br /><br /> **False**= 可以指定任何电子邮件地址。|  
|**DefaultHostName**|此值与 **SendEmailToUserAlias**一起使用。<br /><br /> 指定一个字符串值，表示当 **SendEmailToUserAlias** 设置为 True 时追加到用户别名中的主机名。 此值可以为域名系统 (DNS) 名称或 IP 地址。|  
|**PermittedHosts**|通过显式指定哪些主机能够接收电子邮件传递来限制报表分发。 在 **PermittedHosts**中，每个主机均指定为一个 **HostName** 元素，其中值为 IP 地址或 DNS 名称。<br /><br /> 只有为这些主机定义的电子邮件帐户才是有效的收件人。 如果指定 **DefaultHostName**，请确保在 **PermittedHosts** 的 **HostName**元素中包括该主机。 此值必须是一个或多个 DNS 名称或 IP 地址。 默认情况下，不设置此值。 如果未设置该值，则对于可接收通过电子邮件发送的报表的用户没有任何限制。|  
  
####  <a name="bkmk_documentlibrary_extension"></a> 报表服务器 SharePoint 文档库扩展插件配置  
 报表服务器文档库会将已导出为应用程序文件格式的报表发送到文档库中。 只有配置为在 SharePoint 集成模式下运行的报表服务器才能使用此传递扩展插件。 有关详细信息，请参阅 [SharePoint Library Delivery in Reporting Services](../../reporting-services/subscriptions/sharepoint-library-delivery-in-reporting-services.md)。  
  
|设置|Description|  
|-------------|-----------------|  
|**ExcludedRenderFormats，RenderingExtension**|这些设置用于特意排除那些无法与文档库传递协同工作的导出格式。 HTMLOWC、RGDI 和 Null 传递扩展插件都被排除。 这些格式通常用于交互式报表、预览或预加载报表缓存。 它们无法生成便于桌面应用程序查看的应用程序文件。|  
  
####  <a name="bkmk_null_extension"></a> NULL 传递扩展插件配置  
 NULL 传递提供程序用于为单个用户预生成的报表预加载缓存。 对于此传递扩展插件，没有相应的配置设置。 有关详细信息，请参阅 [缓存报表 (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)版本中预加载缓存的唯一方法。  
  
###  <a name="bkmk_ui"></a> 传递 UI 扩展插件常规配置  
 指定包含在 web 门户中定义单独的订阅时使用的订阅定义页中显示用户界面组件的传递扩展插件。 如果你创建和部署自定义传递扩展插件具有用户定义的选项和你想要使用 web 门户，你必须在此节中注册的传递扩展插件。 默认情况下，存在报表服务器电子邮件和报表服务器文件共享的配置设置。 仅用于数据驱动订阅或 SharePoint 应用程序页的传递扩展插件不具有此处的设置。  
  
|设置|Description|  
|-------------|-----------------|  
|**DefaultDeliveryExtension**|此设置可确定哪个传递扩展插件会最先出现在订阅定义页的传递类型列表中。 仅一个传递扩展插件可包含此设置。 有效值包括 **True** 或 **False**。 如果此值设置为 **True**，则相应扩展插件为默认选项。|  
|**Configuration**|指定传递扩展插件的配置选项。 可以设置每个传递扩展插件的默认呈现格式。 有效值为 rsreportserver.config 文件的呈现部分中描述的呈现扩展名。|  
|**DefaultRenderingExtension**|指定传递扩展插件是否为默认值。 报表服务器电子邮件是默认的传递扩展插件。 有效值包括 **True** 或 **False**。 如果多个扩展插件包含 **True**值，则将第一个扩展插件视为默认扩展插件。|  
  
###  <a name="bkmk_rendering"></a> 呈现扩展插件常规配置  
 指定用于呈现报表的默认（可能为自定义）呈现扩展插件。  
  
 除非部署自定义的呈现扩展插件，否则不要修改此部分。 有关详细信息，请参阅 [Implementing a Rendering Extension](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)。  
  
 默认呈现扩展插件包含以下内容：  
  
-   XML  
  
-   Null  
  
-   CSV  
  
-   PDF  
  
-   RGDI  
  
-   HTML4.0  
  
-   MHTML  
  
-   EXCEL  
  
-   RPL  
  
-   IMAGE  
  
 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本开始，默认情况下 MHTML 和 HTML 4.0 呈现包含以下设备信息设置用于控制调整数据可视化大小的行为。  
  
```  
<DeviceInfo><DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing></DeviceInfo>  
```  
  
 有关 DeviceInfo 设置的详细信息，请参阅以下主题：  
  
-   [MHTML 设备信息设置](../../reporting-services/mhtml-device-information-settings.md)  
  
-   [HTML 设备信息设置](../../reporting-services/html-device-information-settings.md)  
  
-   [呈现扩展插件的设备信息设置 (Reporting Services)](../../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md)  
  
 有关特性的信息的子**\<扩展 >**元素下的**\<呈现 >**，请参阅以下：  
  
-   [在 RSReportServer.Config 中自定义呈现扩展插件参数](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
-   [部署呈现扩展插件](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
 除非部署自定义的呈现扩展插件，否则不要修改此部分。 有关详细信息，请参阅 [Implementing a Rendering Extension](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)。  
  
###  <a name="bkmk_data"></a> 数据扩展插件常规配置  
 指定用于处理查询的默认（可能为自定义）数据处理扩展插件。 默认数据处理扩展插件包含以下内容：  
  
-   SQL  
  
-   SQLAZURE  
  
-   SQLPDW  
  
-   OLEDB  
  
-   OLEDB-MD  
  
-   ORACLE  
  
-   ODBC  
  
-   XML  
  
-   SHAREPOINTLIST  
  
-   SAPBW  
  
-   ESSBASE  
  
-   TERADATA  
  
 除非要添加自定义数据处理插件，否则不要修改此部分。 有关详细信息，请参阅 [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)。  
  
###  <a name="bkmk_semantic"></a> 语义查询扩展插件常规配置  
 指定用于处理报表模型的语义查询处理扩展插件。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 附带的语义查询处理扩展插件支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系数据、Oracle 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维数据。 请不要修改此部分。 查询处理是不可扩展的。  
  
###  <a name="bkmk_model"></a> 模型生成配置  
 指定用于从报表服务器上已发布的共享数据源创建报表模型的模型生成扩展插件。 可以从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系数据、Oracle 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维数据源生成模型。 请不要修改此部分。 模型生成是不可扩展的。  
  
###  <a name="bkmk_security"></a> 安全扩展插件配置  
 指定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]所用的授权组件。 该组件由 RSReportServer.config 文件的 **Authentication** 元素中注册的身份验证扩展插件使用。 除非要实现自定义的身份验证扩展插件，否则不要修改此部分。 有关添加自定义安全功能的详细信息，请参阅 [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)。 有关授权的详细信息，请参阅 [Authorization in Reporting Services](../../reporting-services/extensions/security-extension/authorization-in-reporting-services.md)。  
  
###  <a name="bkmk_authentication"></a> 身份验证扩展插件配置  
 指定报表服务器使用的默认和自定义身份验证扩展插件。 默认的扩展插件基于 Windows 身份验证。 除非要实现自定义的身份验证扩展插件，否则不要修改此部分。 有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的身份验证的详细信息，请参阅 [Reporting Services 中的身份验证](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md) 和 [针对报表服务器的身份验证](../../reporting-services/security/authentication-with-the-report-server.md)。 有关添加自定义安全功能的详细信息，请参阅 [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)。  
  
###  <a name="bkmk_eventprocessing"></a> 事件处理  
 指定默认的事件处理程序。 请不要修改此部分。 此部分不可扩展。  
  
###  <a name="bkmk_reportdefinition"></a> 报表定义自定义  
 指定修改报表定义的自定义扩展插件的名称和类型。  
  
###  <a name="bkmk_rdlsandboxing"></a> RDLSandboxing  
 指定报表定义语言 (RDL) 模式，该模式可帮助您在多个用户共享报表服务器的单个 Web 场的情况下检测到和限制单个用户使用的特定类型的报表资源。 有关详细信息，请参阅 [Enable and Disable RDL Sandboxing](../../reporting-services/report-server-sharepoint/enable-and-disable-rdl-sandboxing.md)。  
  
##  <a name="bkmk_MapTileServer"></a> MapTileServerConfiguration（RSReportServer.config 文件）  
 **MapTileServerConfiguration** 为 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 必应地图 Web 服务定义配置设置，而该 Web 服务为在报表服务器上发布的报表中的某个地图报表项提供图块背景。 所有子元素都是必需的。  
  
|设置|Description|  
|-------------|-----------------|  
|**MaxConnections**|指定与 Bing 地图 Web 服务之间的最大连接数。|  
|**超时**|指定从 Bing 地图 Web 服务等待响应时的超时（秒）。|  
|**AppID**|指定要用于 Bing 地图 Web 服务的应用程序标识符 (AppID)。 **(Default)** 指定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 默认 AppID。<br /><br /> 有关在报表中使用 Bing 地图图块的详细信息，请参阅 [其他使用条款](http://go.microsoft.com/fwlink/?LinkId=151371)。<br /><br /> 请勿更改此值，除非您必须为您自己的 Bing 地图许可协议指定自定义 AppID。 当您更改 AppID 时，不必重新启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，更改就可以生效。|  
|**CacheLevel**|从 System.Net.Cache 的 HttpRequestCacheLevel 枚举指定一个值。 默认值为 **Default**。 有关详细信息，请参阅 [HttpRequestCacheLevel 枚举](http://go.microsoft.com/fwlink/?LinkId=153353)。|  
  
##  <a name="bkmk_nativedefaultfile"></a> 本机模式报表服务器的默认配置文件  
 默认情况下，rsreportserver.config 文件安装到以下位置：  
  
 **C:\Program Files\Microsoft SQL Server\MSRS13。MSSQLSERVER\Reporting Services\ReportServer**  
  
```  
<Configuration>
    <Dsn>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAR58DMGebHUeMvyR6HR04kQQAAAAiAAAAUgBlAHAAbwBy
AHQAaQBuAGcAIABTAGUAcgB2AGUAcgAAAANmAADAAAAAEAAAADczfLRgZ4GF44iBHkLrKY4AAAAA
BIAAAKAAAAAQAAAAJ9wQOmDNauH+LS30rboJ2OAAAAAp0kiFFBrc3r3ypKaldZJtjCORX9LTZRzt
0/JCSVIZc4GXx0peGKqd+f85UyrY/KOyUSHogOC/XoBp9Ppxv6ITbdunsS/LXEcMUBVqEdQD4ylh
x6K1NTC/u8hl9v0MgK+xMQKaiV7BuNYbgGgkaViABcNH0xVzcc5rMTHUkrABbGDFGKyAFniGQ1qu
/rqHibNNyvYbP/2uiqvgC0tQl6u8VkVbXpWrkvO+bFCqxlaJlCoDc2f3rIO321SZEvoFbsYNgPLd
+mIAkSCnH3Z3gm/bI8bqVkFaHblKyQuSfFsi6RQAAACb87b26dV0GjHmMJnE0Tk8CzNmhg==</Dsn>
    <ConnectionType>Default</ConnectionType>
    <LogonUser></LogonUser>
    <LogonDomain></LogonDomain>
    <LogonCred></LogonCred>
    <InstanceId>MSRS13.MSSQLSERVER</InstanceId>
    <InstallationID>{cd920604-a5c7-4554-b2a0-aadc04312fe5}</InstallationID>
    <Add Key="SecureConnectionLevel" Value="0"/>
    <Add Key="DisableSecureFormsAuthenticationCookie" Value="false"/>
    <Add Key="CleanupCycleMinutes" Value="10"/>
    <Add Key="MaxActiveReqForOneUser" Value="20"/>
    <Add Key="DatabaseQueryTimeout" Value="120"/>
    <Add Key="RunningRequestsScavengerCycle" Value="60"/>
    <Add Key="RunningRequestsDbCycle" Value="60"/>
    <Add Key="RunningRequestsAge" Value="30"/>
    <Add Key="MaxScheduleWait" Value="5"/>
    <Add Key="DisplayErrorLink" Value="true"/>
    <Add Key="WebServiceUseFileShareStorage" Value="false"/>
    <!--  <Add Key="ProcessTimeout" Value="150" /> -->
    <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->
    <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->
    <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->
    <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->
    <Add Key="WatsonFlags" Value="0x0428"/>
    <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException"/>
    <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException,System.AppDomainUnloadedException"/>
    <URLReservations>
        <Application>
            <Name>ReportServerWebService</Name>
            <VirtualDirectory>ReportServer</VirtualDirectory>
            <URLs>
                <URL>
                    <UrlString>http://+:80</UrlString>
                    <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>
                    <AccountName>NT SERVICE\ReportServer</AccountName>
                </URL>
            </URLs>
        </Application>
        <Application>
            <Name>ReportServerWebApp</Name>
            <VirtualDirectory>Reports</VirtualDirectory>
            <URLs>
                <URL>
                    <UrlString>http://+:80</UrlString>
                    <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>
                    <AccountName>NT SERVICE\ReportServer</AccountName>
                </URL>
            </URLs>
        </Application>
    </URLReservations>
    <Authentication>
        <AuthenticationTypes>
            <RSWindowsNTLM/>
        </AuthenticationTypes>
        <RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>
        <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>
        <EnableAuthPersistence>true</EnableAuthPersistence>
    </Authentication>
    <Service>
        <IsSchedulingService>True</IsSchedulingService>
        <IsNotificationService>True</IsNotificationService>
        <IsEventService>True</IsEventService>
        <PollingInterval>10</PollingInterval>
        <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>
        <MemorySafetyMargin>80</MemorySafetyMargin>
        <MemoryThreshold>90</MemoryThreshold>
        <RecycleTime>720</RecycleTime>
        <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>
        <MaxQueueThreads>0</MaxQueueThreads>
        <UrlRoot>
        </UrlRoot>
        <UnattendedExecutionAccount>
            <UserName></UserName>
            <Password></Password>
            <Domain></Domain>
        </UnattendedExecutionAccount>
        <PolicyLevel>rssrvpolicy.config</PolicyLevel>
        <IsWebServiceEnabled>True</IsWebServiceEnabled>
        <IsReportManagerEnabled>True</IsReportManagerEnabled>
        <FileShareStorageLocation>
            <Path>
            </Path>
        </FileShareStorageLocation>
        <DefaultFileShareAccount>
            <Domain></Domain>
            <UserName></UserName>
            <Password></Password>
        </DefaultFileShareAccount>
    </Service>
    <UI>
        <ReportServerUrl>
        </ReportServerUrl>
        <PageCountMode>Estimate</PageCountMode>
    </UI>
    <Extensions>
        <Delivery>
            <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider,ReportingServicesFileShareDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <FileShareConfiguration>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                    </FileShareConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider,ReportingServicesEmailDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <RSEmailDPConfiguration>
                        <SMTPServer></SMTPServer>
                        <SMTPServerPort>
                        </SMTPServerPort>
                        <SMTPAccountName>
                        </SMTPAccountName>
                        <SMTPConnectionTimeout>
                        </SMTPConnectionTimeout>
                        <SMTPServerPickupDirectory>
                        </SMTPServerPickupDirectory>
                        <SMTPUseSSL>False</SMTPUseSSL>
                        <SendUsing>2</SendUsing>
                        <SMTPAuthenticate>0</SMTPAuthenticate>
                        <SendUserName></SendUserName>
                        <SendPassword></SendPassword>
                        <From></From>
                        <EmbeddedRenderFormats>
                            <RenderingExtension>MHTML</RenderingExtension>
                        </EmbeddedRenderFormats>
                        <PrivilegedUserRenderFormats>
                        </PrivilegedUserRenderFormats>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                        <SendEmailToUserAlias>True</SendEmailToUserAlias>
                        <DefaultHostName>
                        </DefaultHostName>
                        <PermittedHosts>
                        </PermittedHosts>
                    </RSEmailDPConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server DocumentLibrary" Type="Microsoft.ReportingServices.SharePoint.SharePointDeliveryExtension.DocumentLibraryProvider,ReportingServicesSharePointDeliveryExtension">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <DocumentLibraryConfiguration>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                    </DocumentLibraryConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="NULL" Type="Microsoft.ReportingServices.NullDeliveryProvider.NullProvider,ReportingServicesNullDeliveryProvider"/>
            <Extension Name="Report Server PowerBI" Type="Microsoft.ReportingServices.PowerBIDeliveryProvider.PowerBIDeliveryProvider,ReportingServicesPowerBIDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <PowerBIDeliveryConfiguration>
                    </PowerBIDeliveryConfiguration>
                </Configuration>
            </Extension>
        </Delivery>
        <DeliveryUI>
            <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">
                <DefaultDeliveryExtension>True</DefaultDeliveryExtension>
                <Configuration>
                    <RSEmailDPConfiguration>
                        <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>
                    </RSEmailDPConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>
            <Extension Name="Report Server PowerBI" Type="Microsoft.ReportingServices.PowerBIDeliveryProvider.PowerBIDeliveryUIControl,ReportingServicesPowerBIDeliveryProvider"/>
        </DeliveryUI>
        <Render>
            <Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>
            <Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>
            <Extension Name="EXCELOPENXML" Type="Microsoft.ReportingServices.Rendering.ExcelOpenXmlRenderer.ExcelOpenXmlRenderer,Microsoft.ReportingServices.ExcelRendering"/>
            <Extension Name="EXCEL" Type="Microsoft.ReportingServices.Rendering.ExcelRenderer.ExcelRenderer,Microsoft.ReportingServices.ExcelRendering" Visible="false"/>
            <Extension Name="PPTX" Type="Microsoft.ReportingServices.Rendering.PowerPointRendering.PptxRenderingExtension,Microsoft.ReportingServices.PowerPointRendering"/>
            <Extension Name="PDF" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.PDFRenderer,Microsoft.ReportingServices.ImageRendering"/>
            <Extension Name="IMAGE" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering"/>
            <Extension Name="MHTML" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.MHtmlRenderingExtension,Microsoft.ReportingServices.HtmlRendering">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="CSV" Type="Microsoft.ReportingServices.Rendering.DataRenderer.CsvReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="ATOM" Type="Microsoft.ReportingServices.Rendering.DataRenderer.AtomDataReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="NULL" Type="Microsoft.ReportingServices.Rendering.NullRenderer.NullReport,Microsoft.ReportingServices.NullRendering" Visible="false"/>
            <Extension Name="RGDI" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.RGDIRenderer,Microsoft.ReportingServices.ImageRendering" Visible="false"/>
            <Extension Name="HTML4.0" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.Html40RenderingExtension,Microsoft.ReportingServices.HtmlRendering" Visible="false">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="HTML5" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.Html5RenderingExtension,Microsoft.ReportingServices.HtmlRendering" Visible="false">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="RPL" Type="Microsoft.ReportingServices.Rendering.RPLRendering.RPLRenderer,Microsoft.ReportingServices.RPLRendering" Visible="false" LogAllExecutionRequests="false"/>
        </Render>
        <!--
        For the SQLPDW extension to work, install the SQL Server PDW Client Tools on the report server.
        NOTE: The SQLPDW extension is deprecated. It supports old versions of SQL Server Parallel Data Warehouse (PDW).        
        To connect to Analytics Platform System, use the SQL (SQL Server) extension.        
        For the ORACLE extension to work, install the Oracle Data Provider for NET (ODP.NET) on the report server.
        For TERADATA extension to work, install the .NET Provider for Teradata on the report server.
      -->
        <Data>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.DataExtensions.SqlConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.DataExtensions.SqlAzureConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.DataExtensions.SqlDwConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="OLEDB-MD" Type="Microsoft.ReportingServices.DataExtensions.AdoMdConnection,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SHAREPOINTLIST" Type="Microsoft.ReportingServices.DataExtensions.SharePointList.SPListConnection,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.DataExtensions.OracleClientConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ESSBASE" Type="Microsoft.ReportingServices.DataExtensions.Essbase.EssbaseConnection,Microsoft.ReportingServices.DataExtensions.Essbase"/>
            <Extension Name="SAPBW" Type="Microsoft.ReportingServices.DataExtensions.SapBw.SapBwConnection,Microsoft.ReportingServices.DataExtensions.SapBw"/>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.DataExtensions.TeradataConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="OLEDB" Type="Microsoft.ReportingServices.DataExtensions.OleDbConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ODBC" Type="Microsoft.ReportingServices.DataExtensions.OdbcConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="XML" Type="Microsoft.ReportingServices.DataExtensions.XmlDPConnection,Microsoft.ReportingServices.DataExtensions"/>
        </Data>
        <SemanticQuery>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQLADW.MSSqlAdwSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>True</EnableMathOpCasting>
                    <DisableNO_MERGEInLeftOuters>False</DisableNO_MERGEInLeftOuters>
                    <EnableUnistr>False</EnableUnistr>
                    <DisableTSTruncation>False</DisableTSTruncation>
                </Configuration>
            </Extension>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>True</EnableMathOpCasting>
                    <ReplaceFunctionName>oREPLACE</ReplaceFunctionName>
                </Configuration>
            </Extension>
            <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.QueryExecution.ASSemanticQueryCommand,Microsoft.AnalysisServices.Modeling"/>
        </SemanticQuery>
        <ModelGeneration>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.Generation.ModelGeneratorExtention,Microsoft.AnalysisServices.Modeling"/>
        </ModelGeneration>
        <Security>
            <Extension Name="Windows" Type="Microsoft.ReportingServices.Authorization.WindowsAuthorization, Microsoft.ReportingServices.Authorization"/>
        </Security>
        <Authentication>
            <Extension Name="Windows" Type="Microsoft.ReportingServices.Authentication.WindowsAuthentication, Microsoft.ReportingServices.Authorization"/>
        </Authentication>
        <EventProcessing>
            <Extension Name="SnapShot Extension" Type="Microsoft.ReportingServices.Library.HistorySnapShotCreatedHandler,ReportingServicesLibrary">
                <Event>
                    <Type>ReportHistorySnapshotCreated</Type>
                </Event>
            </Extension>
            <Extension Name="Timed Subscription Extension" Type="Microsoft.ReportingServices.Library.TimedSubscriptionHandler,ReportingServicesLibrary">
                <Event>
                    <Type>TimedSubscription</Type>
                </Event>
            </Extension>
            <Extension Name="Cache Refresh Plan Extension" Type="Microsoft.ReportingServices.Library.CacheRefreshPlanHandler,ReportingServicesLibrary">
                <Event>
                    <Type>RefreshCache</Type>
                </Event>
            </Extension>
            <Extension Name="Shared Dataset Cache Update Extension" Type="Microsoft.ReportingServices.Library.SharedDatasetCacheUpdatePlanHandler,ReportingServicesLibrary">
                <Event>
                    <Type>SharedDatasetCacheUpdate</Type>
                </Event>
            </Extension>
            <Extension Name="Cache Update Extension" Type="Microsoft.ReportingServices.Library.ReportExecutionSnapshotUpdateEventHandler,ReportingServicesLibrary">
                <Event>
                    <Type>SnapshotUpdated</Type>
                </Event>
            </Extension>
        </EventProcessing>
    </Extensions>
    <MapTileServerConfiguration>
        <MaxConnections>2</MaxConnections>
        <Timeout>10</Timeout>
        <AppID>(Default)</AppID>
        <CacheLevel>Default</CacheLevel>
    </MapTileServerConfiguration>
</Configuration> 
```  
  
##  <a name="bkmk_sharepointdefaultfile"></a> SharePoint 模式报表服务器的默认配置文件  
 默认情况下，rsreportserver.config 文件安装到以下位置：  
  
 **C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting**  
  
```  
<Configuration>  
  <Dsn />  
  <ConnectionType>Default</ConnectionType>  
  <LogonUser>  
  </LogonUser>  
  <LogonDomain>  
  </LogonDomain>  
  <LogonCred>  
  </LogonCred>  
  <InstanceId>MSRS12.@Sharepoint</InstanceId>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="CleanupCycleMinutes" Value="10" />  
  <Add Key="MaxActiveReqForOneUser" Value="20" />  
  <Add Key="AlertingCleanupCycleMinutes" Value="20" />  
  <Add Key="AlertingDataCleanupMinutes" Value="360" />  
  <Add Key="AlertingExecutionLogCleanupMinutes" Value="10080" />  
  <Add Key="AlertingMaxDataRetentionDays" Value="180" />  
  <Add Key="RunningRequestsScavengerCycle" Value="60" />  
  <Add Key="RunningRequestsDbCycle" Value="60" />  
  <Add Key="RunningRequestsAge" Value="30" />  
  <Add Key="MaxScheduleWait" Value="5" />  
  <Add Key="DisplayErrorLink" Value="true" />  
  <Add Key="WebServiceUseFileShareStorage" Value="false" />  
  <!--  <Add Key="ProcessTimeout" Value="150" /> -->  
  <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->  
  <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->  
  <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->  
  <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->  
  <Add Key="WatsonFlags" Value="0x0428" />  
  <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException" />  
  <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException" />  
  <RStrace>  
    <add name="FileName" value="ReportServerService" />  
    <add name="FileSizeLimitMb" value="32" />  
    <add name="KeepFilesForDays" value="14" />  
    <add name="Prefix" value="tid, time" />  
    <add name="TraceListeners" value="file" />  
    <add name="TraceFileMode" value="unique" />  
    <add name="Components" value="all:3" />  
  </RStrace>  
  <URLReservations>  
    <Application>  
      <Name>ReportServerWebService</Name>  
      <VirtualDirectory>ReportServer</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
    <Application>  
      <Name>ReportManager</Name>  
      <VirtualDirectory>Reports</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
  </URLReservations>  
  <Authentication>  
    <AuthenticationTypes>  
      <RSWindowsNTLM />  
    </AuthenticationTypes>  
    <EnableAuthPersistence>true</EnableAuthPersistence>  
  </Authentication>  
  <Service>  
    <IsSchedulingService>True</IsSchedulingService>  
    <IsNotificationService>True</IsNotificationService>  
    <IsEventService>True</IsEventService>  
    <IsAlertingService>True</IsAlertingService>  
    <PollingInterval>10</PollingInterval>  
    <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>  
    <MemorySafetyMargin>80</MemorySafetyMargin>  
    <MemoryThreshold>90</MemoryThreshold>  
    <RecycleTime>720</RecycleTime>  
    <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>  
    <MaxQueueThreads>0</MaxQueueThreads>  
    <UrlRoot>  
    </UrlRoot>  
    <PolicyLevel>rssrvpolicy.config</PolicyLevel>  
    <IsWebServiceEnabled>True</IsWebServiceEnabled>    
    <FileShareStorageLocation>  
      <Path>  
      </Path>  
    </FileShareStorageLocation>  
  </Service>  
  <UI>  
    <ReportServerUrl>  
    </ReportServerUrl>  
    <PageCountMode>Estimate</PageCountMode>  
  </UI>  
  <MapTileServerConfiguration>  
    <MaxConnections>2</MaxConnections>  
    <Timeout>10</Timeout>  
    <AppID>(Default)</AppID>  
    <CacheLevel>Default</CacheLevel>  
  </MapTileServerConfiguration>  
</Configuration>  
```  
  
## <a name="see-also"></a>另请参阅  
 [修改 Reporting Services 配置文件 (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [为报表服务器应用程序配置可用内存](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)   
 [Reporting Services 配置文件](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [初始化 Report Server（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [存储加密的 Report Server 数据（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services Configuration Manager（本机模式）](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
 更多问题？ [尝试的 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
  
  

