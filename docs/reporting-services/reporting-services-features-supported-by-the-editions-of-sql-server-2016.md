---
title: 不同版本支持的功能 - SQL Server Reporting Services | Microsoft Docs
description: 了解 SQL Server 各个版本支持的 SQL Server Reporting Services (SSRS) 功能。
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.date: 12/16/2019
ms.openlocfilehash: bbb3196349c648b955e5d27bf1d5fcfdadb9085f
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246656"
---
# <a name="sql-server-reporting-services-features-supported-by-editions"></a>不同版本支持的 SQL Server Reporting Services 功能

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

本主题介绍 SQL Server 各个版本支持的 SQL Server Reporting Services (SSRS) 功能。 可在 180 天的试用期内使用 SQL Server 评估版。  

## <a name="related-links"></a>相关链接
  
 - [SQL Server Reporting Services (SSRS) 发行说明](release-notes-reporting-services.md)。 
 - [SQL Server Reporting Services (SSRS) 最近更新](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)。
 - [不同 SQL Server 版本支持的功能](~/sql-server/editions-and-components-of-sql-server-version-15.md)

##  <a name="sql-server-reporting-services"></a><a name="SSRS"></a> SQL Server Reporting Services  

有关 Evaluation 和 Developer 版本支持的功能，请参阅下表中列出的 SQL Server Enterprise Edition 列。

|功能名称|Enterprise|Standard|Web|Express with Advanced Services|开发人员|  
|------|---------|---------------|-----------|-------|---------|  
| Power BI 报表和 Excel 工作簿 | 是，有软件保障 | | | | 是 |
|移动报表和分析|是||||是|  
|支持的目录数据库 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Standard 或更高版本|Standard 或更高版本|Web|Express|Standard 或更高版本|  
|支持的数据源 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|所有   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Web|Express|所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|  
|报表服务器|是|是|是|是|是|  
|报表设计器|是|是|是|是|是|  
|报表设计器的 Web 门户|是|是|是|是|是|  
|基于角色的安全性|是|是|是|是|是|  
|导出到 Excel、PowerPoint、Word、PDF 和图像|是|是|是|是|是|  
|增强的仪表和图表|是|是|是|是|是|  
|将报表项固定到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 仪表板|是|是|是|是|是|  
|自定义身份验证|是|是|是||是|  
|作为数据馈送的报表|是|是|是|是|是|  
|模型支持|是|是|是||是|  
|为基于角色的安全性创建自定义角色|是|是|||是|  
|模型项安全性|是|是|||是|  
|无限制链接点击|是|是|||是|  
|共享组件库|是|是|||是|  
|电子邮件和文件共享订阅和计划|是|是|||是|  
|报表历史记录、执行快照和缓存|是|是|||是|  
|SharePoint 集成<sup>2</sup>|是|是|||是|  
|远程和非 SQL 数据源支持<sup>1</sup>|是|是|||是|  
|数据源、传递和呈现以及 RDCE 扩展性|是|是|||是|  
|自定义品牌|是||||是|  
|数据驱动报表订阅|是||||是|  
|扩展部署（Web 场）|是||||是|  
|警报<sup>2</sup> (SSRS 2016) |是||||是|  
|Power View<sup>2</sup> (SSRS 2016) |是||||是| 
|注释<sup>3</sup> |是|是|是|是|是|  

 <sup>1</sup> 有关 SQL Server Reporting Services (SSRS) 支持的数据源详细信息，请参阅 [Reporting Services &#40;SSRS&#41; 支持的数据源](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
 <sup>2</sup> 在 SharePoint 模式下需要 SQL Server 2016 Reporting Services。 有关详细信息，请参阅 [安装 SQL Server Reporting Services SharePoint 模式](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。 自 SQL Server 2017 Reporting Services 之后，不再提供与 SharePoint 的集成这一功能。 

<sup>3</sup> 仅在 Power BI 报表服务器和 SQL Server 2017 Reporting Services 及更高版本中。

> [!NOTE]
> SQL Server Express with Tools 和 SQL Server Express 不支持 Reporting Services。
  
## <a name="edition-requirements-for-the-report-server-database"></a>报表服务器数据库的版本要求
 创建报表服务器数据库时，并非所有版本的 SQL Server [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 都可以用来承载数据库。 下表显示了可用于特定 SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 版本的 [!INCLUDE[ssDE](../includes/ssde-md.md)] 版本。  
  
|对于此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services 版本，|使用此版本的数据库引擎实例来承载数据库。|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Standard Edition 或 Enterprise Edition（本地或远程）|  
|Standard|Standard Edition 或 Enterprise Edition（本地或远程）|  
|Web|Web Edition（仅用于本地）|  
|Express with Advanced Services|具有高级服务的 Express（仅本地）|  
|计算|计算|  
  
##  <a name="business-intelligence-clients"></a><a name="BIC"></a>商业智能客户端  
Microsoft 下载中心提供以下软件客户端应用程序。 它们有助于创建在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上运行的商业智能文档。 当你在某一服务器环境中托管这些文档时，请使用支持该文档类型的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 下表标识哪一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本包含承载在这些客户端应用程序中创建的文档所需的服务器功能。  
  
|工具名称|Enterprise|Standard|Web|Express with Advanced Services|开发人员|  
|---------------|----------------|--------------|------------------------|-------------|---------------| 
| 更适用于 Power BI 报表服务器的 Power BI Desktop (.pbix) | 是，有软件保障 | | | | 是 |
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] （.rdl 和 .rds ）|是|是|是|是|是|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] (.rsmobile)|是||||是|  
|用于移动设备的 Power BI 应用（iOS、Windows 10 和 Android）(.rsmobile)|是||||是|  
  
> [!NOTE]  
> * 上表标识启用这些客户端工具所需的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 但是，这些工具可以访问任何 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本上承载的数据。  
> * [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] 是创建移动报表的单一点。 连接到 SSRS 服务器，以访问数据源并创建报表。 然后将其发布到 SSRS 服务器以供组织中其他人访问（在服务器上或在移动设备上）。 你还可以独立于本地数据源使用 [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)]。  
> * 无论使用本地的 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 和/或云中的 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 作为报表传递解决方案，你都只需要一个移动应用便可访问移动设备上的仪表板和移动报表。 可从 Windows、iOS 或 Android 应用商店下载 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 应用。  

## <a name="next-steps"></a>后续步骤

* 请参阅 [SQL Server 2017 各个版本支持的功能](~/sql-server/editions-and-components-of-sql-server-2017.md)。 

* [计划 SQL Server 安装](../sql-server/install/planning-a-sql-server-installation.md)。

* 更多疑问？ 请访问 [SQL Server Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)。
