---
title: 针对 SQL Server 2014 自助商业智能的示例许可证拓扑和成本 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 682b8711-407a-48d1-9807-415d4c24dad6
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4672647d8e9caae94e3b64fc43c3b687aa010920
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185791"
---
# <a name="example-license-topologies-and-costs--for-sql-server-2014-self-service-business-intelligence"></a>针对 SQL Server 2014 自助商业智能的许可证拓扑和成本示例
  本主题说明了选择的高级注意事项[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]商业智能版或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]企业版。 本主题包括若干本地 Microsoft 自助商业智能 (BI) 拓扑示例。 这些示例包括可用来在成本和性能之间取得最佳平衡的版本和许可证。 拓扑、服务器数目和许可成本 **仅作为示例**提供。 Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 Microsoft SharePoint 2013 在许可中引入了若干更改，为您许可服务器、用户和设备提供了更多方式选择。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 许可支持与商业智能相关的相同方案。  
  
-   在商业智能版中提供了 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，并且为某些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供按内核许可。  
  
-   SharePoint 2013 简化了针对 Extranet 和 Internet 方案的 SharePoint Server 许可以及用于 SharePoint Online 的选项。  
  
 在购买前，请访问每种产品的“如何购买”部分，就您的特定许可要求可向您的 Microsoft 代表或本地经销商咨询。 有关最新许可计划和成本的信息，请参阅以下内容：  
  
