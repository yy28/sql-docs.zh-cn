---
title: 安装 Reporting Services SharePoint 模式下用于 SharePoint 2010 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 47efa72e-1735-4387-8485-f8994fb08c8c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 524ad97d02192a19198891c79c07f875a738fc30
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094533"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2010"></a>安装用于 SharePoint 2010 的 Reporting Services SharePoint 模式
  本主题中的过程将指导您完成以 SharePoint 模式在单台服务器上安装 Reporting Services 报表服务器。 涉及的步骤包括运行 SQL Server 安装向导以及使用 SharePoint 2010 管理中心的其他配置任务。 本主题还可用于针对现有安装的单独过程，例如创建 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。 有关添加其他信息[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服务器到现有场，请参阅[向场中添加另一个报表服务器&#40;SSRS 横向扩展&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)并[添加其他 Reporting Services Web场的前端](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 单台服务器安装对于开发和测试方案很有用，但不建议用于生产环境。  
  
> [!NOTE]  
>  有关升级和现有[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]到 SharePoint 模式安装[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，请参阅[升级和迁移 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。  
  

  
##  <a name="bkmk_prereq"></a> 先决条件  
  
-   > [!IMPORTANT]  
    >  配置和管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式不再需要或支持 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器。 使用 SharePoint 管理中心在 SharePoint 模式中配置报表服务器。 有关详细信息，请参阅[管理 Reporting Services SharePoint 服务应用程序](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)。  
  
-   查看以下要求主题，包括针对 SharePoint 2010 产品的要求：  
  
    -   [联机发行说明](https://msdn.microsoft.com/library/dn169381.aspx)
  
    -   [使用 SharePoint 2010 场中的 SQL Server BI 功能的指南](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
-   本主题不涉及安装 SharePoint 2010 产品。 有关详细信息，请参阅[使用 SharePoint 2010 场中 SQL Server BI 功能的指南](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)。  
  
-   以下过程用于配置 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器，但不适用于报表服务器的以前版本。 以前版本的报表服务器未使用 SharePoint Shared Service 体系结构。 例如，SQL Server 2008 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器和 SQL Server 2008 R2 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器。  
  
-   验证是否**SharePoint 2010 管理**Windows 服务器管理器中启动服务。  
  
 ![单服务器安装的 SSRS 组件](../../../2014/sql-server/install/media/rs-deployment-1-server.gif "单服务器安装的 SSRS 组件")  
  
### <a name="database-considerations-for-a-single-server-configuration"></a>单服务器配置的数据库注意事项  
  
-   Reporting Services 和 SharePoint 产品及技术均使用 SQL Server 关系数据库来存储应用程序数据。  
  
-   [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 需要兼容的 SQL 引擎的 SQL Server 评估版实例。  
  
-   SharePoint 产品可以使用现有的数据库实例。 如果未安装数据库引擎的实例，SharePoint 产品安装程序安装 SQL Server Express Edition 以用于 SharePoint 应用程序数据库。  
  
-   报表服务器实例不能将 SQL Server Express Edition 用于其数据库。 但是，由 SharePoint 产品安装的 SQL Server Express Edition 实例可与其他数据库引擎版本并存。  
  

  
##  <a name="bkmk_install_SSRS"></a> 在 SharePoint 模式下安装 Reporting Services 报表服务器  
  
1.  运行 SQL Server 安装向导。  
  
2.  在向导的左侧单击 **“安装”** ，然后单击 **“全新 SQL Server 独立安装或向现有安装添加功能”** 。  
  
3.  在 **“安装程序支持规则”** 页上单击 **“确定”** ，假定所有规则均已通过验证。  
  
4.  在 **“安装程序支持文件”** 页中，单击 **“安装”** 。  
  
5.  单击**下一步**的支持文件已完成安装并且支持规则显示的状态后**传递**。 查看任何警告或妨碍安装的问题。  
  
6.  上**产品密钥**页上，键入你的密钥或接受 Enterprise Evaluation edition 的默认值。  
  
     单击“下一步”  。  
  
7.  阅读并接受许可条款。 对于您单击以同意发送功能使用情况数据来帮助改进产品功能和支持，Microsoft 深表感谢。  
  
     单击“下一步”  。  
  
8.  选择**SQL Server 功能安装**上**安装角色**页。  
  
     单击 **“下一步”**  
  
     ![安装角色的 SQL Server 功能安装](../../../2014/sql-server/install/media/rs-setuprole.gif "SQL Server Feature Installation for setup role")  
  
9. 在 **“功能选择”** 页中，选择以下选项：  
  
    -   **Reporting Services - SharePoint**  
  
    -   **Reporting Services 外接程序用于 SharePoint 2010 产品**。 ![请注意](../../../2014/reporting-services/media/rs-fyinote.png "注意")安装外接程序的安装向导选项是使用新[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]发布。  
  
    -   如果您尚未安装 SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例，则还可以选择 **“数据库引擎服务”** 和 **“管理工具 - 完整”** 以提供一个完整环境。  
  
     单击“下一步”  。  
  
     ![SharePoint 模式下的 SSRS 功能选择](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "SharePoint 模式下的 SSRS 功能选择")  
  
10. 单击**下一步**上**安装规则**页。 查看任何警告或妨碍安装的问题。  
  
11. 如果您已选择“数据库引擎服务”，请在 **“实例配置”** 页上接受 **MSSQLSERVER** 的默认实例，然后单击 **“下一步”** 。 与以前的 Reporting Services 体系结构不同，Reporting Services 共享服务体系结构不基于 SQL Server“实例”。  
  
12. 阅读 **“磁盘空间要求”** 页，然后单击 **“下一步”** 。  
  
13. 上**服务器配置**页上键入相应的凭据。 如果您要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据警报或订阅功能，则需要将 SQL Server 代理的 **“启动类型”** 更改为 **“自动”** 。  
  
     单击“下一步”  。  
  
14. 如果您选择了“数据库引擎服务”，您将看到 **“数据库引擎配置”** 页。请将相应的帐户添加到 SQL 管理员列表，然后单击 **“下一步”** 。  
  
15. 在 **“Reporting Services 配置”** 页上，您应该看到 **“仅安装”** 选项处于选中状态。 此选项将安装报表服务器文件，但不会为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置 SharePoint 环境。SQL Server 安装完成后，您需要按照本主题的其他章节的内容配置 SharePoint 环境。 这包括安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共享服务和创建 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。  
  
     ![rs_SQL11_SETUP_SSRS_configpage_withcircles](../../../2014/sql-server/install/media/rs-kj-setup-ssrs-configpage-withcircles.gif "rs_SQL11_SETUP_SSRS_configpage_withcircles")  
  
16. 请通过在 **“错误报告”** 页上单击用于发送错误报告的复选框，来帮助 Microsoft 改进 SQL Server 功能和服务。  
  
     单击“下一步”  。  
  
17. 查看任何警告，然后在 **“安装配置规则”** 页上单击 **“下一步”** 。  
  
18. 在 **“准备安装”** 页上，查看安装摘要，然后单击 **“下一步”** 。 该摘要将包含**Reporting Services**将包含的安装模式值的节点**SharePointFilesOnlyMode**以及帐户信息。  
  

  
##  <a name="bkmk_install_SSRS_sharedservice"></a> 安装并启动 Reporting Services SharePoint 服务  
 ![与 PowerShell 相关的内容](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell related content")  
  
> [!NOTE]  
>  如果要安装到现有 SharePoint 场**不需要**完成本部分中的步骤。 在上一节中运行 SQL Server 安装向导时，已安装并已启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 服务。  
  
 在执行 SQL Server 安装向导的过程中已安装了必需的文件，但需要将服务注册到 SharePoint 场中。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本引入了对 SharePoint 模式下的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 PowerShell 支持。 以下步骤将指导您完成打开 SharePoint Management Shell 并运行 cmdlet 的过程：  
  
1.  单击 **“开始”** 按钮  
  
2.  单击**Microsoft SharePoint 2010 产品**组。  
  
3.  右键单击**SharePoint 2010 Management Shell**单击**以管理员身份运行**。  
  
4.  运行以下 PowerShell 命令以安装 SharePoint 服务。 命令成功完成后会在 Management Shell 中显示一个新行。 当命令成功完成时，不会向 Management Shell 返回任何消息：  
  
    ```  
    Install-SPRSService  
    ```  
  
5.  运行以下 PowerShell 命令以安装服务代理：  
  
    ```  
    Install-SPRSServiceProxy  
    ```  
  
6.  运行以下 PowerShell 命令以启动服务，或者查看下面的注释以了解有关从 SharePoint 管理中心启动服务的说明：  
  
    ```  
    get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 您也可以通过 SharePoint 管理中心（而不是通过运行第三个 PowerShell 命令）来启动服务。 以下步骤还用于验证服务是否正在运行。  
  
1.  在 SharePoint 管理中心的 **“系统设置”** 组中，单击 **“管理服务器上的服务”** 。  
  
2.  找到 **“SQL Server Reporting Services 服务”** ，然后在“操作”列中单击 **“启动”** 。  
  
3.  Reporting Services 服务的状态将从 **“已停止”** 更改为 **“已启动”** 。 如果 Reporting Services 服务不在列表中，则使用 PowerShell 安装该服务。  
  
    > [!NOTE]  
    >  如果 Reporting Services 服务停留在**起始**状态并且未更改为**已启动**，验证 SharePoint 2010 管理服务已启动 Windows 服务器管理器中。  
  

  
##  <a name="bkmk_create_serrviceapplication"></a> 创建 Reporting Services 服务应用程序  
 本节提供您在查看现有服务应用程序的情况下，用于创建服务应用程序的步骤和属性说明。  
  
1.  在 SharePoint 管理中心的 **“应用程序管理”** 组中，单击 **“管理服务应用程序”** 。  
  
2.  在 SharePoint 功能区中，单击 **“新建”** 按钮。  
  
3.  在“新建”菜单中，单击 **“SQL Server Reporting Services 服务应用程序”** 。  
  
    > [!WARNING]  
    >  如果[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]选项不会出现在列表中，则**指示的[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]共享的服务未安装**。 查看上一节，了解如何使用 PowerShell cmdlt 安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务。  
  
4.  在 **“创建 SQL Server Reporting Services 服务应用程序”** 页中，输入应用程序的名称。 如果您要创建多个 Reporting Services 服务应用程序，则描述性名称或命名约定可帮助您组织您的管理操作。  
  
5.  在 **“应用程序池”** 部分中，为该应用程序创建一个新应用程序池（推荐）。 使用与服务应用程序相同的名称作为新应用程序池的名称，这可以使您正在进行的管理更加容易。  
  
     为该应用程序池选择或创建一个托管帐户。 请确保指定一个域用户帐户。 通过域用户帐户，可以使用 SharePoint 的托管帐户功能，从而使您可以在一个位置中更新密码和帐户信息。 如果您计划扩展部署以便包括将在同一标识下运行的附加服务实例，则域帐户也是必需的。  
  
6.  在 **“数据库服务器”** 中，您可以使用当前服务器或选择其他 SQL Server。  
  
7.  在 **“数据库名称”** 中，默认值是 `ReportingService_<guid>`，这是唯一的数据库名称。 如果您键入一个新值，请键入唯一值。  
  
8.  在 **“数据库身份验证”** 中，默认值是 “Windows 身份验证”。 如果您选择 **“SQL 身份验证”** ，请参考 SharePoint 管理员指南以便了解有关如何在 SharePoint 部署中使用此身份验证类型的最佳实践。  
  
9. 在 **“Web 应用程序关联”** 部分中，选择要设置为供当前 Reporting Services 服务应用程序访问的 Web 应用程序。 可以将一个 Reporting Services 服务应用程序与一个 Web 应用程序相关联。 如果所有当前 Web 应用程序均已与一个 Reporting Services 服务应用程序相关联，将显示警告消息。  
  
10. 单击“确定”  。  
  
11. 用于创建服务应用程序的过程可能会需要几分钟才能完成。 当它完成时，将显示确认消息和一个指向 **“设置订阅和警报”** 页的链接。 如果您要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 订阅和警报功能，请完成该设置步骤。 有关详细信息，请参阅[用于 SSRS 服务应用程序的设置订阅和警报](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)。  
  
 ![PowerShell 相关内容](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 相关内容")有关使用 PowerShell 创建的信息[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服务应用程序，请参阅[创建 Reporting Services 服务应用程序使用 PowerShell](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp)。  
  

  
##  <a name="bkmk_powerview"></a> 激活 Power View 网站集功能。  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]一项功能[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]外接程序[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition 是一个网站集功能。 自动为根网站集和安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序后创建的网站集激活该功能。 如果您计划使用 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]，请验证已激活该功能。  
  
 如果在安装 SharePoint 2010 产品后安装了用于 SharePoint 2010 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序，则仅对根网站集激活报表服务器集成功能和 Power View 集成功能。 对于其他网站集，请手动激活这些功能。  
  
#### <a name="to-activate-the-power-view-feature"></a>激活 Power View 功能  
  
1.  打开浏览器找到所需的 SharePoint 网站。  
  
2.  单击 **“网站操作”** 。  
  
3.  单击 **“网站设置”** 。  
  
4.  在网站集管理组中单击 **“网站集功能”** 。  
  
5.  在列表中找到 **“Power View 集成功能”** 。  
  
6.  单击 **“激活”** 。  
  
 将对每个网站集完成此过程。 有关详细信息，请参阅[激活报表服务器和 Power View 集成功能在 SharePoint 中](../../reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)。  
  
##  <a name="bkmk_additional_config"></a> 附加配置  
 本部分介绍在大多数 SharePoint 部署中很重要的其他配置步骤。  
  
###  <a name="bkmk_provision_agent"></a> 设置订阅和警报  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 订阅和数据警报功能可能要求配置 SQL Server 代理权限。 如果您看到指示“需要 SQL Server 代理”的错误消息，而您已验证 SQL Server 代理正在运行，则应更新权限。 您可以在“创建服务应用程序成功”页上单击链接 **“设置订阅和警报”** ，以便转到其他页来设置 SQL Server 代理。 如果您的部署是跨计算机边界的部署（例如，当 SQL Server 数据库实例位于其他计算机上时），会需要此设置步骤。 有关详细信息，请参阅 [用于 SSRS 服务应用程序的设置订阅和警报](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  

  
### <a name="configure-e-mail-for-a-service-application"></a>为服务应用程序配置电子邮件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据警报功能会在电子邮件中发送警报。 若要发送电子邮件，您可能需要配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序，并可能需要修改该服务应用程序的电子邮件传递扩展插件。 如果您计划将电子邮件传递扩展插件用于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 订阅功能，则需要进行电子邮件设置。 有关详细信息，请参阅[为 Reporting Services 服务应用程序配置电子邮件（SharePoint 2010 和 SharePoint 2013）](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  

  
### <a name="add-reporting-services-content-types"></a>添加 Reporting Services 内容类型  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供预定义的内容类型，用于管理共享数据源 (.rsds) 文件、报表模型 (.smdl) 和报表生成器报表定义 (.rdl) 文件。 将 **“报表生成器报表”** 、 **“报表模型”** 和 **“报表数据源”** 内容类型添加到库中将启用 **“新建”** 命令，以便创建对应类型的新文档。 有关详细信息，请参阅[将报表服务器内容类型添加到库&#40;在 SharePoint 集成模式下的 Reporting Services&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)。  
  

  
### <a name="activate-the-file-sync-feature"></a>激活文件同步功能  
 如果用户经常直接将已发布的报表项上载到 SharePoint 文档库，则报表服务器文件同步功能将很有用。 文件同步功能将更频繁地将报表服务器目录与文档库中的项进行同步。 有关详细信息，请参阅 [在 SharePoint 管理中心中激活报表服务器文件同步功能](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)。  
  
## <a name="see-also"></a>请参阅  
 [用于 Reporting Services SharePoint 模式的 PowerShell cmdlet](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [SQL server 2012 各个版本支持的功能](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Reporting Services SharePoint 服务和服务应用程序](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)  
  
  
