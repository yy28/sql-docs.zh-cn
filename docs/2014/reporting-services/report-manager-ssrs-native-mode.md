---
title: 报表管理器 （SSRS 本机模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], managing
- Report Manager [Reporting Services], about Report Manager
- customizing Report Manager
- Report Manager [Reporting Services], customizing
- report servers [Reporting Services], administering
- browsing reports [Reporting Services]
- administering reports
- Report Manager [Reporting Services]
- components [Reporting Services], Report Manager
ms.assetid: 80949f9d-58f5-48e3-9342-9e9bf4e57896
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 31e64dfe871fa38daee266814006468a8ea32e65
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59940663"
---
# <a name="report-manager--ssrs-native-mode"></a>报表管理器（SSRS 本机模式）
  报表管理器是基于 Web 的报表访问和管理工具，用于通过 HTTP 连接来管理远程位置的单个报表服务器实例。 您还可以使用报表管理器的报表查看器和导航功能。 本主题内容：  
  
-   [什么是报表管理器？](#bkmk_whatis_report_manager)  
  
-   [启动和使用报表管理器](#bkmk_start_report_manager)  
  
-   [图标说明](#bkmk_icon_descriptions)  
  
##  <a name="bkmk_whatis_report_manager"></a> 什么是报表管理器？  
 可以使用报表管理器执行以下任务：  
  
-   查看、搜索、打印和订阅报表。  
  
-   创建、保护和维护文件夹层次结构，以便组织服务器上的项。  
  
-   配置基于角色的安全性，确定对项和操作的访问权限。  
  
-   配置报表执行属性、报表历史记录和报表参数。  
  
-   创建报表模型，使用这些报表模型可以连接到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 关系数据源，并从这些数据源中检索数据。  
  
-   设置模型项安全性，以便可以访问模型中的特定实体，或将实体映射到事先创建的预定义点击链接型报表。  
  
-   创建共享计划和共享数据源，以提高计划和数据源连接的可管理性。  
  
-   创建可以将报表展开为大型收件人列表的数据驱动订阅。  
  
-   创建链接报表，以便按不同方式重用现有报表和重新确定其用途。  
  
-   启动报表生成器来创建可以在报表服务器上保存和运行的报表。  
  
 使用报表管理器可以浏览报表服务器文件夹或搜索特定报表。 可以查看报表、报表的常规属性以及在报表历史记录中捕获的报表以前的副本。 根据权限，可能还可以订阅报表，以便将其传递到电子邮件收件箱或文件系统中的共享文件夹。  
  
> [!NOTE]  
>  有关支持的浏览器和版本的信息，请参阅[规划 Reporting Services 和 Power View 浏览器支持&#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)。  
  
 报表管理器只能供在本机模式下运行的报表服务器使用。 配置为 SharePoint 集成模式的报表服务器不支持报表管理器。  
  
 仅在特定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本中才提供某些报表管理器功能。 有关详细信息，请参阅 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 如果是全新安装，则只有本地管理员有足够的权限来处理内容和设置。 若要对其他用户授予权限，本地管理员必须创建角色分配，以便提供对报表服务器的访问权限。 用户随后可以访问的应用程序页和任务将取决于该用户的角色分配。 有关详细信息，请参阅 [授予用户对报表服务器的访问权限（报表管理器）](security/grant-user-access-to-a-report-server.md)。  
  
 如果您在使用 [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)] 或 Windows Server 2008，则必须配置报表管理器以便进行本地管理。 有关详细信息，请参阅 [为本地管理配置本机模式报表服务器 (SSRS)](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
##  <a name="bkmk_start_report_manager"></a> 启动和使用报表管理器  
 报表管理器是一种 Web 应用程序，您可通过在浏览器窗口的地址栏中键入报表管理器 URL 的方式来将其打开。 启动报表管理器时，基于您在报表服务器中拥有的权限，所看到的页面、链接和选项会有所不同。 若要执行某项任务，必须为自己分配包括该任务的角色。 如果为某用户分配了具有完整权限的角色，则该用户可以访问用来管理报表服务器的所有应用程序菜单和页。 如果为某用户分配的角色具有查看和运行报表的权限，则该用户只能看到支持这些活动的菜单和页。 对于不同的报表服务器，甚至对于存储在单个报表服务器上的不同报表和文件夹，每个用户可以具有不同的角色分配。  
  
 有关角色的详细信息，请参阅 [授予对本机模式报表服务器的权限](security/granting-permissions-on-a-native-mode-report-server.md)。  
  
> [!NOTE]  
>  如果使用的是 Windows Vista 或 Windows Server 2008，则在使用报表管理器来管理本地报表服务器实例之前，必须配置报表服务器进行本地管理。 有关如何配置服务器的说明，请参阅[为本地管理配置本机模式报表服务器&#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
## <a name="start-report-manager"></a>启动报表管理器  
  
#### <a name="to-start-report-manager-from-a-browser"></a>从浏览器启动报表管理器  
  
1.  打开 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 7.0 或更高版本。  
  
2.  在 Web 浏览器的地址栏中，键入报表管理器 URL。  
  
    -   默认情况下，URL 为 `http://[ComputerName]/reports`。  
  
    -   报表服务器可能已配置为使用特定的端口。 例如， `http:// [ComputerName]:80/reports` 或 `http:// [ComputerName]:8080/reports`。  
  
## <a name="configuring-report-manager"></a>配置报表管理器  
 报表管理器配置包含为应用程序定义 URL 的过程。 如果部署包括在单独的计算机上运行报表管理器，则还需要进行其他配置。  
  
 可以自定义报表管理器，但可自定义的方式非常有限。 例如，您可以在“站点设置”页上修改应用程序标题。 如果您是 Web 开发人员，则可以修改包含报表管理器所用样式信息的样式表。 由于没有专门对报表管理器进行设计以支持自定义，因此，必须对所做的任何修改进行全面测试。 如果发现报表管理器不能满足您的需要，则可以开发自定义报表查看器，或者配置 SharePoint Web 部件以便在 SharePoint 站点中找到和查看报表。 有关详细信息，请参阅[配置报表管理器（本机模式）](report-server/configure-web-portal.md)。  
  
##  <a name="bkmk_icon_descriptions"></a> 图标说明  
 下表对报表管理器中使用的图标进行了说明。 有关报表工具栏中显示的图标的详细信息，请参阅[HTML 查看器和报表工具栏](html-viewer-and-the-report-toolbar.md)。  
  
|图标|Description|操作|  
|----------|-----------------|------------|  
|![报表图标](media/hlp-16doc.gif "报表图标")|报告|单击报表图标或名称可打开该报表。 该报表将在单独的窗口中打开。|  
|![模型图标](media/model-icon.gif "Model icon")|报表模型|单击报表模型图标可打开模型属性页。|  
|![链接报表图标](media/hlp-16linked.gif "链接报表图标")|链接报表|单击报表图标或名称可打开链接报表。 该报表将在单独的窗口中打开。|  
|![文件夹图标](media/hlp-16folder.gif "文件夹图标")|文件夹|单击文件夹图标或名称可打开该文件夹。|  
|![订阅图标](media/hlp-16subscription.gif "订阅图标")|订阅|单击订阅图标或说明可编辑相应的订阅。|  
|![数据驱动订阅图标](media/hlp-16subscriptiondd.gif "数据驱动订阅图标")|数据驱动订阅|单击数据驱动订阅图标或说明可编辑相应的订阅。|  
|![通用资源图标](media/hlp-16file.gif "通用资源图标")|资源|单击资源图标或名称可打开该资源。 该资源将在单独的窗口中打开。|  
|![共享数据源图标](media/hlp-16datasource.png "共享数据源图标")|共享数据源项|单击共享数据源图标可打开数据源的属性页、报表列表和订阅列表。|  
|![属性页图标](media/hlp-16prop.gif "属性页图标")|属性页|单击属性图标可访问其他页面来设置属性和安全性。|  
  
## <a name="see-also"></a>请参阅  
 [配置 URL（SSRS 配置管理器）](install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [规划 Reporting Services 和 Power View 浏览器支持的&#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)   
 [报表生成器&#40;SSRS&#41;](tools/report-builder-authoring-environment-ssrs.md)   
 [Reporting Services 工具](tools/reporting-services-tools.md)   
 [报表服务器内容管理（SSRS 本机模式）](report-server/report-server-content-management-ssrs-native-mode.md)   
 [查看和浏览本机模式下使用 SharePoint Web 部件的报表&#40;SSRS&#41;](reports/view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
