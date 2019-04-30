---
title: Reporting Services 报表服务器（SharePoint 模式） | Microsoft Docs
ms.prod: sql-server-2014
ms.technology:
- reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 246b0be389857e002e5c9e30cb899826234a58b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273841"
---
# <a name="reporting-services-report-server-sharepoint-mode"></a>Reporting Services 报表服务器（SharePoint 模式）

为 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式 **配置的** 报表服务器可在 SharePoint 产品的部署中运行。 SharePoint 模式下的报表服务器可针对报表和其他 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 内容类型使用 SharePoint 的协作和管理功能。 SharePoint 模式要求在 SharePoint Web 前端上安装用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序的适当版本。  
  
有关安装和配置的详细信息，请参阅下面的内容：  
  
- [安装适用于 SharePoint 2013 的 Reporting Services SharePoint 模式](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
- [安装用于 SharePoint 2010 的 Reporting Services SharePoint 模式](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)。  
  
- [向场中添加另一个报表服务器&#40;SSRS 横向扩展&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)。  
  
 什么是此版本中的新增功能的信息，请参阅中的 SharePoint 部分[What's New &#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)。  
  
 **本主题内容：**  
  
-   [功能摘要](#bkmk_featuresum)  
  
-   [连接模式和本地模式](#bkmk_connectedandlocal)  
  
-   [不支持的 SharePoint 功能](#bkmk_unsupportedsharepoint)  
  
-   [支持的 SharePoint 外接程序与报表服务器之间的组合](#bkmk_supportedcombinations)  
  
-   [提供集成的组件](#bkmk_components)  
  
-   [语言注意事项](#bkmk_language)  
  
-   [相关任务](#bkmk_relatedtasks)  
  
##  <a name="bkmk_featuresum"></a> 功能摘要

 将报表服务器配置为在 SharePoint 集成模式下运行可获得以下附加功能（只有在以此模式部署报表服务器时才能获得这些功能）：  
  
-   使用 SharePoint 文档管理和协作功能，包括警报。 SharePoint 站点为从一个位置访问和管理所有报表项提供了统一的门户。  
  
-   使用 SharePoint 的权限和身份验证提供程序控制对报表、模型和其他项的访问。  
  
-   使用 SharePoint 的部署拓扑通过防火墙外部的 Internet 连接来分发报表。 报表服务器可在针对 Internet 访问进行配置的大型 SharePoint 部署环境中提供报表和数据处理服务。  
  
-   在 SharePoint 站点的自定义应用程序页中管理报表、模型、数据源、计划和报表历史记录。 可以在 SharePoint 站点中设置属性、定义计划和订阅以及创建和管理报表历史记录，其方式与使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的其他工具创建和管理它们的方式完全相同。  
  
-   将报表、报表模型、资源以及共享数据源文件发布或上载到 SharePoint 库，包括 Office SharePoint Server 中的报表中心。  
  
     使用报表设计器、模型设计器和报表生成器来创建要直接发布到 SharePoint 库的报表和数据源。 此外，您还可以在 SharePoint 站点中使用上载操作，将所有报表定义和报表模型添加到 SharePoint 库。  
  
     因为无论使用何种服务器模式，报表服务器均以相同方式处理报表定义，因此报表数据和布局不受服务器模式的影响。 任何可以在本机模式的报表服务器中运行的报表也能够在配置为 SharePoint 集成模式的报表服务器中运行。  
  
-   使用新的 SharePoint 传递扩展插件向 SharePoint 库订阅和将报表传递到 SharePoint 库。 您还可以通过电子邮件传递报表或将报表传递到共享文件夹。 报表服务器传递扩展插件用于传递报表。 对于使用在运行时查询的订阅服务器数据的大规模报表分发，可以创建数据驱动的订阅。  
  
-   可以使用您添加到 SharePoint 页的报表查看器 Web 部件来查看 SharePoint Web 应用程序中的报表。 该 Web 部件包括页面导航、搜索、打印和导出功能。  
  
-   针对新的 SOAP 端点进行编程，以创建与 SharePoint 站点集成的自定义应用程序。 此外，您还可以使用经过更新的 Windows Management Instrumentation (WMI) 提供程序，以编程方式对在 SharePoint 集成模式下运行的报表服务器实例进行配置。  
  
-   连接模式下的 Microsoft Access 服务报告。  
  
-   AAM 区域、面向 internet 的部署以及针对 SharePoint 列表的 SharePoint 用户标记。  
  
##  <a name="bkmk_connectedandlocal"></a> 连接模式和本地模式

 SQL Server 2008 R2 版本引入了新的“本地模式”，可用于从安装了用于 SharePoint 2010 产品的 Microsoft SQL Server 2008 R2 或更高版本的 Reporting Services 外接程序的 SharePoint 2010 服务器查看报表。  
  
-   *本地模式下*:本地模式允许在本地从 SharePoint 文档库呈现报表，而无需与 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器集成。 用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序是必需的，但 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器不是。 外接程序可以以多种不同的方式进行安装，包括 SharePoint 2010 产品准备工具。 有关本地模式的详细信息，请参阅[报表查看器中的本地模式和连接模式下的报表在报表查看器中&#40;SharePoint 模式下的 Reporting Services&#41; ](../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)并[在哪里可以找到 Reporting Services 外接程序用于 SharePoint 产品](install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。  
  
-   *连接模式*:通过集成支持连接的模式[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]到 SharePoint 场中使用 SharePoint 管理中心的报表服务器。 与报表服务器的集成可以实现完整的端到端报告，提供 SharePoint 2010 的协作功能以及基于服务器功能，报表服务器包括：订阅、 快照和基于服务器处理。  
  
##  <a name="bkmk_unsupportedsharepoint"></a> 不支持的 SharePoint 功能

 并非所有的 SharePoint 功能对于集成操作都可用。 以下是 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 未直接集成的 SharePoint 功能的列表：  
  
-   Secure Store Service。  
  
-   您无法将 SharePoint 的 Outlook 日历集成功能或 SharePoint 的计划功能用于文档库中的报表服务文件。  
  
-   SharePoint 业务数据目录。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 页也不支持 SharePoint 个性化。 如果对 SharePoint Web 应用程序启用匿名访问，则不支持报表服务器集成。  
  
-   SQL Server Reporting Services  不支持 SharePoint 文档库版本控制。 如果将报表项保存在启用“文档版本历史记录”配置的文档库中，则 Reporting Services 功能将不能正确操作并会在 ULS 日志中生成错误。 下面是 ULS 日志中错误的示例：  
  
    -   “… 与报表关联的数据源已禁用”。  
  
     文档库版本历史记录是在“库设置”的“版本控制设置”页面上配置的。  
  
##  <a name="bkmk_supportedcombinations"></a> 支持的 SharePoint 外接程序与报表服务器之间的组合

 在报表服务器、SharePoint 的 Reporting Services 外接程序和 SharePoint 产品的所有组合中，并非所有功能都受支持。 有关详细信息，请参阅[支持组合的 SharePoint 和 Reporting Services 服务器与外接程序&#40;SQL Server 2014&#41;](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  必须将 Reporting Services 外接程序的正确版本与 SharePoint 产品的对应版本结合使用。  
  
##  <a name="bkmk_components"></a> 提供集成的组件

 若要在单个部署中组合服务器，可以将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的安装与 SharePoint 产品的实例集成  
  
 集成是通过 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序提供的。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序是一个免费分发组件，可下载该组件，然后安装在运行 SharePoint 适当版本的服务器上。  
  
> [!TIP]  
>  在报表服务器、SharePoint 的 Reporting Services 外接程序和 SharePoint 产品的所有组合中，并非所有功能都受支持。 有关详细信息，请参阅[支持组合的 SharePoint 和 Reporting Services 服务器与外接程序&#40;SQL Server 2014&#41;](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)。  
  
-   在 SharePoint 上， [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序提供 ReportServer 代理终结点、一个报表查看器 Web 部件和多个应用程序页面，以便你可以查看、存储和管理 SharePoint 站点或场中的报表服务器内容。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供更新后的程序文件、SOAP 端点以及自定义安全性和传递扩展插件。 必须将报表服务器配置为在 SharePoint 集成模式下运行，该模式专门支持通过 SharePoint 站点实现报表访问和传递。  
  
 在 SharePoint 上安装 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序并将这两个服务器进行集成配置后，您可以将报表服务器内容类型上载或发布到 SharePoint 库，然后从 SharePoint 站点查看和管理这些文档。 上传或发布报表服务器内容是至关重要的第一步。选择 SharePoint 站点中的报表定义 (.rdl)、报表模型 (.smdl) 及共享数据源 (.rsds) 后，才可以访问 Web 部件和页面。  
  
##  <a name="bkmk_language"></a> 语言注意事项

 [!INCLUDE[SPF2010](../includes/spf2010-md.md)] 和 [!INCLUDE[SPS2010](../includes/sps2010-md.md)] 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 如果将报表服务器配置为在部署的 SharePoint 产品之内运行，则可能会出现混合使用多种语言的情况。 用户界面、文档和消息将以下列语言显示：  
  
-   来自 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的所有应用程序页、工具、错误、警告和消息将使用某个 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 语言版本中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例所使用的语言。  
  
-   在 SharePoint 站点、报表查看器 Web 部件和报表生成器中打开的应用程序页都将以 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序支持的语言中的一种显示。 若要查看支持的语言列表，请转到 [SQL Server 下载](https://msdn.microsoft.com/sql/downloads/)，并找到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序的下载页。  
  
-   SharePoint 站点、SharePoint 管理中心、联机帮助和消息可使用 Office Server 产品支持的语言。  
  
 如果 SharePoint 产品或技术的语言与报表服务器的语言不同， [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 将尝试从同一个语系中选择一种最接近的语言。 如果无法找到最接近的替代语言，报表服务器将使用英语。  
  
##  <a name="bkmk_relatedtasks"></a> 相关任务

 下表汇总了与 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式报表服务器有关的任务：  
  
|**任务**|**链接**|  
|--------------|--------------|  
|在 SharePoint 模式下安装和配置 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的详细步骤。|[安装 Reporting Services SharePoint 模式下用于 SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)并[向场中添加另一个报表服务器&#40;SSRS 横向扩展&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)。|  
|通过添加其他报表服务器扩展 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 部署。|[向场中添加另一个报表服务器&#40;SSRS 横向扩展&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)并[SharePoint 中的 SQL Server BI 功能的部署拓扑](../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)。|  
|添加安装了 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 组件用于查看报表项的其他 SharePoint Web 前端。|[向场中添加另一个 Reporting Services Web 前端](install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|为 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 数据警报和订阅功能配置电子邮件。|[为 Reporting Services 服务应用程序配置电子邮件（SharePoint 2010 和 SharePoint 2013）](install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|有关此版本的最新信息，位于 TechNet Wiki 上。|[SQL Server 2012 Reporting Services 提示、技巧和故障排除](https://go.microsoft.com/fwlink/?LinkId=221297)。|  
  
## <a name="see-also"></a>请参阅  
 [安装或卸载 Reporting Services 外接程序的 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41; ](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md) [硬件和软件要求的 Reporting Services SharePoint 模式下的](../../2014/sql-server/install/hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode.md) [SharePoint 站点上的报表查看器 Web 部件](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)