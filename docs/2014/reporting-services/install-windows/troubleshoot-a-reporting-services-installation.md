---
title: 排除 Reporting Services 安装故障 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e2536f7f-d90c-4571-9ffd-6bbfe69018d6
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 95b88a3ad52ebce063a545f07e16cabb9ef00011
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129845"
---
# <a name="troubleshoot-a-reporting-services-installation"></a>排除 Reporting Services 安装故障
  如果由于安装期间出现错误而导致无法安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，请使用本主题中的说明来解决最有可能导致安装错误的情况。  
  
 有关问题的最新信息[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，请参阅[Reporting Services SQL Server 2012 提示、 技巧和故障排除](http://go.microsoft.com/fwlink/?LinkId=221297)  
  
 有关和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 相关的其他错误和问题的信息，请参阅 [解决 SSRS 问题和错误](http://social.technet.microsoft.com/wiki/contents/articles/ssrs-troubleshooting-issues-and-errors.aspx)。  
  
 查看 [联机发行说明](http://go.microsoft.com/fwlink/?linkid=236893) ，也许在发行说明中会论及您遇到的问题。  
  
 本主题包含以下信息：  
  
-   [检查安装程序日志](#bkmk_setuplogs)  
  
-   [检查必备项](#bkmk_prereq)  
  
-   [排除 SharePoint 模式安装问题](#bkmk_tshoot_sharepoint)  
  
-   [排除本机模式安装问题](#bkmk_tshoot_native)  
  
-   [Additional Resources](#bkmk_additional)  
  
##  <a name="bkmk_setuplogs"></a> 检查安装程序日志  
 安装程序错误记录在日志文件**程序 Files\Microsoft SQL Server\110\Setup Bootstrap\Log**文件夹。 每次运行安装程序时都会创建一个子文件夹。 该子文件夹名称为您运行安装程序的时间和日期。 有关如何查看安装程序日志文件的说明，请参阅 [查看和阅读 SQL Server 安装程序日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
-   该日志文件包括文件集合。  
  
-   打开 *_summary.txt 文件可查看产品、组件和实例信息。  
  
-   打开 *_errorlog.txt 文件可查看安装期间生成的错误信息。  
  
-   打开 *_RS\_\*_ComponentUpdateSetup.log 以查看 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装程序信息。  
  
##  <a name="bkmk_prereq"></a> 检查系统必备条件  
 安装程序会自动检查系统必备条件。 不过，如果要排除安装中的问题，则了解安装程序将检查哪些条件非常有用。  
  
-   运行安装程序的帐户要求包括本地 Administrators 组中的成员身份。 安装程序必须具有添加文件的权限、注册表设置权限、创建本地安全组权限和设置权限。 如果要在安装时采用默认配置，安装程序必须具有在所安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上创建报表服务器数据库的权限。  
  
-   操作系统必须支持 HTTP.SYS 1.1。  
  
-   HTTP 服务必须已启用并正在运行。  
  
-   如果还要安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务，则必须运行分布式事务处理协调器 (DTC)。  
  
-   System32 文件夹中必须存在 Authz.dll。  
  
 安装程序不再检查 Internet Information Services (IIS) 或 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 需要 MDAC 2.0 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 版；如果尚未安装这些组件，则安装程序将会安装它们。  
  
##  <a name="bkmk_tshoot_sharepoint"></a> 排除 SharePoint 模式安装问题  
  
-   [Reporting Services 配置管理器不启动](#bkmk_configmanager_notstart)  
  
-   [在 SharePoint 模式下安装 SQL Server 2012 SSRS 后没有看到 SharePoint 管理中心中的 SQL Server Reporting Services 服务](#bkmk_no_ssrs_service)  
  
-   [Reporting Services PowerShell cmdlet 不可用，并且命令无法识别](#bkmk_cmdlets_not_recognized)  
  
-   [您将会看到一则错误消息，指示 URL 未配置](#bkmk_URL_not_configured)  
  
-   [在安装有但未配置 SharePoint 的计算机上进行安装时安装程序将失败](#bkmk_sharepoint_not_confiugred)  
  
-   [SharePoint 管理中心页空白](#bkmk_central_admin_blank)  
  
-   [当您尝试创建新的报表生成器报表时，您会看到一条错误消息](#bkmk_reportbuilder_newreport_error)  
  
-   [您看到一条指示 PREPAREIMAGE 不支持 RS_SHP 的错误消息](#bkmk_RS_SHP_notsupported)  
  
###  <a name="bkmk_configmanager_notstart"></a> Reporting Services 配置管理器不启动  
 **说明：** 此问题是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的设计问题。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 现在是为 SharePoint 服务体系结构而设计的。 在 SharePoint 模式下配置和管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不再需要配置管理器。  
  
 **解决方法：** 使用 SharePoint 管理中心在 SharePoint 模式中配置报表服务器。 有关详细信息，请参阅 [管理 Reporting Services SharePoint 服务应用程序](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
###  <a name="bkmk_no_ssrs_service"></a> 在 SharePoint 模式下安装 SQL Server 2012 SSRS 后没有看到 SharePoint 管理中心中的 SQL Server Reporting Services 服务  
 **描述：** 成功安装后的如果[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在 SharePoint 模式下与[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]外接程序对于 SharePoint 2010，你在看不到"SQL Server Reporting Services"下面的两个菜单，然后[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]尚未注册服务：  
  
-   SharePoint 2010 管理中心 ->“应用程序管理”->“管理服务器上的服务”页  
  
-   SharePoint 2010 管理中心 ->“应用程序管理”->“管理服务应用程序”->“新建”菜单  
  
 **解决方法：** 注册并启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint Services，完成以下操作：  
  
1.  在运行 SharePoint 2010 管理中心的计算机上  
  
    1.  使用管理员权限打开 SharePoint 2010 Management Shell。 右键单击图标，然后单击“以管理员身份运行”。 从 shell 运行以下三个 cmdlet：  
  
    2.  ```  
        Install-SPRSService  
        ```  
  
    3.  ```  
        Install-SPRSServiceProxy  
        ```  
  
    4.  ```  
        Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
        ```  
  
2.  验证[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服务的状态显示为"**已启动**"页面上： SharePoint 2010 中部管理->"**应用程序管理**"->"**上的管理服务服务器**"  
  
###  <a name="bkmk_cmdlets_not_recognized"></a> Reporting Services PowerShell cmdlet 不可用，并且命令无法识别  
 **说明：** 当您尝试运行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] PowerShell cmdlet 时，您会看到如下的错误消息：  
  
-   术语“Install-SPRSServiceInstall-SPRSService” **无法识别** 作为 cmdlet、函数、脚本文件或可操作程序的名称。 请检查该名称的拼写是否正确，或者如果包含路径，则确认该路径正确并重试。At line:1 char:39+ Install-SPRSServiceInstall-SPRSService <<<<    + CategoryInfo          : ObjectNotFound: (Install-SPRSServiceInstall-SPRSService:String) [], CommandNotFoundExcep  
  
 **解决方法：** 完成以下操作之一：  
  
-   运行用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序。 **rssharepoint.msi**。  
  
-   从 SQL Server 安装介质安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。  
  
 **注意：** 如果在您完成上述解决方法之一时 **SharePoint 2013 Management Shell** 是打开的，则关闭后再重新打开该 Management shell。  
  
 有关详细信息，请参见以下内容：  
  
-   [在何处查找用于 SharePoint 产品的 Reporting Services 外接程序](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [安装用于 SharePoint 2010 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
-   [安装适用于 SharePoint 2013 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
###  <a name="bkmk_URL_not_configured"></a> 您将会看到一则错误消息，指示 URL 未配置  
 **说明** ：你会看到如下错误消息：  
  
 不支持此 SQL Server Reporting Services (SSRS) 功能。 使用管理中心可验证和修复以下一个或多个问题：•报表服务器 URL 未配置。 使用“SSRS 集成”页可以设置该 URL。•SSRS 服务应用程序代理未配置。 使用 SSRS 服务应用程序页可以配置该代理。•该 SSRS 服务应用程序未映射到此 Web 应用程序。 使用 SSRS 服务应用程序页可以将该 SSRS 服务应用程序代理与此 Web 应用程序的应用程序代理组相关联。  
  
 **解决方法：** 错误消息包含三个建议的步骤来纠正此问题。 “报表服务器 URL 未配置...”消息中的第一个建议 在与 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]之前的报表服务器版本集成时相关。 使用 **SQL Server Reporting Services (2008 和 2008 R2)** 在 **常规应用程序设置**页上完成针对以前报表服务器版本的 SharePoint 配置。  
  
 **更多信息：** 在您尝试使用要求连接到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务的任何 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能时将看到此错误消息。 这包括：  
  
-   从 SharePoint 文档库中打开 SQL Server 报表生成器。  
  
-   管理订阅。  
  
-   管理服务应用程序。  
  
###  <a name="bkmk_sharepoint_not_confiugred"></a> 在安装有但未配置 SharePoint 的计算机上进行安装时安装程序将失败  
 **说明：** 如果选择在安装有但未配置 SharePoint 的计算机上安装 Reporting Services SharePoint 模式，则将看到一条类似于以下内容的消息，而且安装程序将停止运行：  
  
 SQL Server 安装程序已停止工作  
  
 **解决方法：** 配置 SharePoint，然后运行 SQL Server 安装。  
  
 **更多信息：** 将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装到现有 SharePoint 安装中时，安装程序会尝试安装并启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 服务。 如果未配置 SharePoint，服务安装将失败，从而导致安装程序失败。  
  
###  <a name="bkmk_central_admin_blank"></a> SharePoint 管理中心页空白  
 **说明：** 您能够成功地安装 SharePoint 2010，而不出现任何安装错误。 但是，当您浏览到管理中心时，您仅看到空白页：  
  
 **解决方法：** 此问题不是特定于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，但与整体 SharePoint 安装中的权限配置有关。 下面是建议列表：  
  
-   查看有关开发环境的 SharePoint 主题。 [设置开发环境用于 SharePoint 2010 上 Windows Vista、 Windows 7 和 Windows Server 2008](http://msdn.microsoft.com/library/ee554869\(office.14\).aspx)  
  
-   查阅论坛帖子： [在 Windows 7 上进行安装后管理中心返回空白页](http://social.technet.microsoft.com/Forums/en/sharepoint2010setup/thread/a422a3c8-39f6-4b9e-988a-4c4d1e745694)  
  
-   您用于 SharePoint 2010 管理中心服务等 SharePoint 服务的服务帐户在本地操作系统中应具有管理权限。  
  
###  <a name="bkmk_reportbuilder_newreport_error"></a> 当您尝试创建新的报表生成器报表时，您会看到一条错误消息  
 **说明：** 当您尝试在文档库内创建报表生成器报表时您会看到一条类似于以下内容的错误消息：  
  
 不支持此功能，因为 SQL Server Reporting Services 服务应用程序不存在或者尚未在管理中心配置报表服务器 URL。  
  
 **解决方法：** 确认您有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序且已正确对其进行配置。 有关详细信息请参阅明创建 Reporting Services 服务应用程序中[安装 Reporting Services SharePoint 模式用于 SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
###  <a name="bkmk_RS_SHP_notsupported"></a> 您看到一条指示 PREPAREIMAGE 不支持 RS_SHP 的错误消息  
 **说明：** 当您尝试为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 运行 PREPAREIMAGE 时，您会看到如下的错误消息：  
  
 “当执行 PREPAREIMAGE 操作时，指定的功能“RS_SHP”不受支持，因为它不支持 SysPrep。 删除与 SysPrep 不兼容的功能，然后重新运行安装程序。”  
  
 **解决方法：** 没有解决方法。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不支持 SYSPREP (PREPAREIMAGE)。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式支持 SYSPREP。  
  
##  <a name="bkmk_tshoot_native"></a> 排除本机模式安装问题  
  
###  <a name="PerfCounters"></a> 升级到 Windows Vista 或 Windows Server 2008 后，性能计数器不可见  
 如果将运行 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 的计算机的操作系统升级到 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，则升级后不会设置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 性能计数器。  
  
#### <a name="to-reinstate-reporting-services-performance-counters"></a>恢复 Reporting Services 性能计数器  
  
1.  删除以下注册表项：  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service**  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service**  
  
2.  打开命令窗口，然后在提示符下键入以下命令：  
  
    -   **运行\<**  *.NET 2.0 Framework 目录* **> \InstallUtil.exe \<**  *报表服务器 Bin 目录* **> \ReportingServicesLibrary.dll**  
  
        > [!NOTE]  
        >  替换\< *.NET 2.0 Framework 目录*> 与.NET Framework 2.0 的物理路径文件，并替换\<*报表服务器 Bin 目录*> 使用的物理路径报表服务器 bin 文件。  
  
3.  重新启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务。  
  
 若要验证这些步骤是否有效，请打开 Web 浏览器，导航到报表管理器 URL 或报表服务器 URL。 然后打开性能监视器以验证计数器是否正常工作。  
  
#### <a name="to-re-add-the-performance-registry-keys-by-using-registry-editor"></a>使用注册表编辑器重新添加性能注册表项  
  
1.  打开注册表编辑器：  
  
    1.  单击 **“开始”**，再单击 **“运行”**。  
  
    2.  在**运行**对话框中，在**打开**框中，键入`regedit`。  
  
2.  在注册表编辑器中，选择以下注册表项： `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance`  
  
3.  右键单击“性能”节点，指向“新建”，然后单击“多字符串值”。  
  
4.  类型`Counter Names`然后按 ENTER。  
  
5.  重复添加`Counter Types`此节点中的注册表项。  
  
6.  导航到以下注册表项： `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance`  
  
7.  右键单击“性能”节点，指向“新建”，然后单击“多字符串值”。  
  
8.  类型`Counter Names`然后按 ENTER。  
  
9. 重复添加`Counter Types`此节点中的注册表项。  
  
 修复 64 位实例或手动重新添加注册表项之后，可以使用性能监视器来配置要监视的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 性能对象。  
  
###  <a name="ConfigPropsMissing"></a> 从 SQL Server 2005 升级后，未配置 ReportServerExternalURL 和 PassThroughCookies 配置属性  
 当你升级从[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]到[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]、`ReportServerExternalURL`和`PassThroughCookies`配置属性不会配置在升级过程。 `ReportServerExternalURL` 是一个可选属性，并且仅当你使用的 SharePoint 2.0 Web 部件且希望用户能够检索报表并在新的浏览器窗口中打开它应设置它。 有关详细信息`ReportServerExternalURL`，请参阅[配置文件中的 Url &#40;SSRS 配置管理器&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)。 `PassThroughCookies` 仅在使用自定义身份验证方法时，需要。 有关详细信息`PassThroughCookies`，请参阅[配置报表管理器指向将传递自定义身份验证 Cookie](../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)。  
  
> [!NOTE]  
>  使用自定义身份验证时，建议您迁移安装而不是执行升级。 有关迁移 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的详细信息，请参阅[迁移 Reporting Services 安装（本机模式）](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)。  
  
 默认情况下， [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 配置中不存在这些属性。 如果在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中配置了这些属性且继续需要这些属性提供的功能，则在升级过程后，必须手动将它们添加到 **RSReportServer.config** 文件中。 有关详细信息，请参阅[修改 Reporting Services 配置文件 (RSreportserver.config)](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
###  <a name="Default2005InstallBreaks2008"></a> SQL Server 2005 Reporting Services 的默认实例运行 SQL Server 2012 reporting Services 的计算机上安装失败  
 如果你尝试安装的默认实例[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]已运行的实例的计算机上[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]实例将无法安装具有以下错误消息：  
  
 “此计算机上已安装了同名实例。 若要继续执行 SQL Server 安装程序，请提供唯一的实例名称。”  
  
 无论 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 实例是默认实例还是命名实例，并且无论计算机上是否已存在该名称的 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 实例，都会出现此问题。  
  
 若要解决此问题，可使用以下选项之一：  
  
-   如果必须运行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]作为计算机上的默认实例，必须安装[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]实例，再[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]实例。  
  
-   如果[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]实例不需要为默认实例，你可以安装[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]实例作为命名实例安装后[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]实例。  
  
###  <a name="WindowsAuthBreaksAfterUpgrade"></a> 使用后从 SQL Server 2005 升级到 SQL Server 2012 的 Windows 身份验证时发生 401-未经授权错误  
 如果从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 升级到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]，并对 Report Server 服务帐户使用 NTLM 身份验证和内置帐户，则在升级后访问报表服务器或报表管理器时，可能会遇到 401-未经授权的错误。  
  
 出现这种情况是因为 Windows 身份验证的默认 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 配置发生了更改。 当报表服务器服务帐户是 Network Service 或 Local System 时，会配置 Negotiate。 当报表服务器服务帐户不是这些内置帐户之一时，会配置 NTLM。 若要在升级后解决此问题，可以编辑 RSReportServer.config 文件，将 `AuthenticationType` 配置为 `RSWindowsNTLM`。 有关详细信息，请参阅 [Configure Windows Authentication on the Report Server](../security/configure-windows-authentication-on-the-report-server.md)。  
  
###  <a name="Uninstall32BitBreaks64Bit"></a> 卸载 32 位实例的 SQL Server 2012 Reporting Services 中的并行部署与 64 位实例中断 64 位实例  
 如果在计算机上并行安装 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 的 32 位实例和 64 位实例，卸载 32 位实例时，将删除 4 个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 注册表项。 这样会破坏 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的 64 位实例。 卸载 32 位实例时删除的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 注册表项为：  
  
 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance:Counter Types` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service\Performance:Counter Types`  
  
 若要解决此问题，可以修复 64 位实例。 尽管建议使用修复，但您可以使用注册表编辑器手动重新添加注册表项。  
  
> [!CAUTION]  
>  错误编辑注册表会严重损坏您的系统。 更改注册表之前，应当备份计算机中的所有重要数据。  
  
##  <a name="bkmk_additional"></a> 其他资源  
 下面是可以查阅的用来帮助您解决问题的其他资源：  
  
-   TechNet Wiki：故障排除主题 [排除 SharePoint 集成模式下的 SQL Server Reporting Services (SSRS) 问题](http://social.technet.microsoft.com/wiki/contents/articles/troubleshoot-sql-server-reporting-services-ssrs-in-sharepoint-integrated-mode.aspx)  
  
-   [论坛：SQL Server Reporting Services](http://social.msdn.microsoft.com/Forums/sqlreportingservices/threads)  
  
 ![SharePoint 设置](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 设置")[通过 Microsoft SQL Server Connect 提交反馈和联系信息](https://connect.microsoft.com/SQLServer/Feedback)(https://connect.microsoft.com/SQLServer/Feedback)。  
  
  