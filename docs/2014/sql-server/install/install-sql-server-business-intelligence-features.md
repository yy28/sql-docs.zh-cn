---
title: 安装 SQL Server 2014 BI 功能
ms.custom: ''
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.date: 10/24/2018
ms.technology: install
ms.openlocfilehash: 44805d6fd7512a5180a2b62e2c8808b890901705
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151651"
---
# <a name="install-sql-server-2014-bi-features"></a>安装 SQL Server 2014 BI 功能

  SQL Server 功能是 Microsoft Business Intelligence 平台的一部分，其中包括： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]以及用于创建或使用分析数据的若干客户端应用程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装文档中的本部分说明如何安装这些功能。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可在扩展配置中作为独立服务器安装，或者在 SharePoint 场中作为共享服务应用程序安装。 在场中安装这些服务会启用仅在 SharePoint 中可用的 BI 功能，其中包括 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 和 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]，后者是在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 表格模型数据库中运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 即席交互报表设计器。  
  
 如果您已经对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 PowerPivot for SharePoint 的安装步骤比较熟悉，则可以跳过一些步骤，直接转到指导如何启用特定方案的核对清单。 有关详细信息，请参阅[用于使用 SharePoint 安装 BI 功能的核对清单](checklists-for-installing-bi-features-with-sharepoint.md)。  
  
## <a name="contents"></a>目录

本节内容：
  
|链接|任务|  
|----------|----------|  
|[将 BI 功能随 SharePoint 一起安装的核对清单](checklists-for-installing-bi-features-with-sharepoint.md)|如果您已知道要安装的项并且对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的安装步骤比较熟悉，则可以使用本部分中的核对清单，该清单将对安装顺序、帐户和权限要求以及部署高级拓扑（包括多服务器和多功能部署）的步骤进行指导。|  
|[使用 SharePoint 安装 SQL Server BI 功能&#40;PowerPivot 和 Reporting Services&#41;](install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)|本节介绍如何在 SharePoint 环境中安装 SQL Server 功能。 它标识对于特定版本的 SharePoint，提供了哪些 SQL Server 功能。 本节还包含在 SharePoint 模式下安装 PowerPivot for SharePoint 和 Reporting Services 的过程。|  
|[在多维和数据挖掘模式下安装 Analysis Services](install-analysis-services-in-multidimensional-and-data-mining-mode.md)<br /><br /> [在表格模式下安装 Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)<br /><br /> [安装 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)<br /><br /> [安装集成服务](../../integration-services/install-windows/install-integration-services.md)<br /><br /> [安装 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)<br /><br /> [安装 Reporting Services 本机模式报表服务器](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)|本节提供了用于安装 Analysis Services、Integration Services、Master Data Services 和 Reporting Services 的说明，其中，Analysis Services 和 Reporting Service 是在没有 SharePoint 的情况下安装的。 这有时称为*本机模式*，它是 Reporting Services 和 Analysis Services 的最常见安装方案。 在本节中，您将了解直接确定服务器的操作环境的安装选项。 对于 Reporting Services，这可能是预先配置的服务器，或者是要求首先执行多个配置步骤后才能使用的服务器。 对于 Analysis Services，您选择的安装选项将决定您可以部署到服务器的项目类型。|  
|[验证或 SQL Server BI 功能安装问题疑难解答](../../../2014/sql-server/install/verify-or-troubleshoot-sql-server-bi-feature-installation-problems.md)|本节包括用于验证安装的步骤。 本节还提供指向 Web 上的问题解决信息的链接。|  
  
## <a name="related-content"></a>相关内容  
  
|链接|任务|  
|----------|----------|  
|[升级到 SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)<br /><br /> [升级 Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)<br /><br /> [升级 PowerPivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)<br /><br /> [升级和迁移 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)|使用本节中的指导可以将服务器和内容从以前的版本升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|[卸载 SQL Server 2014](uninstall-sql-server.md)<br /><br /> [卸载 PowerPivot for SharePoint](../../../2014/sql-server/install/uninstall-power-pivot-for-sharepoint.md)<br /><br /> [卸载 Reporting Services](../../../2014/sql-server/install/uninstall-reporting-services.md)|使用本节中的说明可卸载 BI 功能。|  
  
## <a name="see-also"></a>请参阅

* [新增功能&#40;Reporting Services&#41;](../../../2014/reporting-services/what-s-new-reporting-services.md)

* [什么是 Analysis Services 和 Business Intelligence 中的新增功能](../../analysis-services/what-s-new-in-analysis-services.md)

* [安装 SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)

* [升级到 SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)
