---
title: 升级和迁移 Reporting Services | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SSRS, upgrading
- Reporting Services, upgrades
- SQL Server Reporting Services, upgrading
- upgrading Reporting Services
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 42cdcb1245e5280d25a94a81617da92f755ea048
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176937"
---
# <a name="upgrade-and-migrate-reporting-services"></a>Upgrade and Migrate Reporting Services

本主题概述 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的升级和迁移选项。 有两种用于升级 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 部署的常规方法：

-   **升级：** 升级服务器和[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]实例上当前安装的组件。 这通常称为“就地”升级。 对于从 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务器的一种模式升级到另一模式，不支持就地升级。 例如，不能将本机模式报表服务器升级到 SharePoint 模式报表服务器。 您可以将报表项从一个模式迁移到另一个模式。 有关详细信息，请参阅本文档后面的 "本机到 SharePoint 迁移" 部分和相关主题[示例 Reporting Services Rs-232c 脚本在报表服务器之间迁移内容](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)。

-   **迁移**：安装和配置新的 SharePoint 环境，将报表项和资源复制到新环境，并将新环境配置为使用现有内容。 迁移的较低级别形式是复制 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据库、配置文件，如果使用的是 SharePoint 模式，则还包括复制 SharePoint 内容数据库。

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]纯模式|

##  <a name="bkmk_top"></a>本主题内容：

