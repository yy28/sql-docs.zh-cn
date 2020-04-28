---
title: 通过 SharePoint 安装 SQL Server BI 功能（PowerPivot 和 Reporting Services） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3166107c-30c2-468e-bb1b-bb42b79b37c3
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: cd1dae56cf2ea571ca9ab16de178764b807260db
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388089"
---
# <a name="install-sql-server-bi-features-with-sharepoint-powerpivot-and-reporting-services"></a>使用 SharePoint 安装 SQL Server BI 功能（PowerPivot 和 Reporting Services）
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可与 Microsoft SharePoint 场相集成，以便实现 SharePoint 中的商业智能 (BI) 功能。 这些功能包括 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]、 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 用于 SharePoint 场中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据访问。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 是用于在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 中创建的工作簿以及从 SharePoint 库访问的工作簿的数据引擎。 在您将某一 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿保存到 SharePoint 后，就可以将该工作簿用作 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表的数据源。

 SharePoint 2010 所需的某些安装和配置步骤与 SharePoint 2013 所需步骤不同。 本节中的某些主题适用于这两个版本的 SharePoint。

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|

 ![注意](../../../2014/reporting-services/media/rs-fyinote.png "注意")有关最新的发行说明，请参阅[SQL server 2014 发行说明](https://go.microsoft.com/fwlink/?LinkID=296445)。

##  <a name="in-this-topic"></a><a name="bkmk_top"></a>本主题中的

-   [SQL Server BI 方案和 SharePoint 2013](#bkmk_bi_scenarios)

-   [安装概述](#bkmk_install_sharepoint2013_overview)

## <a name="in-this-section"></a>本节内容
 除了本主题中的信息外，本节内容还包括以下相关主题。

 [SharePoint 中 SQL Server BI 功能的部署拓扑](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)

 [在 SharePoint 2010 场中使用 SQL Server BI 功能的指南](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)

 [将 BI 功能随 SharePoint 一起安装的核对清单](../../../2014/sql-server/install/checklists-for-installing-bi-features-with-sharepoint.md)

 [Reporting Services sharepoint 模式安装 &#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)

 [PowerPivot for SharePoint 2013 安装](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)

 [PowerPivot for SharePoint 2010 安装](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)

##  <a name="sql-server-bi-scenarios-and-sharepoint-2013"></a><a name="bkmk_bi_scenarios"></a>SQL Server BI 方案和 SharePoint 2013
 本部分概述了您可以选择安装和配置的不同级别的 BI 功能。

 SharePoint 2013 中的 Excel Services 包括数据模型功能，用于在浏览器中实现与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿的交互。 对于基本数据模型功能，您无需将 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 外接程序部署到场中。 您只需在 SharePoint 模式下安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器，并且在 Excel Services 的 **“数据模型”** 设置中注册该服务器。

 通过部署 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 外接程序，可以在 SharePoint 场中实现附加功能。 这些附加功能包括 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库、计划数据刷新和 PowerPivot 管理面板。 有关其他信息，请参阅表。

||级别|功能|安装或配置|
|-|-----------|--------------|--------------------------|
|1|仅限 SharePoint|本机 Excel Services 功能|SharePoint Server 2013 随附的 Excel Services 和其他服务。|
|**2**|SharePoint 以及 SharePoint 模式下的 Analysis Services|浏览器中的交互式 PowerPivot 工作簿|在 SharePoint 模式下安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。<br /><br /> 在 Excel Services 中注册 Analysis Services 服务器。|
|**3**|SharePoint 以及 SharePoint 模式下的 Reporting Services|Power View|在 SharePoint 模式下安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。<br /><br /> 安装[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]适用于 SharePoint 的外接程序 **（rssharepoint.msi）** 。 有关详细信息，请参阅[安装或卸载用于 sharepoint 的 Reporting Services 外接程序 &#40;sharepoint 2010 和 sharepoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)|
|**4**|所有 PowerPivot 功能|从场外作为数据源访问工作簿。<br /><br /> 计划数据刷新。<br /><br /> PowerPivot 库。<br /><br /> 管理面板。<br /><br /> BISM 链接文件内容类型。|部署 PowerPivot for SharePoint 2013 外接程序 **（sppowerpivot.msi）**。 有关详细信息，请参阅以下主题：<br /><br /> [在 SharePoint 2013 &#40;安装或卸载 PowerPivot for SharePoint 加载项&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)<br /><br /> 有关如何下载 **spPowerPivot.msi**的信息，请参阅 [下载 SQL Server 2014 PowerPivot for SharePoint](https://go.microsoft.com/fwlink/?LinkID=296473)。|

 有关启用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]功能的其他信息，请参阅[适用于 SharePoint 2013 的 SQL Server BI 细小故事](https://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx)（。https://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx)

##  <a name="overview-of-installation"></a><a name="bkmk_install_sharepoint2013_overview"></a>安装概述
 如果要同时使用 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，请运行 SQL Server 安装向导两次。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]是 SQL Server 安装向导的 "**设置角色**" 页上的单独选项。

 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 支持 SharePoint 2010 和 SharePoint 2013；但根据 SharePoint 的版本，会使用不同的体系结构和安装过程。

 下面是用于在单个服务器上部署 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 商业智能功能的安装步骤的摘要：

 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]2013**

 对于 **SharePoint 2013**， [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安装可在未安装 SharePoint 产品的服务器上运行。 用于 SharePoint 2013 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 体系结构在 SharePoint 场 **外** 运行，可以安装在也包含 SharePoint 安装的服务器上，或者安装在不包含 SharePoint 安装的服务器上。

1.  安装 SharePoint Server 2013 并启用 Excel Services。

2.  在 SharePoint 模式下安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，并在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中向 SharePoint 场和服务帐户授予服务器管理员权限。

     对于这两个版本的 SharePoint，可通过在 SQL Server 安装向导中选择 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] “SQL Server PowerPivot for SharePoint” **安装角色或使用 SQL Server 命令提示符安装，开始** 安装过程。

     ![设置角色](../../../2014/sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "安装角色")

3.  对于 SharePoint 2013，可以扩展 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能和体验。 下载并运行 **spPowerPivot.msi** 以添加针对 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿的服务器端数据刷新处理、协作和管理支持。 有关详细信息，请参阅 [Microsoft SQL Server 2014 PowerPivot for Microsoft® SharePoint](https://go.microsoft.com/fwlink/?LinkID=324854)。

     在 SharePoint 场中的每台服务器上运行 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 安装包 **spPowerPivot.msi** ，以确保安装正确版本的数据访问接口。

4.  若要配置 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013，请使用 **PowerPivot for SharePoint 2013 配置** 工具。

     SQL Server 安装向导会安装两个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具。 其中一个配置工具支持 SharePoint 2013，另一个工具支持 SharePoint 2010。

     ![两个 PowerPivot 配置工具](../../analysis-services/media/as-powerpivot-configtools-bothicons.gif "两个 PowerPivot 配置工具")

5.  在 SharePoint Server 2013 中配置 Excel Services 以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。 有关详细信息，请参阅[PowerPivot for SharePoint 2013 安装](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)中的 "配置基本 Analysis Services SharePoint 集成" 一节。和[管理 Excel Services 数据模型设置（SharePoint Server 2013）](https://technet.microsoft.com/library/jj219780.aspx) （https://technet.microsoft.com/library/jj219780.aspx)。

6.  有关详细信息，请参阅 [PowerPivot for SharePoint 2013 Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)。

 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]2010**

 对于 SharePoint 2010， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安装需要在已安装或将要安装 SharePoint 2010 的服务器上运行。 用于 SharePoint 2010 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 体系结构在场 **内** 运行，并且在安装了 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的服务器上需要有 SharePoint。

1.  在 SharePoint 模式下安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，并在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中向 SharePoint 场和服务帐户授予服务器管理员权限。

     SharePoint 2010 部署不支持 spPowerPivot.msi，并且该 .msi **不是** SharePoint 2010 所必需的。

     对于这两个版本的 SharePoint，可通过在 SQL Server 安装向导中选择 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] “SQL Server PowerPivot for SharePoint” **安装角色或使用 SQL Server 命令提示符安装，开始** 安装过程。

2.  SQL Server 安装向导会安装两个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具。 其中一个配置工具支持 SharePoint 2013，另一个工具支持 SharePoint 2010。

     若要为 SharePoint 2010 配置 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ，请使用 **PowerPivot 配置工具** 。

3.  有关详细信息，请参阅 [PowerPivot for SharePoint 2010 Installation](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)。

 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]** for SharePoint 2010 和2013

1.  在 SharePoint 模式下针对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的安装与以前版本相比没有变化。

     针对 SharePoint 2010 和 SharePoint 2013 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装步骤非常相似。 下面是有关 SharePoint 版本的重要说明：

    -   请参见以下支持的组合：

        -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的版本。

        -   用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序。

        -   SharePoint 产品的版本。

         [支持的 SharePoint 和 Reporting Services Server 和外接程序的组合 &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)

    -   SharePoint 2010 上的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 要求 SharePoint 2010 Service Pack 2 (SP2)。

    1.  在 SharePoint 模式下安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 [Reporting Services Sharepoint 模式安装 &#40;sharepoint 2010 和 sharepoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)并[安装 Reporting Services SharePoint mode for sharepoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)。

    2.  安装用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序 (rsSharePoint.msi)。 请参阅[安装或卸载用于 sharepoint &#40;sharepoint 2010 和 sharepoint 2013&#41;Reporting Services 外接程序](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。 有关用于 SharePoint 的[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]外接程序的当前版本，请参阅[在何处查找用于 sharepoint 产品的 Reporting Services 外接程序](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。

    3.  配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 服务和至少一个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。 有关详细信息，请参阅[安装 sharepoint 2013 Reporting Services Sharepoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)中的 "创建 Reporting Services 服务应用程序" 部分。

##  <a name="overview-of-database-attach-upgrade-and-sharepoint-2013"></a><a name="bkm_database_attach"></a>数据库附加升级和 SharePoint 2013 概述
 SharePoint 2013 不支持就地升级。 但是 **支持数据库附加升级**。

 如果您具有与 SharePoint 2010 相集成的现有 PowerPivot 安装，则不能就地升级 SharePoint 服务器。  但是，您可以作为 SharePoint 数据库附加升级的一部分完成以下步骤：

1.  安装新的 SharePoint Server 2013 场。

2.  完成 SharePoint 数据库附加升级，并且将您的 PowerPivot 相关内容数据库迁移到 SharePoint 2013 场。

3.  在 SharePoint 模式下安装 SQL Server Analysis Services 实例，并且在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中向 SharePoint 场和服务帐户授予服务器管理员权限。

4.  在 SharePoint 场中的每个服务器上都安装 PowerPivot for SharePoint 2013 安装包 **spPowerPivot.msi** 。

5.  在 SharePoint 2013 管理中心中，对 Excel Services 进行配置，以便使用在步骤 3 中创建的在 SharePoint 模式下运行的 Analysis Services 服务器。

     若要迁移刷新计划，请配置 PowerPivot 服务应用程序。

> [!NOTE]
>  有关 PowerPivot 和 SharePoint 数据库附加升级的详细信息，请参阅下列文章：

-   [将 PowerPivot 迁移到 SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013)

-   [升级到 SharePoint 2013 的过程概述](https://go.microsoft.com/fwlink/p/?LinkId=256688)。

-   [升级到 SharePoint 2013 之前的清除准备](https://go.microsoft.com/fwlink/p/?LinkId=256689)。

-   [将数据库从 SharePoint 2010 升级到 SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690)。

## <a name="see-also"></a>另请参阅
 [在何处查找用于 Sharepoint 产品的 Reporting Services 外接程序](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)[支持的 Sharepoint 和 Reporting Services 服务器和外接程序的组合 &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md) [安装或卸载用于 SharePoint Reporting Services sharepoint 2010 和 sharepoint 2013 &#40;的外接程序&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)


