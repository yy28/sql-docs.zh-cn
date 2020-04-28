---
title: SharePoint 中 SQL Server BI 功能的部署拓扑 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 39f76bc7-94e6-4dbc-bfa5-d56f4430bb26
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 2ba357fc3910779573ffa36f3070b55c08ced8ee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388729"
---
# <a name="deployment-topologies-for-sql-server-bi-features-in-sharepoint"></a>SharePoint 中 SQL Server BI 功能的部署拓扑
  本主题将说明用于在 SharePoint 2010 和 SharePoint 2013 环境中安装 SQL Server 商业智能功能 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 的常见拓扑。 例如单服务器和三层安装。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **本主题内容：**  
  
-   [SharePoint 2013 示例部署拓扑](#bkmk_example_deployments_2013)  
  
    -   [PowerPivot for SharePoint 2013 和 Reporting Services 三服务器部署](#bkmk_bi_Sharepoint2013_3tier)  
  
    -   [PowerPivot for SharePoint 2013 单服务器部署](#bkmk_powerpivot_sharepoint2013_1server)  
  
    -   [PowerPivot for SharePoint 2013 双服务器部署](#bkmk_powerpivot_sharepoint2013_2server)  
  
    -   [PowerPivot for SharePoint 2013 三服务器部署](#bkmk_powerpivot_sharepoint2013_3server)  
  
    -   [PowerPivot for SharePoint 2013 和 Reporting Services 单服务器部署](#bkmk_powerpivot_ssrs_sharepoint2013_1server)  
  
    -   [PowerPivot for SharePoint 2013 和 Reporting Services 双服务器部署](#bkmk_powerpivot_ssrs_sharepoint2013_2server)  
  
-   [SharePoint 2010 示例部署拓扑](#bkmk_example_deployments_2010)  
  
    -   [单服务器部署](#bkmk_sharepoint2010_1server)  
  
    -   [两层部署](#bkmk_sharepoint2010_2server)  
  
    -   [三层部署](#bkmk_sharepoint2010_3server)  
  
    -   [三层扩展部署](#bkmk_sharepoint2010_scaleserver)  
  
##  <a name="sharepoint-2013-example-deployment-topologies"></a><a name="bkmk_example_deployments_2013"></a>SharePoint 2013 示例部署拓扑  
 SQL Server 安装选项 **PowerPivot for SharePoint** 不依赖于 SharePoint。 它不使用 SharePoint 对象模型或接口来支持集成。 因此， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以安装在运行 Windows Server 2008 R2 或更高版本的任何计算机上。 但是，它可以不必是 SharePoint 场中的应用程序服务器。 配置步骤之一将是将 Excel Services 指向运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的服务器。 出于负载平衡和故障容错的原因，建议安装和注册多个在 SharePoint 模式下运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器。  
  
 Sharepoint 模式要求 sharepoint server 2013，并利用 sharepoint 服务应用程序体系结构。 ** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **  
  
 下面的部分说明了典型的部署拓扑：  
  
###  <a name="powerpivot-for-sharepoint-2013-and-reporting-services-three-server-deployment"></a><a name="bkmk_bi_Sharepoint2013_3tier"></a>PowerPivot for SharePoint 2013 和 Reporting Services 三台服务器部署  
 在下面的三服务器部署中，SQL Server 数据库引擎、在 SharePoint 模式下运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器与 SharePoint 分别运行在不同服务器上。 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 2013 安装程序包 (**spPowerPivot.msi**) 必须在 SharePoint 服务器上运行。  
  
 ![SSAS 和 SSRS SharePoint 模式 3 服务器部署](../../../2014/sql-server/install/media/as-and-rs-3server-deployment.gif "SSAS 和 SSRS SharePoint 模式 3 服务器部署")  
  
|||  
|-|-|  
|**2**|Excel Service 应用程序。 作为 SharePoint 安装的一部分创建的服务应用程序。|  
|**pps-2**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]服务应用程序。 默认名称为 **“默认的 PowerPivot 服务应用程序”**。|  
|**三维空间**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。|  
|**4**|从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装介质或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能包中安装用于 SharePoint 的 Reporting Services 外接程序。|  
|**5**|运行**sppowerpivot.msi**以安装数据访问接口、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]配置工具、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]库并计划数据刷新。|  
|**共**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]SharePoint 模式下的服务器。 将 Excel Services 应用程序 **“数据模型设置”** 配置为使用此服务器。|  
|**全天候**|SharePoint 内容、配置和服务应用程序数据库。|  
  
 ![SharePoint 设置](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 设置")https://connect.microsoft.com/SQLServer/Feedback)[通过 Microsoft SQL Server Connect （）提交反馈和联系信息](https://connect.microsoft.com/SQLServer/Feedback)。  
  
###  <a name="powerpivot-for-sharepoint-2013-single-server-deployment"></a><a name="bkmk_powerpivot_sharepoint2013_1server"></a>PowerPivot for SharePoint 2013 单一服务器部署  
 单服务器部署用于测试目的，不建议在生产部署中采用。  
  
 以下关系图阐明了属于单服务器 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署的一部分的组件。  
  
 ![PowerPivot for SharePoint 单服务器部署](../../../2014/sql-server/install/media/as-powerpivot-mode-1server-deployment.gif "PowerPivot for SharePoint 单服务器部署")  
  
|||  
|-|-|  
|**2**|Excel Service 应用程序。 作为 SharePoint 安装的一部分创建的服务应用程序。|  
|**pps-2**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]服务应用程序。 默认名称为 **“默认的 PowerPivot 服务应用程序”**。|  
|**三维空间**|SharePoint 内容、配置和服务应用程序数据库。|  
|**4**|SharePoint 模式下的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器。 将 Excel Services 应用程序 **“数据模型设置”** 配置为使用此服务器。|  
  
###  <a name="powerpivot-for-sharepoint-2013-two-server-deployment"></a><a name="bkmk_powerpivot_sharepoint2013_2server"></a>PowerPivot for SharePoint 2013 2 服务器部署  
 在下面的双服务器部署中，SQL Server 数据库引擎和 SharePoint 模式下的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 与 SharePoint 分别运行在不同的服务器上。 对于 SharePoint 2013， [!INCLUDE[ssGeminiLongvnext](../../includes/ssgeminilongvnext-md.md)] 安装程序包 (**spPowerPivot.msi**) 安装在 SharePoint 服务器上。  
  
 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 扩展了 SharePoint Server 2013 的功能，以便为具有高级数据模型的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿和 Excel 工作簿添加服务器端数据刷新处理、数据访问接口、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库以及管理支持。  
  
 该安装程序包作为 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 功能包的一部分提供。 此功能包可以[!INCLUDE[msCoName](../../includes/msconame-md.md)]通过 microsoft [® SQL Server® 2014 PowerPivot® For microsoft® SharePoint®](https://go.microsoft.com/fwlink/?LinkID=296473) （超链接 "<https://go.microsoft.com/fwlink/?LinkID=296473>" \t "_blank" <https://go.microsoft.com/fwlink/?LinkID=296473>）下载。  
  
 ![SSAS PowerPivot 模式 2 服务器部署](../../analysis-services/media/as-powerpivot-mode-2server-deployment.gif "SSAS PowerPivot 模式 2 服务器部署")  
  
|||  
|-|-|  
|**2**|Excel Service 应用程序。 作为 SharePoint 安装的一部分创建的服务应用程序。|  
|**pps-2**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]服务应用程序。 默认名称为 **“默认的 PowerPivot 服务应用程序”**。|  
|**三维空间**|运行**sppowerpivot.msi**以安装数据访问接口、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]配置工具、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]库并计划数据刷新。|  
|**4**|SharePoint 模式下的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器。 将 Excel Services 应用程序 **“数据模型设置”** 配置为使用此服务器。|  
|**5**|SharePoint 内容、配置和服务应用程序数据库。|  
  
###  <a name="powerpivot-for-sharepoint-2013-three-server-deployment"></a><a name="bkmk_powerpivot_sharepoint2013_3server"></a>PowerPivot for SharePoint 2013 3 服务器部署  
 在下面的三服务器部署中，SQL Server 数据库引擎、在 SharePoint 模式下运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器与 SharePoint 分别运行在不同服务器上。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 安装程序包 (spPowerPivot.msi) 必须安装在 SharePoint 服务器上。  
  
 ![AS PowerPivot 模式 3 服务器部署](../../../2014/sql-server/install/media/as-powerpivot-mode-3server-deployment.gif "AS PowerPivot 模式 3 服务器部署")  
  
|||  
|-|-|  
|**2**|Excel Service 应用程序。 作为 SharePoint 安装的一部分创建的服务应用程序。|  
|**pps-2**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]服务应用程序。 默认名称为 **“默认的 PowerPivot 服务应用程序”**。|  
|**三维空间**|运行 spPowerPivot.msi 以安装数据访问接口、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库并计划数据刷新。|  
|**4**|SharePoint 模式下的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器。 将 Excel Services 应用程序 **“数据模型设置”** 配置为使用此服务器。|  
|**5**|SharePoint 内容、配置和服务应用程序数据库。|  
  
###  <a name="powerpivot-for-sharepoint-2013-and-reporting-services-single-server-deployment"></a><a name="bkmk_powerpivot_ssrs_sharepoint2013_1server"></a>PowerPivot for SharePoint 2013 和 Reporting Services 单一服务器部署  
 单服务器部署用于测试目的，不建议在生产部署中采用。  
  
 ![SSAS 和 SSRS SharePoint 模式1服务器部署](../../../2014/sql-server/install/media/as-and-rs-1server-deployment.gif "SSAS 和 SSRS SharePoint 模式1服务器部署")  
  
|||  
|-|-|  
|**2**|Excel Service 应用程序。 作为 SharePoint 安装的一部分创建的服务应用程序。|  
|**pps-2**|PowerPivot 服务应用程序。 默认名称为 **“默认的 PowerPivot 服务应用程序”**。|  
|**三维空间**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。|  
|**4**|从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装介质或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能包中安装用于 SharePoint 的 Reporting Services 外接程序。|  
|**5**|SharePoint 内容、配置和服务应用程序数据库。|  
|**共**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]SharePoint 模式下的服务器。 将 Excel Services 应用程序 **“数据模型设置”** 配置为使用此服务器。|  
  
###  <a name="powerpivot-for-sharepoint-2013-and-reporting-services-two-server-deployment"></a><a name="bkmk_powerpivot_ssrs_sharepoint2013_2server"></a>PowerPivot for SharePoint 2013 和 Reporting Services 两个服务器部署  
 在下面的双服务器部署中，SQL Server 数据库引擎和在 SharePoint 模式下运行的 Analysis Services 服务器与 SharePoint 分别运行在不同的服务器上。 PowerPivot for SharePoint 2013 安装程序包 **（sppowerpivot.msi）** 必须在 SharePoint 服务器上运行。  
  
 ![SSAS 和 SSRS SharePoint 模式 2 服务器部署](../../../2014/sql-server/install/media/as-and-rs-2server-deployment.gif "SSAS 和 SSRS SharePoint 模式 2 服务器部署")  
  
|||  
|-|-|  
|**2**|Excel Service 应用程序。 作为 SharePoint 安装的一部分创建的服务应用程序。|  
|**pps-2**|PowerPivot 服务应用程序。 默认名称为 **“默认的 PowerPivot 服务应用程序”**。|  
|**三维空间**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。|  
|**4**|从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装介质或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能包中安装用于 SharePoint 的 Reporting Services 外接程序。|  
|**5**|运行 **spPowerPivot.msi** 以安装数据访问接口、PowerPivot 配置工具、PowerPivot 库并安排数据刷新。|  
|**共**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]SharePoint 模式下的服务器。 将 Excel Services 应用程序 **“数据模型设置”** 配置为使用此服务器。|  
|**全天候**|SharePoint 内容、配置和服务应用程序数据库。|  
  
##  <a name="sharepoint-2010-example-deployment-topologies"></a><a name="bkmk_example_deployments_2010"></a>SharePoint 2010 示例部署拓扑  
 下图显示了每个层上运行哪些服务和提供程序。 请注意，该图包含了若干内置服务；这些服务是一些 SQL Server BI 方案所必需的。 Excel Services、Secure Store Services 和 Claims to Windows Token Service 为 SharePoint 中的 PowerPivot for SharePoint 或 Reporting Services 部署所必需或建议使用的。 此外，MSOLAP OLE DB 访问接口和 ADO.NET 服务是某些 PowerPivot 数据访问方案所必需的。 如果您要基于 SharePoint 外部承载的表格模型数据库生成 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表，则可以选择在数据层安装 Analysis Services。  
  
 ![逻辑体系结构示意图](../../../2014/sql-server/install/media/sql11bisetup.gif "逻辑体系结构示意图")  
  
##  <a name="single-server-deployments"></a><a name="bkmk_sharepoint2010_1server"></a>单服务器部署  
 您可以在一台计算机上安装所有服务器组件（包括数据层）。 如果您要评估软件或开发自定义应用程序（包含 SharePoint 模式下的 Reporting Services），则此部署配置会很有用。 这种部署最易于配置。 因为所有组件都安装在同一台计算机上，所以该部署使用的许可证也最少。 、 和可作为  的一个许可副本进行安装。  
  
 若要在一台服务器上安装所有功能，请依次在同一物理服务器上安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 。 有关独立服务器配置的说明，请参阅[部署清单： Reporting Services、Power View 和 PowerPivot for SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)。  
  
##  <a name="two-tier-deployment"></a><a name="bkmk_sharepoint2010_2server"></a>双层部署  
 两层部署通常是指在一台计算机上安装 SharePoint Server 2010，而在第二台计算机上安装 SQL Server 数据库引擎。 将数据层移到专用服务器是由 2 台计算机组成的场的最常见配置。 在两层场中，您可以在 SharePoint 服务器上安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 。 前端上的所有 Web 服务和应用程序层中的共享服务均在同一物理服务器上运行。 2 层部署的安装步骤与独立部署非常类似，都是在同一物理服务器上依次安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 。  
  
##  <a name="three-tier-deployment"></a><a name="bkmk_sharepoint2010_3server"></a>三层部署  
 通常，三层部署会将 Web 前端服务从处理功能或占用大量内存的应用程序中分离出来。 在此拓扑中，您只在应用程序服务器上安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 。 运行于 Web 前端的 Web 服务将作为安装后任务，在服务器配置期间通过部署到场中应用程序的解决方案进行安装。 下图说明了 3 层部署。  
  
 ![3-服务器拓扑](../../../2014/sql-server/install/media/sql11bisetup-3server.gif "3-服务器拓扑")  
  
##  <a name="three-tier-scale-out-deployment"></a><a name="bkmk_sharepoint2010_scaleserver"></a>三层扩展部署  
 此拓扑说明了在多台服务器上运行同一共享服务的扩展部署，该部署为大量请求提供服务并为 PowerPivot 数据或 Reporting Services 报表提供更强大的处理能力。 下图中有三种应用程序服务器群集，每一种均运行不同组合的共享服务。 在 SharePoint 环境中，已将服务发现和可用性内置于场中。 运行同一共享服务应用程序的多台物理服务器之间的负载平衡是共享服务体系结构的一部分。  
  
 部署多服务器场时，请务必按照以下 SharePoint 文章中的说明执行操作： [三层服务器场的多个服务器 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834)。  
  
 ![5 服务器拓扑](../../../2014/sql-server/install/media/sql11bisetup-5server.gif "5 服务器拓扑")  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services sharepoint 模式安装 &#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [PowerPivot for SharePoint 2013 安装](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)   
 [PowerPivot for SharePoint 2010 安装](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
