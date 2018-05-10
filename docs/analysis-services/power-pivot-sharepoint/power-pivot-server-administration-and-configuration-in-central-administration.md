---
title: Power Pivot 服务器管理和在管理中心的配置 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e14e6068bc5d6538eab1ec13c3a3cc37ed34fb61
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="power-pivot-server-administration-and-configuration-in-central-administration"></a>在管理中心中管理和配置 PowerPivot 服务器
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务器管理和配置由 SharePoint 服务应用程序管理员使用 SharePoint 管理中心来执行。  
  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 必须先进行配置，然后才能使用。 使用 SQL Server 安装程序安装 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 后，你可以使用以下任意方法来配置它：  
  
-   [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 配置工具或 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 2013 配置工具  
  
-   SharePoint 管理中心  
  
-   PowerShell Cmdlet  
  
 这三种方法都提供完全配置的服务器。  
  
 本节包含使用管理中心配置软件的任务。 至少必须执行下面列表中所列的所有三个必需的配置任务。  
  
> [!IMPORTANT]  
>  对于 SharePoint 2010，必须首先安装 SharePoint 2010 Service Pack 1 (SP1)，然后才能配置 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 或使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 数据库服务器的 SharePoint 场。 如果您尚未安装 Service Pack，则应立即安装 Service Pack，然后再开始配置服务器。  
  
## <a name="benefits-of-configuring-power-pivot-for-sharepoint-using-central-administration"></a>使用管理中心配置 Power Pivot for SharePoint 的好处  
 SharePoint 管理中心是 SharePoint 场的管理应用程序。 如果你是场管理员，可能想在向场中添加 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 实例时使用熟悉的工具。  
  
 与 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 配置工具或 PowerShell cmdlet 相比，管理中心提供一些页面，这些页面指定在你配置应用程序或服务器时可能设置的所有选项。 而其他方法要么将配置工作流缩减为更少的步骤，要么需要预先掌握如何使用 PowerShell 配置 SharePoint 服务器的知识。  
  
## <a name="related-content"></a>相关内容  
 [使用 Windows PowerShell 配置 Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 [Power Pivot 配置工具](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>相关任务  
  
|链接|类型|任务说明|  
|----------|----------|----------------------|  
|[将 Power Pivot 解决方案部署到 SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)|必需|此步骤安装解决方案文件，这些文件将程序文件和应用程序页添加到场和站点集合。|  
|[在管理中心中创建和配置 Power Pivot 服务应用程序](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)|必需|此步骤设置 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 系统服务。|  
|[在管理中心中针对网站集激活 Power Pivot 功能集成](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)|必需|此步骤在站点集合级别启用 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 功能。|  
|[将 MSOLAP.5 添加为 Excel Services 中的受信任数据访问接口](../../analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|必需|此步骤将 Analysis Services OLE DB 访问接口添加为 Excel Services 中的受信访问接口。|  
|[使用 SharePoint 2010 进行 Power Pivot 数据刷新](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)|建议|数据刷新是可选的，但建议执行刷新。 它允许你对已发布的 Excel 工作簿中的 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 数据计划执行无人参与的更新。|  
|[配置 Power Pivot 无人参与的数据刷新帐户 (Power Pivot for SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)|建议|此步骤设置特殊目的的帐户，该帐户可用于在服务器上运行数据刷新作业。|  
|[配置使用情况数据收集 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|選擇性|默认情况下，配置使用情况数据收集。 您可以使用这些步骤修改默认设置。|  
|[配置专用数据刷新或仅限查询的处理 (Power Pivot for SharePoint)](http://msdn.microsoft.com/en-us/5e027605-1086-4941-bb01-f315df8f829b)|選擇性|一个 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 实例可以专用于数据刷新作业或查询。 此外，您可以修改并行数据刷新作业的默认设置。|  
|[配置 Power Pivot 服务帐户](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)|選擇性|说明如何更新密码或更改服务帐户。|  
|[将 Power Pivot 服务应用程序连接到管理中心中的 SharePoint Web 应用程序](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|選擇性|说明如何修改服务关联。|  
|[在管理中心中为 Power Pivot 站点创建受信任位置](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|選擇性|说明如何将 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 库作为受信任的位置添加。|  
|[配置和查看 SharePoint 日志文件和诊断日志记录 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)|選擇性|默认情况下，配置事件日志记录。 您可以使用这些步骤修改默认设置。|  
|[配置 Power Pivot 运行状况规则](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md)|選擇性|默认情况下，配置服务器运行状况规则。 您可以使用这些步骤修改一些默认设置。|  
|[创建和自定义 Power Pivot 库](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md)|選擇性|对于手动配置的安装，此过程说明如何创建 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 库，该库显示它包含的 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 工作簿的缩略图。|  
|[将 BI 语义模型连接内容类型添加到库 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md)|選擇性|说明如何扩展文档库以支持创建 BI 语义模型连接文件。|  
  
## <a name="see-also"></a>另请参阅  
 [Power Pivot for SharePoint 2010 安装](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)   
 [配置设置参考 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [针对 Power Pivot for SharePoint 灾难恢复](http://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
