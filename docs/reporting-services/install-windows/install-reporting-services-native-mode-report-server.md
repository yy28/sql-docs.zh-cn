---
title: "安装 Reporting Services 本机模式报表服务器 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
caps.latest.revision: 68
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 65a02d6be519b146f37159dd75f1f51dcfb254cc
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="install-reporting-services-native-mode-report-server"></a>安装 Reporting Services 本机模式报表服务器

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../../includes/ssrs-appliesto-sql2016-xpreview.md)]

了解如何在本机模式下安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 这将提供对用于管理报表和其他项的 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 的访问权限。

> [!NOTE]
> 查找 Power BI 报表服务器？ 请参阅[安装 Power BI 报表服务器](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/)。

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式报表服务器是默认的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务器模式，可从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导安装或从命令行安装。 在安装向导中，你可以选择安装文件并使用默认设置配置服务器或仅安装文件。  本主题讨论“本机模式默认配置”，其中，安装程序安装并配置报表服务器实例。 安装完成后，报表服务器便进入运行状态，可供基本的报表查看和管理。  其他功能（例如 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 集成和使用订阅处理电子邮件的发送）需要其他配置。  
  
##  <a name="bkmk_whatisdefaultconfiguration"></a> 什么是默认配置？  
 当您选择本机模式默认配置选项时，安装程序将安装下列 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能：  
  
-   报表服务器服务（包括报表服务器 Web 服务、后台处理应用程序和用于查看和管理报表的 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 以及权限）。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 命令行实用工具 rsconfig.exe、rskeymgmt.exe 和 rs.exe。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 现在是单独的下载。  
  
 安装程序为本机模式的报表服务器安装配置以下设置：  
  
-   报表服务器服务的服务帐户。  
  
-   报表服务器 Web 服务 URL。  
  
-   [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] URL。  
  
-   报表服务器数据库。  
  
-   服务帐户对报表服务器数据库的访问权限。  
  
-   报表服务器数据库的连接信息，又称为数据源名称 (DSN)。  
  
 安装程序不会配置无人参与的执行帐户和报表服务器电子邮件，不会备份加密密钥或进行扩展部署。 可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器配置这些属性。 有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)。
  
##  <a name="bkmk_whentoinstalldefaultconfig"></a> 何时安装本机模式默认配置  
 默认配置在操作状态下安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，以便在安装程序结束后可以立即使用报表服务器。 如果希望通过省掉那些原本要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具中执行的必要配置任务从而减少配置步骤，请指定此模式。  
  
 安装默认配置不能确保安装程序结束后报表服务器即可工作。 服务启动时，默认 URL 可能无法注册。 请始终对安装进行测试，以确保服务启动并按预期方式运行。  请参阅 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)。
  
##  <a name="bkmk_requirements"></a> 要求  
 默认配置选项使用默认值来配置使报表服务器正常运行所需的核心设置。 安装具有以下要求：  
  
-   阅读 [Hardware and Software Requirements for Installing SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md) 。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 必须安装在同一实例中。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例承载安装程序创建和配置的报表服务器数据库。  
  
-   用于运行安装程序的用户帐户必须是本地 Administrators 组成员，而且拥有针对承载报表服务器数据库的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例创建数据库的权限。  
  
-   安装程序必须能够使用默认值来保留用于访问报表服务器和 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]的 URL。 这些值为端口 80、 强通配符和格式中的虚拟目录名称**ReportServer_\<***instance_name*  **>** 和**Reports_\<***instance_name***>**。  
  
-   安装程序必须能够使用默认值来创建报表服务器数据库。 这些值包括 **ReportServer** 和 **ReportServerTempDB**。 如果存在以前安装的现有数据库，安装程序则因无法将报表服务器配置为本机模式的默认配置而被阻止。 必须重命名、移动或删除这类数据库以取消阻止安装程序。  
  
 如果计算机不满足默认安装的全部要求，则必须在“仅文件”模式下安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，并在安装程序结束后使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器对其进行配置。
 
 > [!IMPORTANT]
 > 虽然可以在只读域控制器 (RODC) 的环境中安装 Reporting Services，Reporting Services 需要访问读写域控制器正常。 如果 Reporting Services 仅有权访问在 RODC，你可能尝试管理该服务时遇到错误。
  
##  <a name="bkmk_defaultURLreservations"></a> 默认 URL 保留项  
 URL 保留项由前缀、主机名、端口和虚拟目录组成：  
  
|组成部分|说明|  
|----------|-----------------|  
|前缀|默认的前缀为 HTTP。 如果以前安装过安全套接字层 (SSL) 证书，安装程序将尝试创建使用 HTTP 前缀的 URL 保留项。|  
|主机名|默认主机名为强通配符 (+)。 它指定报表服务器将接受解析为计算机上，任何主机名的指定端口上的任何 HTTP 请求包括`http://<computername>/reportserver`， `http://localhost/reportserver`，或`http://<IPAddress>/reportserver`。|  
|端口|默认端口为 80。 请注意，如果使用端口 80 以外的其他任何端口，则在浏览器窗口中打开 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 应用程序时，必须将该端口显式添加至 URL 中。|  
|虚拟目录|默认情况下，虚拟目录创建 ReportServer_ 格式\<*instance_name*> 为报表服务器 Web 服务和 Reports_\<*instance_name*> 为[!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]。 对于报表服务器 Web 服务，默认的虚拟目录为 **reportserver**。 对于 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]，默认的虚拟目录为 **reports**。|  
  
 完整的 URL 字符串示例如下所示：  
  
