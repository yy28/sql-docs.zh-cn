---
title: 管理中心中的 PowerPivot 服务器管理和配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2cdbfdc5-45a9-4000-a03d-318cc7ac8fe9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: de72001ced1b7e2690f90b2de4c59bb35aca6ce4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071105"
---
# <a name="powerpivot-server-administration-and-configuration-in-central-administration"></a>在管理中心中管理和配置 PowerPivot 服务器
  PowerPivot 服务器管理和配置由 SharePoint 服务应用程序管理员使用 SharePoint 管理中心来执行。  
  
 PowerPivot for SharePoint 必须先进行配置，然后才能使用。 使用 SQL Server 安装程序安装 PowerPivot for SharePoint 后，您可以使用以下任意方法来配置它：  
  
-   PowerPivot 配置工具或 PowerPivot for SharePoint 2013 配置工具  
  
-   SharePoint 管理中心  
  
-   PowerShell cmdlet  
  
 这三种方法都提供完全配置的服务器。  
  
 本节包含使用管理中心配置软件的任务。 至少必须执行下面列表中所列的所有三个必需的配置任务。  
  
> [!IMPORTANT]  
>  对于 SharePoint 2010，必须首先安装 SharePoint 2010 Service Pack 1 (SP1)，然后您才能配置 PowerPivot for SharePoint 或使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 数据库服务器的 SharePoint 场。 如果您尚未安装 Service Pack，则应立即安装 Service Pack，然后再开始配置服务器。  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-central-administration"></a>使用管理中心配置 PowerPivot for SharePoint 的好处  
 SharePoint 管理中心是 SharePoint 场的管理应用程序。 如果您是场管理员，可能想在向场中添加 PowerPivot for SharePoint 实例时使用熟悉的工具。  
  
 与 PowerPivot 配置工具或 PowerShell cmdlet 相比，管理中心提供一些页面，这些页面指定在您配置应用程序或服务器时可能设置的所有选项。 而其他方法要么将配置工作流缩减为更少的步骤，要么需要预先掌握如何使用 PowerShell 配置 SharePoint 服务器的知识。  
  
## <a name="related-content"></a>相关内容  
 [使用 Windows PowerShell 配置 PowerPivot](power-pivot-configuration-using-windows-powershell.md)  
  
 [PowerPivot Configuration Tools](power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
|链接|类型|任务说明|  
|----------|----------|----------------------|  
|[将 PowerPivot 解决方案部署到 SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)|必须|此步骤安装解决方案文件，这些文件将程序文件和应用程序页添加到场和站点集合。|  
|[在管理中心中创建和配置 PowerPivot 服务应用程序](create-and-configure-power-pivot-service-application-in-ca.md)|必须|此步骤设置 PowerPivot 系统服务。|  
|[在管理中心中针对网站集激活 PowerPivot 功能集成](activate-power-pivot-integration-for-site-collections-in-ca.md)|必须|此步骤在站点集合级别启用 PowerPivot 功能。|  
|[将 MSOLAP.5 添加为 Excel Services 中的受信任数据访问接口](add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|必须|此步骤将 Analysis Services OLE DB 访问接口添加为 Excel Services 中的受信访问接口。|  
|[使用 SharePoint 2010 进行 PowerPivot 数据刷新](../powerpivot-data-refresh-with-sharepoint-2010.md)|建议|数据刷新是可选的，但建议执行刷新。 它允许您对已发布的 Excel 工作簿中的 PowerPivot 数据计划执行无人参与的更新。|  
|[将 PowerPivot 无人参与的数据刷新帐户配置 &#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)|建议|此步骤设置特殊目的的帐户，该帐户可用于在服务器上运行数据刷新作业。|  
|[为 &#40;配置使用情况数据收集 PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|可选|默认情况下，配置使用情况数据收集。 您可以使用这些步骤修改默认设置。|  
|[配置专用数据刷新或仅限查询的处理 &#40;PowerPivot for SharePoint&#41;](../configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)|可选|一个 PowerPivot 实例可以专用于数据刷新作业或查询。 此外，您可以修改并行数据刷新作业的默认设置。|  
|[配置 PowerPivot 服务帐户](configure-power-pivot-service-accounts.md)|可选|说明如何更新密码或更改服务帐户。|  
|[将 PowerPivot 服务应用程序连接到管理中心中的 SharePoint Web 应用程序](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|可选|说明如何修改服务关联。|  
|[Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|可选|说明如何将 PowerPivot 库作为受信任的位置添加。|  
|[配置和查看 SharePoint 日志文件和诊断日志记录 &#40;PowerPivot for SharePoint&#41;](configure-and-view-sharepoint-and-diagnostic-logging.md)|可选|默认情况下，配置事件日志记录。 您可以使用这些步骤修改默认设置。|  
|[PowerPivot 运行状况规则 - 配置](configure-power-pivot-health-rules.md)|可选|默认情况下，配置服务器运行状况规则。 您可以使用这些步骤修改一些默认设置。|  
|[创建和自定义 PowerPivot 库](create-and-customize-power-pivot-gallery.md)|可选|对于手动配置的安装，此过程说明如何创建 PowerPivot 库，该库显示它包含的 PowerPivot 工作簿的缩略图。|  
|[将 BI 语义模型连接内容类型添加到库 &#40;PowerPivot for SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)|可选|说明如何扩展文档库以支持创建 BI 语义模型连接文件。|  
  
## <a name="see-also"></a>另请参阅  
 [PowerPivot for SharePoint 2010 安装](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [配置设置引用 &#40;PowerPivot for SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Disaster Recovery for PowerPivot for SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
