---
title: 安装 Reporting Services 本机模式报表服务器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ba2744f759a59ae4360bcd0d7c09dc45c7a4bdbf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78173447"
---
# <a name="install-reporting-services-native-mode-report-server"></a>安装 Reporting Services 本机模式报表服务器
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式报表服务器可从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导安装或从命令行安装。 在安装向导中，您可以选择：1) 安装文件并使用默认设置配置服务器；或 2) 仅安装文件，不通过安装向导配置服务器。  本主题讨论“本机模式默认配置”，其中，安装程序安装并配置报表服务器实例。 安装程序结束后，报表服务器便进入运行状态，可供使用。 本机模式报表服务器作为一个独立的应用程序服务器运行。 本机模式是默认服务器模式。

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式|

##  <a name="in-this-topic"></a><a name="bkmk_top"></a>本主题中的

-   [什么是默认配置？](#bkmk_whatisdefaultconfiguration)

-   [何时安装本机模式的默认配置](#bkmk_whentoinstalldefaultconfig)

-   [惠?](#bkmk_requirements)

-   [默认 URL 保留项](#bkmk_defaultURLreservations)

-   [通过 SQL Server 安装向导安装本机模式](#bkmk_installwithwizard)

-   [使用命令行安装本机模式](#bkmk_commandline)

##  <a name="what-is-the-default-configuration"></a><a name="bkmk_whatisdefaultconfiguration"></a>什么是默认配置？
 当您选择本机模式默认配置选项时，安装程序将安装下列 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能：

-   报表服务器服务（包括报表服务器 Web 服务、后台处理应用程序和报表管理器）

-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器

-    命令行实用工具（rsconfig.exe、rskeymgmt.exe 和 rs.exe）

 此选项不适用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]或[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]之类的共享功能，如果您要安装这些功能，则必须将其指定为单独的项。

 安装程序为本机模式的报表服务器安装配置以下设置：

-   报表服务器服务的服务帐户。

-   报表服务器 Web 服务 URL。

-   报表管理器 URL。

-   报表服务器数据库。

-   服务帐户对报表服务器数据库的访问权限。

-   与报表服务器数据库的 DSN 连接。

 安装程序不会配置无人参与的执行帐户和报表服务器电子邮件，不会备份加密密钥或进行扩展部署。 可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器配置这些属性。 有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)。

##  <a name="when-to-install-the-default-configuration-for-native-mode"></a><a name="bkmk_whentoinstalldefaultconfig"></a>何时安装本机模式的默认配置
 默认配置在操作状态下安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，以便在安装程序结束后可以立即使用报表服务器。 如果希望通过省掉那些原本要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具中执行的必要配置任务从而减少配置步骤，请指定此模式。

 安装默认配置不能确保安装程序结束后报表服务器即可工作。 服务启动时，默认 URL 可能无法注册。 请始终对安装进行测试，以确保服务启动并按预期方式运行。

##  <a name="requirements"></a><a name="bkmk_requirements"></a> 要求
 默认配置选项使用默认值来配置使报表服务器正常运行所需的核心设置。 安装具有以下要求：

-   您的硬件应满足运行 Microsoft SQL Server 的最低硬件和软件要求。 有关详细信息，请参阅 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。

-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 必须安装在同一实例中。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例承载安装程序创建和配置的报表服务器数据库。

-   用于运行安装程序的用户帐户必须是本地 Administrators 组成员，而且拥有针对承载报表服务器数据库的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例创建数据库的权限。

-   安装程序必须能够使用默认值来保留用于访问报表服务器和报表管理器的 URL。 这些值包括端口 80、强通配符和虚拟目录名（格式为 ReportServer_\<instance_name>  和 Reports_\<instance_name>  。

-   安装程序必须能够使用默认值来创建报表服务器数据库。 这些值包括 **ReportServer** 和 **ReportServerTempDB**。 如果存在以前安装的现有数据库，安装程序则因无法将报表服务器配置为本机模式的默认配置而被阻止。 必须重命名、移动或删除这类数据库以取消阻止安装程序。

 如果计算机不满足默认安装的全部要求，则必须在“仅文件”模式下安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，并在安装程序结束后使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器对其进行配置。

 请不要仅为了使默认安装继续进行而试图对计算机进行重新配置。 这样做可能需要好几个小时的工作量，实际上抵消了该安装选项所带来的省时优势。 最佳的解决方案是在“仅文件”模式下安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，然后将报表服务器配置为使用特定值。

##  <a name="default-url-reservations"></a><a name="bkmk_defaultURLreservations"></a>默认 URL 保留项
 URL 预留由前缀、主机名、端口和虚拟目录组成：

|组成部分|说明|
|----------|-----------------|
|前缀|默认的前缀为 HTTP。 如果以前安装过安全套接字层 (SSL) 证书，安装程序将尝试创建使用 HTTP 前缀的 URL 预留。|
|主机名|默认主机名为强通配符 (+)。 它指定对于解析为计算机的任何主机名，Report Server 将接受指定端口上的任何 HTTP 请求，包括 http://\<computername>/reportserver、 http://localhost/reportserver或 http://\<IPAddress>/reportserver。|
|端口|默认端口为 80。 请注意，如果使用端口 80 以外的其他任何端口，则在浏览器窗口中打开 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 应用程序时，必须将该端口显式添加至 URL 中。|
|虚拟目录|默认情况下，将以报表服务器 Web 服务的 ReportServer_\<*instance_name*> 的格式创建虚拟目录，\<*并 Reports_ instance_name> 报表管理器。* 对于报表服务器 Web 服务，默认的虚拟目录为 **reportserver**。 对于报表管理器，默认的虚拟目录为 **reports**。|

 完整的 URL 字符串示例如下所示：

-   http://+:80/reportserver 用于访问报表服务器。

-   http://+:80/reports提供对报表管理器的访问。

##  <a name="install-native-mode-with-the-sql-server-installation-wizard"></a><a name="bkmk_installwithwizard"></a>通过 SQL Server 安装向导安装本机模式
 以下列表介绍了在 SQL Server 安装向导中选择的  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 特定步骤和选项。 该列表并不介绍您在安装向导中看到的每一页，而是仅介绍作为本机模式安装一部分的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 相关页。

1.  在 **“安装角色”** 页上，选择 **“SQL Server 功能安装”** 。

     ![安装角色的 SQL Server 功能安装](../../../2014/sql-server/install/media/rs-setuprole.gif "安装角色的 SQL Server 功能安装")

2.  在 **“功能选择”** 页上，选择以下选项：

    -   **Database Engine Services**（除非已安装数据库引擎实例）。

    -   **Reporting Services 本机**。

    -   **管理工具-基本**。 管理工具不是必需的，但是建议您安装，除非您安装了其他一些管理工具。 默认配置选项将导致 Report Server 运行，但你可能想要在以后更改配置选项。 某些选项（如 "我的报表"）通过[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]

     ![功能选择中的 SSRS 本机模式选择](../../../2014/sql-server/install/media/rs-setupfeatureselection-native-withcircles.gif "功能选择中的 SSRS 本机模式选择")

3.  如果计划使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 订阅功能，则在 **“服务器配置”** 页上，您要验证是否为 **“自动”** 启动类型配置了 SQL Server 代理。

4.  在 **“Reporting Services 配置”** 页上，选择 **“安装和配置”** 。

     ![SSRS 本机模式配置](../../../2014/sql-server/install/media/rs-setupconfiguration-native-with-circles.gif "SSRS 本机模式配置")

5.  完成 SQL Server 安装向导后，使用以下基本步骤验证默认本机模式安装。

    -   打开 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，确认您可以连接到报表服务器。

    -   使用管理权限打开浏览器并连接到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表管理器，例如 `http://loclahost/Reports`。

    -   使用管理权限打开浏览器并连接到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器页。 例如  `http://loclahost/ReportServer`

 有关详细信息，请参阅以下两个主题的“本机”一节：

 [验证 Reporting Services 安装](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)

 [排除 Reporting Services 安装故障](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)

##  <a name="install-native-mode-with-the-command-line"></a><a name="bkmk_commandline"></a>用命令行安装纯模式
 以下示例包括 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务，因为默认配置需要此服务。

```
setup /q /ACTION=install /FEATURES=SQL,RS,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" 
/RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK 
SERVICE" /RSSVCSTARTUPTYPE="Manual" /RSINSTALLMODE="DefaultNativeMode"
```

 有关详细信息和示例，请参阅[Reporting Services SharePoint 模式和本机模式的命令提示符安装](../../reporting-services/install-windows/install-reporting-services-at-the-command-prompt.md)和[从命令提示符安装 SQL Server 2014](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

## <a name="see-also"></a>另请参阅
 [排查 Reporting Services 安装问题](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)[验证 Reporting Services 安装](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)[将报表服务器服务帐户配置 &#40;ssrs Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md) [ssrs &#40;配置](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)报表服务器 Url Configuration Manager ssrs&#41;&#40;Configuration Manager 仅文件安装&#41;[配置报表服务器数据库连接](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md) [&#40;Reporting Services&#41;](../../reporting-services/install-windows/files-only-installation-reporting-services.md) [初始化报表服务器 &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md) [在本机模式报表服务器上配置 SSL 连接](../security/configure-ssl-connections-on-a-native-mode-report-server.md)[配置报表服务器 url &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md) [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)[快速开始安装 SQL Server 2014](../../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)