-   [关于许可 – SQL Server 2014](http://www.microsoft.com/licensing/about-licensing/sql2014.aspx)  
  
-   [SharePoint 2013 许可](http://office.microsoft.com/sharepoint/sharepoint-licensing-overview-collaboration-software-FX103789438.aspx)。  
  
 **本主题内容：**  
  
-   [SQL Server 商业智能组件](#bkmk_bi_components)  
  
-   [SQL Server 2014 许可摘要](#bkmk_sql_server_license)  
  
-   [SharePoint 2013 许可摘要](#bkmk_sharepoint_license)  
  
-   [与单独的 PowerPivot 服务器的 3 层拓扑](#bkmk_3tier_powerpivot)  
  
-   [3 层拓扑](#bkmk_3tier)  
  
-   [2 层拓扑](#bkmk_2tier)  
  
-   [引用和社区内容](#bkmk_reference)  
  
##  <a name="bkmk_bi_components"></a> SQL Server 商业智能组件  
 本主题着重说明 SQL Server 和 SharePoint 服务器技术。 成本和示例并非专门说明您为完整客户端和服务器解决方案所要求的 Microsoft Windows Server 或 Microsoft Office 组件。 在本主题中涵盖的 SQL Server 商业智能组件是在 SharePoint 模式下运行的 SQL Server Reporting Services 和 PowerPivot for SharePoint。 这些组件包括以下功能：  
  
-   浏览器中的交互式 PowerPivot 工作簿。  
  
-   交互式[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]SharePoint 中的报表。  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库、计划数据刷新、管理面板。  
  
-   SharePoint 模式下的 Reporting Services，包括数据警报。  
  
 有关详细信息，请参阅中的功能表[安装 SQL Server BI 功能以及 SharePoint &#40;PowerPivot 和 Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)。  
  
## <a name="license-summary"></a>许可摘要  
 本节概要说明针对 SQL Server 和 SharePoint 的许可要求。 本节中的信息是概括性摘要，仅涵盖在拓扑关系图中使用的方案以及本文档中的成本示例。 有关更详细的许可细节，请参考所示的内容链接。 示例价格基于 Microsoft 公开许可计划 (MOLP) 价格。  
  
 通常，将 **Enterprise Edition** 用于运行 SQL Server 数据库引擎的服务器，将 **商业智能版** 用于运行 Reporting Services 或 PowerPivot for SharePoint 的服务器。 但是，您的部署中的 **用户数** 和 **服务器内核数** 将会影响成本以及对要使用的版本的决策。  
  
###  <a name="bkmk_sql_server_license"></a> SQL Server 2014 许可摘要  
  
-   SQL Server Enterprise Edition 使用基于内核的许可。 基于内核的许可在 **两内核** 包装中销售。  
  
-   SQL Server BI 版本使用服务器许可和客户端访问许可 (CAL)。  
  
-   CAL 许可基于连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每个用户或设备，与它们连接到的服务器数目无关。  
  
-   内核许可要求服务器中的所有内核都受到某一许可证的涵盖。 对于服务器中的每个物理处理器，需要最少 **四个** 内核许可证。  
  
 下表总结了用于部署设计和许可成本评估的许可详细信息。 **注意：**  所示价格仅供演示。  
  
|SQL Server 版本|SQL Server 许可 + 客户端访问许可 (CAL)|SQL Server 基于内核的许可|  
|-------------------------|---------------------------------------------------------|-----------------------------------|  
|Enterprise|不适用|**（是）** $6874 X [内核数] X [内核系数]|  
|Business Intelligence|**（是）** $8592 + 每个 CAL $199|不适用|  
|Standard|**（是）**|**（是）**|  
  
 有关详细信息示例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]许可价格，请参阅：  
  
-   [虚拟环境的许可](http://www.microsoft.com/licensing/about-licensing/virtualization.aspx)(http://www.microsoft.com/licensing/about-licensing/virtualization.aspx)。  
  
-   [SQL Server 2014 许可数据表-Microsoft 主页](http://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf)(http://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf)。  
  
-   [SQL server 2014 版本和许可](http://www.microsoft.com/licensing/about-licensing/sql2014.aspx#tab=2)  
  
1.  **SQL Server 假设和更多许可信息：**  
  
2.  本主题中的关系图使用 SQL Server 的 Enterprise Edition 用于数据库服务器，以便提供全套高可用性功能，例如 AlwaysOn 可用性组。 有关详细信息，请参阅 [Features Supported by the Editions of SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
3.  此示例中的服务器均为 2 个 Intel Xeon 6 核处理器，因此，在计算许可成本时， **SQL Server 内核系数** 为 **1** 。 有关内核系数和许可成本的详细信息，请参阅[SQL Server 内核系数表](http://download.microsoft.com/download/9/B/F/9BF63163-D8F9-4339-90AA-EBC9AAFC49AD/SQL2012_CoreFactorTable_Mar2012.pdf)(http://download.microsoft.com/download/0/C/8/0C85665B-11EA-4FF5-B37C-8CC21CF95AC4/BizTalk%202013_CoreFactorTable_**3.19.2013**。 v4.pdf)。  
  
###  <a name="bkmk_sharepoint_license"></a> SharePoint 2013 许可摘要  
 下面的列表总结了用于部署设计和许可成本评估的许可模型。 所示价格仅供演示。  
  
1.  SharePoint 服务器许可是每个 Microsoft SharePoint Server 实例所必需的。  
  
2.  若要向 SharePoint Enterprise 授予许可，对于每个最终用户或最终设备，请购买 Microsoft SharePoint Server 2013 **标准 CAL 许可证** 以及 Microsoft SharePoint Server 2013 **企业 CAL 许可证**。  
  
3.  为访问 SharePoint 服务器的每个用户或设备购买一个 SharePoint CAL 许可证。 您无需为每个服务器都购买 CAL 许可证。  
  
 例如，如果您的环境由供 100 个用户使用的 2 个实例构成，并且您的成本构成如下：  
  
-   Microsoft SharePoint Server 2013 Standard CAL license: <bpt id="p1">**</bpt>$107.99<ept id="p1">**</ept>  
  
-   Microsoft SharePoint Server 2013 Enterprise CAL license: <bpt id="p1">**</bpt>$94.99<ept id="p1">**</ept>  
  
-   Microsoft SharePoint Server 2013 license: <bpt id="p1">**</bpt>$6,412.99<ept id="p1">**</ept>  
  
 The cost would be: <bpt id="p1">**</bpt>$33,123.98<ept id="p1">**</ept>  
  
-   CAL 许可证：($107.99 +$94.99) X 100 =$20,298.00  
  
-   服务器许可证：($6,412.99 X 2) =$12,825.98  
  
 **SharePoint 假设和更多许可信息：**  
  
 这些示例部署全都是 Intranet 环境，因此需要 SharePoint CAL 许可。  
  
-   [SharePoint 完整许可列表](http://technet.microsoft.com/en-in/library/jj819267.aspx#bkmk_FeaturesOnPremise)(http://technet.microsoft.com/en-in/library/jj819267.aspx#bkmk_FeaturesOnPremise)。  
  
-   [如何购买 SharePoint](http://sharepoint.microsoft.com/en-in/Pages/buy.aspx) (http://sharepoint.microsoft.com/en-in/Pages/buy.aspx)。  
  
##  <a name="bkmk_3tier_powerpivot"></a> 3 层使用单独的拓扑[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]服务器  
 此示例说明，对于 800 个或更少用户，将 SQL Server BI 版本用于 SharePoint 应用程序服务器和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 服务器的开销最少。 但在由 800 个或更多的用户时，SQL Server Enterprise Edition 的开销较低。 内核许可与用户数目无关，因此，在您对内核和 CAL 许可成本进行比较以及用户数目增加时，存在成本阈值点。 从该成本阈值点往上，Enterprise Edition 是开销最低的解决方案。 为了确定成本阈值，将基于要许可的内核数目的成本与要许可的最终用户或最终设备 CAL 的数目进行比较。  
  
-   此示例是一个 Intranet 部署；因此，SharePoint CAL 许可适用于 SharePoint 2013。  
  
-   应用程序角色 (2) 包括在 SharePoint 模式下安装的 SQL Server Reporting Services。  
  
     SharePoint 服务应用程序数据库运行在数据库角色 (4) 服务器上。  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 运行在单独的服务器 (3) 上。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 运行在 SharePoint 场之外，可以在不包含 SharePoint 安装，从而提高性能的服务器上安装。  
  
-   数据库角色 (4) 使用 SQL Server Enterprise，以便提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能 AlwaysOn 可用性组。  
  
 ![bi_license_3tiers_and_ASseparate](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseparate.gif "bi_license_3tiers_and_ASseparate")  
  
 对于 100 个用户，SQL Server BI 版本的开销较低。  
  
 ![bi_license_3tiers_and_ASseperate_calcs](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseperate-calcs.gif "bi_license_3tiers_and_ASseperate_calcs")  
  
 但对于 300 个用户，使用 SQL Server Enterprise Edition 的开销较低。  
  
 ![bi_license_3tiers_and_ASseperate_calcs2](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseperate-calcs2.gif "bi_license_3tiers_and_ASseperate_calcs2")  
  
##  <a name="bkmk_3tier"></a> 3 层拓扑  
 此示例说明了对于 100 个或更少的用户，将 SQL BI 版本用于运行 SQL Server BI 功能的服务器的成本较低。 但在有 500 个或更多的用户时，SQL Server Enterprise Edition 的开销较低。  
  
-   此示例是一个 Intranet 部署；因此，SharePoint CAL 许可适用于 SharePoint 2013。  
  
-   Analysis Services 在 PowerPivot 模式 (2) 场外运行，但 PowerPivot 正运行**上的相同物理**中其他应用程序角色的服务器。  
  
-   数据库角色 (3) 使用 SQL Server Enterprise，以便[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能 AlwaysOn 可用性组不可用。  
  
 ![bi_license_3tiers](../../../2014/sql-server/install/media/bi-license-3tiers.gif "bi_license_3tiers")  
  
 对于 100 个用户，SQL Server BI 版本的开销较低。  
  
 ![bi_license_3tiers_calcs1](../../../2014/sql-server/install/media/bi-license-3tiers-calcs1.gif "bi_license_3tiers_calcs1")  
  
 但对于 500 个用户，SQL Server Enterprise Edition 的开销较低。  
  
 ![bi_license_3tiers_calcs3](../../../2014/sql-server/install/media/bi-license-3tiers-calcs3.gif "bi_license_3tiers_calcs3")  
  
##  <a name="bkmk_2tier"></a> 2 层拓扑  
 对于仅 2 层拓扑，使用 SQL Server Enterprise Edition，以便 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能 AlwaysOn 可用性组可用于 SQL Server 数据库引擎。 因此，在 SQL Server 的各版本之间进行比较时没有成本上的差异。 唯一变化是 SharePoint CAL 价格基于用户的数目。  
  
-   此示例是一个 Intranet 部署；因此，SharePoint CAL 许可适用于 SharePoint 2013。  
  
-   PowerPivot 模式下的 Analysis Services 在场外运行，但 PowerPivot 正在与 SQL Server 数据库引擎运行在相同物理服务器 (2) 上。  
  
 ![bi_license_2tiers](../../../2014/sql-server/install/media/bi-license-2tiers.gif "bi_license_2tiers")  
  
 ![bi_license_2tiers_calcs1](../../../2014/sql-server/install/media/bi-license-2tiers-calcs1.gif "bi_license_2tiers_calcs1")  
  
##  <a name="bkmk_reference"></a> 引用和社区内容  
  
### <a name="license-tools"></a>许可工具  
  
-   [Microsoft 许可证顾问](http://mla.microsoft.com/default.aspx)(http://mla.microsoft.com/default.aspx)。  
  
-   [客户端访问许可证 (CAL) 决策工具](http://www.microsoft.com/licensing/CalTool/)(http://www.microsoft.com/licensing/CalTool/)。  
  
-   [Microsoft 业务中心： 如何购买](http://www.microsoftbusinesshub.com/How_To_Buy#)(http://www.microsoftbusinesshub.com/How_To_Buy#)。  
  
### <a name="microsoft-license-information"></a>Microsoft 许可信息  
  
-   [关于许可： 客户端访问许可证和管理许可证](http://www.microsoft.com/licensing/about-licensing/client-access-license.aspx)(http://www.microsoft.com/licensing/about-licensing/client-access-license.aspx)。  
  
-   [关于许可： 产品许可搜索](http://www.microsoftvolumelicensing.com/default.aspx)(http://www.microsoftvolumelicensing.com/default.aspx)。  
  
-   [批量许可： 定价和购买方式](http://www.microsoft.com/licensing/how-to-buy/how-to-buy.aspx)(http://www.microsoft.com/licensing/how-to-buy/how-to-buy.aspx)。  
  
### <a name="community-content"></a>社区内容  
  
-   [SQL Server 2014 Developer Edition 许可](http://sqlmag.com/sql-server-2014/sql-server-2014-developer-edition-licensing)。  
  
-   [SQL Server 2014 许可变更](http://www.brentozar.com/archive/2014/04/sql-server-2014-licensing-changes)(http://www.brentozar.com/archive/2014/04/sql-server-2014-licensing-changes)。  
  
-   [SQL server 2014 许可变更](https://www.directionsonmicrosoft.com/sites/default/files/PDFs/Licensing_Changes_for_SQL_Server_2014.pdf)(https://www.directionsonmicrosoft.com/sites/default/files/PDFs/Licensing_Changes_for_SQL_Server_2014.pdf)。  
  
-   [SharePoint 2013 许可成本估算](http://www.degdigital.com/blog/sharepoint-2013-licensing-for-dummies/)(http://www.degdigital.com/blog/sharepoint-2013-licensing-for-dummies/)。  
  
-   [Microsoft 批量许可客户社区](http://www.microsoft.com/licensing/existing-customers/community.aspx)(http://www.microsoft.com/licensing/existing-customers/community.aspx)。  
  
  