-   `http://+:80/reportserver`提供对报表服务器的访问。  
  
-   `http://+:80/reports`提供对访问[!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]。
  
##  <a name="bkmk_installwithwizard"></a> 使用 SQL Server 安装向导安装本机模式  
 以下列表介绍了在 SQL Server 安装向导中选择的  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 特定步骤和选项。 该列表并不介绍您在安装向导中看到的每一页，而是仅介绍作为本机模式安装一部分的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 相关页。  
  
1.  运行 SQL Server 安装向导 (setup.exe) 并单步执行以下起始页：  
  
    -   产品密钥  
  
    -   许可条款  
  
    -   全局规则  
  
    -   Microsoft Update  
  
    -   产品更新  
  
    -   安装安装程序文件  
  
    -   安装规则  
  
2.  在 **“安装角色”** 页上，选择 **“SQL Server 功能安装”**。  
  
     ![安装程序角色的 SQL Server 功能安装](../../reporting-services/install-windows/media/rs-setuprole.png "for 安装角色的 SQL Server 功能安装")  
  
3.  在 **“功能选择”** 页上，选择以下选项：  
  
    -   (1) **数据库引擎服务**，除非已安装数据库引擎实例）。  
  
    -   (2) **Reporting Services - 本机**。  
  
     ![在功能选择中选择的 SSRS 本机模式](../../reporting-services/install-windows/media/rs-setupfeatureselection-native-withcircles.png "在功能选择中选择的 SSRS 本机模式")  
  
4.  查看通过的“功能规则”  。  
  
5.  在实例配置页中，请记住，如果选择配置“命名实例” ，则当浏览到报表管理器和报表服务器本身时，将需要在 URLS 中使用实例名称。 如果实例名称是“THESQLINSTANCE”，URLS 将如下所示：  
  
    -   `http://[ServerName]/ReportServer_THESQLINSTANCE`  
  
    -   `http://[ServerName]/Reports_THESQLINSTANCE`  
  
6.  **服务器配置**： 如果你打算使用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]订阅功能，然后在**服务器配置**页上，配置 SQL Server 代理**自动**启动类型。   默认为手动。  
  
7.  在“数据库引擎配置”  页上，添加 SQL Server 管理员。  
  
8.  在 **“Reporting Services 配置”** 页上，选择 **“安装和配置”**。  
  
     ![SSRS 本机模式配置](../../reporting-services/install-windows/media/rs-setupconfiguration-native-with-circles.png "SSRS 本机模式配置")  
  
    > [!NOTE]  
    >  除非同时选择安装该数据库功能，否则“安装和配置” 将不可用。  
  
9. 功能配置规则：验证通过的规则。 如果所有规则都通过，则安装向导将自动前进到“安装准备就绪”  。  针对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，规则将验证报表服务器目录和临时目录数据库是否尚未存在。  
  
10. ![请注意](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "注意")上**准备好安装**页上，记下配置文件的路径，因为可以在以后进行的服务器的初始总结内指[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]包括安装，组件的配置服务帐户和管理员。  
  
11. 完成 SQL Server 安装向导后，使用以下基本步骤验证默认本机模式安装。  
  
    -   打开 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，确认您可以连接到报表服务器。  
  
    -   **使用管理权限** 打开浏览器并连接到 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]，例如 `http://localhost/Reports`。  
  
    -   使用管理权限打开浏览器并连接到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器页。 例如  `http://localhost/ReportServer`  
  
 有关详细信息，请参阅以下两个主题的“本机”一节：  
  
 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
  
 [排除 Reporting Services 安装故障](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
  
##  <a name="bkmk_additional_configuration"></a> 其他配置  
  
-   若要配置[!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]集成以便可以固定报表项到[!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]仪表板，请参阅[Power BI 报表服务器集成](../../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)。  
  
-   若要配置为订阅处理的电子邮件，请参阅[电子邮件设置-Reporting Services 本机模式](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)和[Reporting Services 中的电子邮件传递](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)。  
  
-   若要配置 web 门户，以便您可以查看和管理报表的报表计算机上访问它，请参阅[为报表服务器访问配置防火墙](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)和[配置报表服务器以进行远程管理](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)。  
  
## <a name="see-also"></a>另请参阅

[排除 Reporting Services 安装故障](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
[验证 Reporting Services 安装](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[配置报表服务器服务帐户](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
[配置报表服务器 Url](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[配置报表服务器数据库连接](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[“仅文件”安装 (Reporting Services)](../../reporting-services/install-windows/files-only-installation-reporting-services.md)   
[初始化报表服务器](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
[在本机模式报表服务器上配置 SSL 连接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)   
[配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   

更多问题？ [尝试的 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)

