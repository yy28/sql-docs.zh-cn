---
title: PowerPivot for SharePoint （SSAS） |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c4c393d3-4856-47ac-ab5f-15da2f240d1d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 34a4cc6b16e22a20e0e8be3ded12b0465ba46eab
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84535119"
---
# <a name="powerpivot-for-sharepoint-ssas"></a>PowerPivot for SharePoint (SSAS)
  PowerPivot for SharePoint 是一个在 SharePoint 模式下运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器。 PowerPivot for SharePoint 对 SharePoint 场中的 PowerPivot 数据提供服务器托管。 PowerPivot 数据是使用以下项之一生成的分析数据模型：  
  
-   PowerPivot for Excel 2010 外接程序  
  
-   Excel 2013  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]2013 |[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]2010  
  
 这些数据的服务器托管要求安装 SharePoint、Excel Services 和 PowerPivot for SharePoint。 数据加载到 PowerPivot for SharePoint 实例上，从中，可以使用服务器为 Excel 2010 工作簿或 SharePoint 2013 Excel Services 为 Excel 2013 工具簿提供的 PowerPivot 数据刷新功能定期刷新数据。  
  
## <a name="powerpivot-for-sharepoint-2013"></a>PowerPivot for SharePoint 2013  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]支持 [!INCLUDE[msCoName](../../includes/msconame-md.md)]SharePoint 2013 Excel Services 使用包含数据模型和 Power View 报表的 Excel 工作簿 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。  
  
 SharePoint 2013 中的 Excel Services 包括数据模型功能，以便在浏览器中实现与 PowerPivot 工作簿的交互。 您无需将 PowerPivot for SharePoint 2013 外接程序部署到场中。 您只需在 SharePoint 模式下安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器，并且在 Excel Services 的 **“数据模型”** 设置中注册该服务器。  
  
 通过部署 PowerPivot for SharePoint 2013 外接程序，您可以在 SharePoint 场中实现附加功能。 这些附加功能包括 PowerPivot 库、计划数据刷新和 PowerPivot 管理面板。  
  
 ![SSAS PowerPivot 模式 2 服务器部署](../media/as-powerpivot-mode-2server-deployment.gif "SSAS PowerPivot 模式 2 服务器部署")  
  
## <a name="powerpivot-for-sharepoint-2010"></a>PowerPivot for SharePoint 2010  
 PowerPivot for SharePoint 2010 对 SharePoint 2010 场中的 PowerPivot 数据提供服务器托管。 PowerPivot 数据是使用 PowerPivot for Excel 外接程序在 Excel 中生成的一种分析数据模型。 这些数据的服务器托管要求安装 SharePoint 2010、Excel Services 和 PowerPivot for SharePoint。 数据加载到场中的 PowerPivot for SharePoint 实例上，从中，可以使用服务器提供的 PowerPivot 数据刷新功能定期刷新数据。  
  
### <a name="components-of-powerpivot-for-sharepoint-2010"></a>PowerPivot for SharePoint 2010 的组件  
 PowerPivot for SharePoint 作为共享服务实现，这意味着可以使用内置功能和基础结构来管理、保护和使用 PowerPivot 服务应用程序。 服务器和数据库发现、重定向和连接管理全都在场级别管理。 管理中心提供服务用来管理服务器标识、服务器状态和配置属性的管理界面。  
  
 完整部署 PowerPivot for SharePoint 包括将 Excel 和 Excel Services 在 SharePoint 场中进行集成的客户端和服务器组件。 Excel 工作簿内的 PowerPivot 数据是一种 Analysis Services 数据库，它要求 Analysis Services xVelocity 内存中分析引擎 (VertiPaq) 加载和查询数据。 在客户端工作站上，xVelocity 引擎在 Excel 内部在进程内运行。 在 SharePoint 场上，Analysis Services 在应用程序服务器上运行，它与相关服务配合使用以处理 PowerPivot 数据请求。 下面的关系图说明了 PowerPivot 客户端和服务器组件：  
  
 ![GMNI_GeminiArch2](../media/gmni-geminiarch2.gif "GMNI_GeminiArch2")  
  
 PowerPivot Web 服务在 Web 应用程序服务器上运行。 它将来自 Web 应用程序的请求重定向到场中的 PowerPivot 系统服务实例上。  
  
 PowerPivot 系统服务对 Analysis Services 服务器发出加载请求，管理已加载到内存中的数据的正在进行的连接，并且在数据不再使用或者出现系统资源争用时缓存或卸载数据。 它还跟踪用户活动。 收集服务器运行状况数据和其他使用情况数据并显示在报表中，以便指出系统的运行状况如何。  
  
 SharePoint 集成模式下的 Analysis Service 服务器实例完成该部署。 它加载、查询和卸载数据。 如果工作簿配置用于 PowerPivot 数据刷新，它还可以处理数据。  每个实例都与属于同一安装的本地 PowerPivot 系统服务紧密结合。  
  
##  <a name="in-this-section"></a><a name="bkmk_RelatedContent"></a> 本节内容  
 [在管理中心中管理和配置 PowerPivot 服务器](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [使用 Windows PowerShell 配置 PowerPivot](power-pivot-configuration-using-windows-powershell.md)  
  
 [PowerPivot Configuration Tools](power-pivot-configuration-tools.md)  
  
 [PowerPivot 身份验证和授权](power-pivot-authentication-and-authorization.md)  
  
 [PowerPivot 运行状况规则 - 配置](configure-power-pivot-health-rules.md)  
  
 [PowerPivot 管理面板和使用情况数据](power-pivot-management-dashboard-and-usage-data.md)  
  
 [PowerPivot 库](../../2014-toc/index.yml)  
  
 [PowerPivot 数据访问](power-pivot-data-access.md)  
  
 [PowerPivot 数据刷新](power-pivot-data-refresh.md)  
  
 [PowerPivot 数据馈送](power-pivot-data-feeds.md)  
  
 [PowerPivot BI 语义模型连接 &#40; bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)  
  
 **其他部分**  
  
## <a name="additional-topics"></a>其他主题  
 [升级 PowerPivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)  
  
 [PowerPivot for SharePoint 2013 安装](../instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
 [针对 PowerPivot for SharePoint 的 PowerShell 参考](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
 [SQL Server 2014 自助商业智能的许可证拓扑和成本示例](../../sql-server/install/example-license-topologies-costs-self-service-business-intelligence.md)  
  
## <a name="see-also"></a>另请参阅  
 [PowerPivot 规划和部署](https://go.microsoft.com/fwlink/?linkID=220972)   
 [Disaster Recovery for PowerPivot for SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
