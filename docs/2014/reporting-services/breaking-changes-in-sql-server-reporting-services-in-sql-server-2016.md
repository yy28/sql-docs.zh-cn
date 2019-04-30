---
title: SQL Server 2014 中的 SQL Server Reporting Services 中的重大更改 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e779a88940db2883846168535e7823c1723f4b4e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63266715"
---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2014"></a>SQL Server 2014 的 SQL Server Reporting Services 中的重大更改
  本主题介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的重大更改。 这些更改可能导致基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的早期版本的应用程序、脚本或功能无法继续使用。 您在升级时，或在自定义脚本或报表中可能会遇到这些问题。 有关详细信息，请参阅 [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)。  
  
 **本主题内容：**  
  
-   [SQL Server 2014 Reporting Services 重大更改](#bkmk_sql14)  
  
-   [SQL Server 2012 Reporting Services 重大更改](#bkmk_rc0)  
  
-   [SQL Server 2008 R2 Reporting Services 重大更改](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Reporting Services 重大更改  
 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中没有针对 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]的重大更改。  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Reporting Services 重大更改  
  
### <a name="sharepoint-mode-server-references-require-the-sharepoint-site"></a>SharePoint 模式服务器引用要求 SharePoint 网站  
 您不能在 URL 路径中使用虚拟名称来直接浏览或引用报表服务器。 例如：  
  
 `http://<Server name>/ReportServer`  
  
 现在要求您在 URL 路径中包括 SharePoint 网站。 例如，如果你的站点名称为`videos`，使用`sites`前缀，URL 将如下所示：  
  
 `http://<Server Name>/sites/videos/_vti_bin/ReportServer`  
  
### <a name="changes-to-sharepoint-mode-command-line-installation"></a>SharePoint 模式命令行安装的更改  
 输入设置 **/RSINSTALLMODE** 仅用于本机模式安装，不用于 SharePoint 模式安装。 例如，在不支持以下[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]:**了 /RSINSTALLMODE ="DefaultSharePointMode"**。 使用 **/RSSHPINSTALLMODE="DefaultSharePointMode"** 来代替该输入设置。  
  
 下面的语句是完整安装命令和参数集的示例： **setup /ACTION = install /FEATURES = SQL，RS / = Denali_INST1.../RSSHPINSTALLMODE ="DefaultSharePointMode"**  
  
 在命令行安装的详细信息，请参阅[命令提示符下安装的 Reporting Services SharePoint 模式和本机模式](install-windows/install-reporting-services-at-the-command-prompt.md)。  
  
### <a name="the-reporting-services-wmi-provider-no-longer-supports-configuration-of-sharepoint-mode"></a>Reporting Services WMI 提供程序不再支持 SharePoint 模式配置  
 现在使用 PowerShell cmdlet 和 SharePoint 管理中心完成 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 配置。 新的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式体系结构利用 SharePoint 服务体系结构。 SharePoint 不支持 WMI 接口。  
  
 下面的列表中包括受这些更改影响的组件和工作流：  
  
-   在 SharePoint 模式下将 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] WMI 提供程序用于 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的自定义应用程序。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 配置管理器、rskeymgmt.exe 和 rsconfig.exe。 代替使用这些实用工具配置 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式，使用 SharePoint 管理中心和 PowerShell。  
  
-   SQL Server Management Studio:客户不能引用服务器使用语法类似于 < m a c h > / < 实例名称 >。 从 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 版本开始，建议的方法是使用 SharePoint 站点 URL。 例如， **http://<sharepoint_server>/<sharePoint_site&gt**。 从 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]开始，SharePoint 站点 URL 是唯一支持的语法。  
  
### <a name="report-model-designer-is-not-available-in-sql-server-data-tools"></a>报表模型设计器在 SQL Server Data Tools 中不提供  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 不再支持报表模型项目。 在 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]中将不提供报表模型设计器。 无法在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中创建新的报表模型项目或打开现有项目，并且无法创建或更新报表模型。 若要更新报表模型，可以使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 或更早的工具。 您可以继续使用报表模型作为在 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 工具（例如报表生成器和报表设计器）中创作的报表中的数据源。 你用来创建查询以便从报表模型提取报表数据的查询设计器将继续在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中提供。  
  
##  <a name="bkmk_kj"></a> SQL Server 2008 R2 Reporting Services 重大更改  
 本节介绍 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的重大更改。  
  
> [!NOTE]  
>  因为 SQL Server 2008 R2 是 SQL Server 2008 的次版本升级，所以，我们建议您也查看 SQL Server 2008 部分的内容。  
  
### <a name="expanded-csv-data-renderer"></a>扩展的 CSV 数据呈现器  
 在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中，CSV 文件包括图表和仪表数据。 依赖于以前的 CSV 文件结构的应用程序将不再有效，因为针对图表和仪表添加了其他列。  
  
 有关详细信息，请参阅 [导出到 CSV 文件（报表生成器和 SSRS）](report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)中处理数据。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 中的 SQL Server Reporting Services 的行为更改](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [新增功能&#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [SQL Server 2014 中的 SQL Server Reporting Services 中已弃用的功能](deprecated-features-in-sql-server-reporting-services-ssrs.md)   
 [SQL Server 2014 的 SQL Server Reporting Services 中已停止使用的功能](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  