-   [已知的升级问题和最佳做法](#bkmk_known_issues)

-   [并行安装](#bkmk_side_by_side)

-   [就地升级](#bkmk_inplace_upgrade)

-   [升级准备一览表](#bkmk_upgrade_checklist)

-   [本机模式升级和迁移方案](#bkmk_native_scenarios)

-   [升级 Reporting Services 本机模式扩展部署](#bkmk_native_scaleout)

-   [SharePoint 模式升级和迁移方案](#bkmk_sharePoint_scenarios)

-   [迁移注意事项](#bkmk_migration_considerations)

-   [其他资源](#bkmk_additional_resources)

##  <a name="bkmk_known_issues"></a>已知的升级问题和最佳做法
 有关可以升级的受支持版本的详细列表，请参阅 [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)。

> [!TIP]
>  有关与 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的问题相关的最新信息，请参阅以下内容：
> 
>  -   [SQL Server 2014 发行说明](https://go.microsoft.com/fwlink/?LinkID=296445)。
> -   [SQL Server 2014 Reporting Services 提示、技巧和故障排除](https://go.microsoft.com/fwlink/?LinkID=391254)。
> -   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升级顾问。 有关详细信息，请参阅[升级顾问 &#40;Reporting Services 升级问题&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)和[如何：安装升级顾问](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md)。

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

##  <a name="bkmk_side_by_side"></a>并行安装
 
  [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 本机模式可与 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 本机模式部署并行安装。

 不支持并行部署 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] SharePoint 模式和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式组件的任何先前版本。

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

##  <a name="bkmk_inplace_upgrade"></a>就地升级
 升级由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序完成。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序可用于升级任意或所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]组件，包括。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装程序将检测现有实例并提示您进行升级。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序提供了升级选项，您可以将其作为命令行参数指定或在安装向导中指定。

 运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序时，可以选择从以下版本之一升级，也可以安装运行现有并行安装的 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 的新实例：

-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]

-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]

-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]

-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]

 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的详细信息，请参阅以下内容：

||
|-|
|[升级到 SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)|
|[使用安装向导 &#40;安装程序升级到 SQL Server 2014&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)|
|[Install SQL Server 2014 from the Command Prompt](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)|

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

##  <a name="bkmk_upgrade_checklist"></a>升级前的清单
 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之前，请先查看以下内容：

-   检查相关要求，以确定硬件和软件是否可以支持 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]。 有关详细信息，请参阅 [Hardware and Software Requirements for Installing SQL Server 2014](../../../2014/sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。

-   使用系统配置检查器 (SCC) 扫描报表服务器计算机中是否有可能妨碍 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]成功安装的任何情况。 有关详细信息，请参阅 [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)。

-   查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的安全最佳实践和指南。 有关详细信息，请参阅[SQL Server 安装的安全注意事项](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)。

-   在报表服务器计算机上运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升级顾问，以确定可能妨碍成功升级的任何问题。 有关详细信息，请参阅 [Use Upgrade Advisor to Prepare for Upgrades](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)。

-   备份对称密钥。 有关详细信息，请参阅 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。

-   备份报表服务器数据库和配置文件。 有关详细信息，请参阅 [Backup and Restore Operations for Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)。

-   备份对 IIS 中现有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 虚拟目录的任何自定义。

-   删除无效的 SSL 证书。  这包括在升级 Reporting Services 前未计划更新的到期证书。  无效证书将导致升级失败，且会将类似于以下的错误消息写入 Reporting Services 日志文件： **Microsoft.ReportingServices.WmiProvider.WMIProviderException: A Secure Sockets Layer (SSL) certificate is not configured on the Web site**。

 在升级生产环境之前，务必在与生产环境具有相同配置的生产前环境中运行测试升级。

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

## <a name="overview-of-migration-scenarios"></a>迁移方案概述
 如果从 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的受支持版本升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则通常可以运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导来升级报表服务器程序文件、数据库以及所有应用程序数据。

 然而，如果遇到以下任何情况，都需要手动 **迁移** 报表服务器安装：

-   升级顾问检测到了一个或多个升级阻塞程序。 有关详细信息，请参阅 [Use Upgrade Advisor to Prepare for Upgrades](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)。

-   您想要更改部署中使用的报表服务器的类型。 例如，不能将本机模式报表服务器升级或转换到 SharePoint 模式。 有关详细信息，请参阅[从本机迁移到 SharePoint (SSRS)](../../reporting-services/install-windows/native-to-sharepoint-migration-ssrs.md)。

-   您需要在升级过程中最大限度地减少报表服务器的脱机时间。 在您将内容数据复制到新报表服务器实例，并在不改变现有报表服务器安装状态的情况下测试该安装时，当前安装将保持联机状态。

-   您要将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 SharePoint 2010 部署迁移到 SharePoint 2013。 SharePoint 2013 不支持从 SharePoint 2010 就地升级。 有关详细信息，请参阅[迁移 Reporting Services 安装（SharePoint 模式）](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)。

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

##  <a name="bkmk_native_scenarios"></a>本机模式升级和迁移方案
 **升级：** 对于本主题中前面列出的每个受支持的版本，本机模式的就地升级都是相同的。 运行 SQL Server 安装向导或命令行安装。 在安装后，报表服务器数据库将自动升级到新的报表服务器数据库架构。 有关详细信息，参阅本主题中的 [In-place upgrade](#bkmk_inplace_upgrade) 部分。

 当选择了一个要升级的现有报表服务器实例时，升级过程即开始。

1.  如果报表服务器数据库位于远程计算机上，而您没有更新该数据库的权限，则安装程序将提示您提供更新远程报表服务器数据库的凭据。 请确保提供具有 `sysadmin` 或数据库更新权限的凭据。

2.  安装程序检查阻止升级的条件或设置并读取配置设置。 示例包括在报表服务器上部署的自定义扩展插件。 如果升级受阻，则必须修改您的安装以便不再阻止升级，或者迁移到新的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例。 有关详细信息，请参阅升级顾问文档。

3.  如果升级可以继续，则安装程序将提示您继续升级过程。

4.  安装程序为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 程序文件创建新的文件夹。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]安装的程序文件夹包括 MSRS12。\<*实例名*>。

5.  安装程序添加 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器程序文件、配置工具和作为报表服务器功能一部分的命令行实用工具。

    1.  删除先前版本中的程序文件。

    2.  升级到新版本的报表服务器配置工具和实用工具包括本机模式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具、命令行实用工具（如 RS.exe）和报表生成器。

    3.  不升级其他客户端工具（如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和联机丛书）。 若要获得这些工具的新版本，可以在运行安装程序时添加它们。 其早期版本将与 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本并存。 如果安装了示例，则会保留早期版本。 安装程序不支持升级 SQL Server 示例。

    4.  
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 为单独下载。 有关详细信息，请参阅 [Microsoft SQL Server 2014 Data Tools - Business Intelligence for Microsoft Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)。

6.  安装程序重用服务控制管理器中 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器服务的服务条目。 此服务条目包括报表服务器 Windows 服务帐户。

7.  安装程序基于 IIS 中的现有虚拟目录设置保留新的 URL。 安装程序可能不会删除 IIS 中的虚拟目录，所以请确保在完成升级之后手动删除它们。

8.  安装程序将报表服务器数据库升级到新架构并通过为角色添加数据库所有者权限来修改 `RSExecRole`。 仅当从[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SP1 之前的升级时，才会执行此步骤。

9. 安装程序合并配置文件中的设置。 添加新条目时，使用当前安装的配置文件作为基础。 不会删除过时的条目，但是在升级完成后，报表服务器不会再读取它们。 升级不会删除旧日志文件、过时的 RSWebApplication.config 文件或 IIS 中的虚拟目录设置。 升级不会删除 SQL Server 2005 报表设计器、Management Studio 或其他客户端工具。 如果不再需要它们，请确保在升级完成后删除这些文件和工具。

 **迁移：** 将以前版本的本机模式安装迁移到[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的步骤与本主题前面列出的所有支持的版本的步骤相同。 有关详细信息，请参阅 [迁移 Reporting Services 安装（本机模式）](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

##  <a name="bkmk_native_scaleout"></a>升级 Reporting Services 本机模式扩展部署
 下面概述了如何升级扩展为多个报表服务器的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式部署。 此过程需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 部署停机：

1.  备份报表服务器数据库和加密密钥。 有关详细信息，请参阅 [Reporting Services 的备份和还原操作](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)和[添加和删除横向扩展部署的加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)。

2.  使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，从扩展部署中删除所有报表服务器。 有关详细信息，请参阅[配置本机模式报表服务器扩展部署（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)。

3.  将一台报表服务器升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。

4.  使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，将报表服务器重新添加到扩展部署。 有关详细信息，请参阅[配置本机模式报表服务器扩展部署（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)。

     对于每个服务器，重复升级和扩展步骤。

##  <a name="bkmk_sharePoint_scenarios"></a>SharePoint 模式升级和迁移方案
 以下部分介绍从[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint 模式的指定版本升级或迁移到[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint 模式所需的问题和基本步骤。

 有两种升级 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式部署的安装组件。

-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 共享服务。

    > [!TIP]
    >  使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint cmdlet `Get-SPRSServiceApplicationServers` 确定 SharePoint 场中当前运行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 共享服务并因此需要升级的服务器。

-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]用于 SharePoint 产品的外接程序。 有关详细信息，请参阅[安装或卸载用于 sharepoint 的 Reporting Services 外接程序 &#40;sharepoint 2010 和 sharepoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。

 有关迁移 SharePoint 模式安装的详细步骤，请参阅[迁移 Reporting Services 安装（SharePoint 模式）](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)。

> [!IMPORTANT]
>  由于需要升级不同技术，下面的某些方案将需要将 SharePoint 环境停止运行。 如果您的情况不允许停机，则需要完成迁移，而非就地升级。

### <a name="sssql11-to-sssql14"></a>[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]自[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **正在启动环境：** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]，SharePoint 2010。

 **结束环境：** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]、SharePoint 2010 或 sharepoint 2013。

-   **SharePoint 2010：** 支持就地升级[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，但升级方案需要 SharePoint 环境停机。

     如果您还希望结束环境运行 SharePoint 2013，则需完成 SharePoint 2010 到 SharePoint 2013 的数据库附加升级。

-   **SharePoint 2013：** SharePoint 2013 不支持从 SharePoint 2010 就地升级。 但是支持**数据库附加升级**过程。 该行为不同于升级到 SharePoint 2010，在后者，客户可以在两个基本的升级方法（就地升级和数据库附加升级）之间进行选择。

     如果您具有与 SharePoint 2010 相集成的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装，则不能就地升级 SharePoint 服务器。 不过，您可以将内容数据库和服务应用程序数据库从 SharePoint 2010 场迁移到 SharePoint 2013 场。

### <a name="sskilimanjaro-to-sssql14"></a>[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]自[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **正在启动环境：** SQL Server 2008 R2，SharePoint 2010。

 **结束环境：** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，SharePoint 2010。

-   支持就地升级，并且不会停止 SharePoint 环境的运行。

-   在场中的每个 Web 前端上安装用于 SharePoint 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 外接程序的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本。 您可以通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导或通过下载外接程序安装该外接程序。

-   运行[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安装以升级每个 "Report Server" 的 SharePoint 模式。SQL Server 安装向导将安装[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服务并创建新的服务应用程序。

     如果您还希望结束环境运行 SharePoint 2013，则需完成 SharePoint 2010 到 SharePoint 2013 的数据库附加升级。

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

### <a name="sskatmai-sp2-to-sssql14"></a>
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2 至 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **启动环境：** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2、SharePoint 2007。

 **结束环境：** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，SharePoint 2010。

-   此就地升级方案要求停止 SharePoint 环境的运行，因为 SharePoint 和 SQL Server 技术都需要升级。 您可能要考虑完成迁移，而不是就地升级。

-   如果尚未完成，请首先将 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 升级到 Service Pack 2 (SP2)。

-   将 SharePoint 升级到 2010。 当您运行 SharePoint 2010 必备安装程序时，它将升级用于 SharePoint 2010 产品的 Reporting Services 外接程序。

-   在所有 SharePoint Web 前端上都安装用于 SharePoint 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 外接程序的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本。 该 SharePoint 必备安装程序安装了该外接程序的 SQL Server 2008 R2 版本，但您需要 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本以便与 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器配合使用。

-   > [!WARNING]
    >  在执行了 SharePoint 升级后，您的 Reporting Services 环境将在升级 SQL Server 前处于非工作状态。

-   将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 运行 SQL server 安装向导时，将会看到有关 "**SQL Server Reporting Services SharePoint 模式身份验证**" 对话框的对话框。 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务将被安装，并且来自身份验证页的凭据将用于创建新的 SharePoint 应用程序池。

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

### <a name="sql-server-2005-sp2-to-sssql14"></a>将 2005 SP2 SQL Server 到[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **正在启动环境：** SQL Server 2005 SP2、SharePoint 2007。

 **结束环境：** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，SharePoint 2010。

-   此就地升级方案要求停止 SharePoint 环境的运行，因为 SharePoint 和 SQL Server 技术都需要升级。 您可能要考虑完成迁移，而不是就地升级。

-   如果尚未完成，请首先将 SQL Server 2005 升级到 Service Pack 2 (SP2)。

-   将 SharePoint 升级到 SharePoint 2010。 当您运行 SharePoint 2010 必备安装程序时，它将升级用于 SharePoint 2010 产品的 Reporting Services 外接程序。

-   > [!WARNING]
    >  在执行了 SharePoint 升级后，您的 Reporting Services 环境将在升级 SQL Server 前处于非工作状态。

-   在所有 SharePoint Web 前端上都安装用于 SharePoint 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 外接程序的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本。 该 SharePoint 必备安装程序安装了该外接程序的 SQL Server 2008 R2 版本，但您需要 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本以便与 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器配合使用。

-   将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 在您运行 SQL Server 安装向导时，将会看到“SQL Server Reporting Services SharePoint 模式身份验证”对话框。 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务将被安装，并且来自身份验证页的凭据将用于创建新的 SharePoint 应用程序池。

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

##  <a name="bkmk_migration_considerations"></a>迁移注意事项
 移动应用程序数据时，应注意下列事项和约束：

-   加密密钥的保护包括一个合并计算机标识的哈希。

-   报表服务器数据库名称将固定，并且无法在新计算机上重命名。

### <a name="encryption-key-considerations"></a>加密密钥注意事项
 将报表服务器数据库移到新计算机之前始终备份加密密钥。

 将报表服务器安装移到另一台计算机会使保护加密密钥（这些加密密钥用于为报表服务器数据库中存储的敏感数据提供安全保障）的哈希无效。 使用该数据库的每个报表服务器实例都有其加密密钥副本，在当前计算机对其定义时将使用服务帐户的标识对其进行加密。 如果更改计算机，则即使在新计算机上使用同一帐户名称，服务也无法访问其密钥。

 若要在新的报表服务器计算机上重新建立可逆加密，必须还原先前备份的密钥。 报表服务器数据库中存储的完整密钥集由对称密钥值和服务标识信息组成，后者用于限制密钥的访问，使密钥仅可供存储它的报表服务器实例使用。 在密钥还原过程中，报表服务器将用密钥的新版本替换密钥的现有副本。 新版本包括当前计算机上定义的计算机标识值和服务标识值。 有关详情，请参阅以下主题：

-   SharePoint 模式：请参阅[管理 Reporting Services SharePoint 服务应用程序](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)的“密钥管理”部分

-   本机模式：请参阅 [备份和还原 Reporting Services 加密密钥](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

### <a name="fixed-database-name"></a>固定数据库名称
 不能重命名报表服务器数据库。 创建数据库时，数据库的标识将记录在报表服务器存储过程中。 重命名报表服务器主数据库或临时数据库会在过程运行时导致出现错误，从而使报表服务器安装无效。

 如果现有安装的数据库名称不适合新安装，应考虑创建一个具有您所选名称的新数据库，然后使用下面列出的技术加载现有应用程序数据：

-   编写调用报表服务器 Web 服务 SOAP 方法的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 脚本，以在各数据库之间复制数据。 可以使用 RS.exe 实用工具来运行该脚本。 有关这种方法的详细信息，请参阅 [脚本编写和带 Reporting Services 的 PowerShell](../tools/scripting-and-powershell-with-reporting-services.md)。

-   编写调用 WMI 提供程序的代码，以在各数据库之间复制数据。 有关这种方法的详细信息，请参阅 [访问 Reporting Services WMI 提供程序](../tools/access-the-reporting-services-wmi-provider.md)。

-   如果仅有少量项，则可以将报表、报表模型以及共享数据源从报表设计器、模型设计器和报表生成器重新发布到新的报表服务器。 必须重新创建角色分配、订阅、共享计划、报表快照计划、对报表或其他项设置的自定义属性、模型项安全性以及对报表服务器设置的属性。 您将丢失报表历史记录和报表执行日志数据。

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

##  <a name="bkmk_additional_resources"></a>其他资源

> [!NOTE]
>  有关 SharePoint 数据库附加升级的详细信息，请参阅下列文章：

-   [SharePoint 2013 升级过程概述](https://go.microsoft.com/fwlink/p/?LinkId=256688)（https://go.microsoft.com/fwlink/p/?LinkId=256688)。

-   https://go.microsoft.com/fwlink/p/?LinkId=256689)[升级到 SharePoint 2013 （之前的准备](https://go.microsoft.com/fwlink/p/?LinkId=256689)工作。

-   [将数据库从 sharepoint 2010 升级到 sharepoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690) （https://go.microsoft.com/fwlink/p/?LinkId=256690)。

 [本主题中与 "](#bkmk_top) ![返回页首" 链接一起使用的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")：

## <a name="see-also"></a>另请参阅
 [升级报表](../../reporting-services/install-windows/upgrade-reports.md)[将使用安装向导 &#40;安装程序升级到 SQL Server 2014&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)


