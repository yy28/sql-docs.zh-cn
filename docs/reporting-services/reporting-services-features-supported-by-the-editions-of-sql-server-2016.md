---
title: SQL Server 2016 各个版本支持的 Reporting Services 功能 | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 39f03d2d-6e48-4b34-a9d3-07f86313b937
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c1a1b85b3e6e7bb782c9e384eabc25ed986a7138
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43280096"
---
# <a name="reporting-services-features-supported-by-the-editions-of-sql-server-2016"></a>SQL Server 2016 各个版本支持的 Reporting Services 功能

本主题提供有关不同版本的 SQL Server 2016 所支持的功能的详细信息。  
  
 可在 180 天的试用期内使用 SQL Server 评估版。  
  
 有关最新的发行说明，请参阅 [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md)。 有关新增功能的最新信息，请参阅 [Reporting Services 中的新增功能 (SSRS)](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)。
    
 **试用 SQL Server 2016！**    
    
 > [![从评估中心下载](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[从评估中心下载 SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure 虚拟机小](../analysis-services/media/azure-virtual-machine-small.png) **[启动已安装 SQL Server 2016 的虚拟机](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    

有关评估版和开发人员版支持的功能，请参阅 SQL Server 企业版。

若要导航到 SQL Server 某种技术相应的表，请单击其链接：  

-   [Reporting Services](#SSRS)  
  
-   [Business Intelligence 客户端](#BIC)  

##  <a name="SSRS"></a> Reporting Services  
  
|功能名称|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|移动报表和 KPI|用户帐户控制||||||用户帐户控制|  
|支持的目录 DB [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Standard 或更高版本|Standard 或更高版本|Web|Express|||Standard 或更高版本|  
|支持的数据源 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|所有   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Web|Express|||所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|  
|报表服务器|用户帐户控制|是|是|是|||用户帐户控制|  
|报表设计器|用户帐户控制|是|是|是|||用户帐户控制|  
|报表设计器的 Web 门户|用户帐户控制|是|是|是|||用户帐户控制|  
|基于角色的安全性|用户帐户控制|是|是|是|||用户帐户控制|  
|导出到 Excel、PowerPoint、Word、PDF 和图像|用户帐户控制|是|是|是|||用户帐户控制|  
|增强的仪表和图表|用户帐户控制|是|是|是|||用户帐户控制|  
|将报表项固定到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]仪表板|用户帐户控制|是|是|是|||用户帐户控制|  
|自定义身份验证|用户帐户控制|是|是|是|||用户帐户控制|  
|作为数据馈送的报表|用户帐户控制|是|是|是|||用户帐户控制|  
|模型支持|用户帐户控制|是|是||||用户帐户控制|  
|为基于角色的安全性创建自定义角色|用户帐户控制|是|||||用户帐户控制|  
|模型项安全性|用户帐户控制|是|||||用户帐户控制|  
|无限制链接点击|用户帐户控制|是|||||用户帐户控制|  
|共享组件库|用户帐户控制|是|||||用户帐户控制|  
|电子邮件和文件共享订阅和计划|用户帐户控制|是|||||用户帐户控制|  
|报表历史记录、执行快照和缓存|用户帐户控制|是|||||用户帐户控制|  
|SharePoint 集成|用户帐户控制|是|||||用户帐户控制|  
|远程和非 SQL 数据源支持<sup>1</sup>|用户帐户控制|是|||||用户帐户控制|  
|数据源、传递和呈现、RDCE 可扩展性|用户帐户控制|是|||||用户帐户控制|  
|自定义品牌|用户帐户控制||||||用户帐户控制|  
|数据驱动报表订阅|用户帐户控制||||||用户帐户控制|  
|扩展部署（Web 场）|用户帐户控制||||||用户帐户控制|  
|警报<sup>2</sup>|用户帐户控制||||||用户帐户控制|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] <sup>2</sup>|用户帐户控制||||||用户帐户控制|  
  
 <sup>1</sup> 有关 SQL Server 2016 Reporting Services (SSRS) 支持的数据源的详细信息，请参阅 [Reporting Services 支持的数据源 (SSRS)](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
 <sup>2</sup> 在 SharePoint 模式下需要 Reporting Services。 有关详细信息，请参阅 [安装 Reporting Services SharePoint 模式](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。  
  
## <a name="report-server-database-server-edition-requirements"></a>报表服务器数据库的服务器版本要求  
 创建报表服务器数据库时，并非所有版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 均可用来承载数据库。 下表显示了可用于特定 [!INCLUDE[ssDE](../includes/ssde-md.md)] 版本的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]版本。  
  
|对于此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services 版本|使用此版本的数据库引擎实例来承载数据库|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|企业版或标准版（本地或远程）|  
|Standard|企业版或标准版（本地或远程）|  
|Web|Web Edition（仅用于本地）|  
|Express with Advanced Services|Express with Advanced Services（仅用于本地）。|  
|Evaluation|Evaluation|  
  
##  <a name="BIC"></a> Business Intelligence 客户端  
 以下软件客户端应用程序在 Microsoft 下载中心提供，它们旨在帮助你创建在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上运行的商业智能文档。 当你在某一服务器环境中托管这些文档时，请使用支持该文档类型的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 下表标识哪一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本包含承载在这些客户端应用程序中创建的文档所需的服务器功能。  
  
|工具名称|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] （.rdl 和 .rds）|用户帐户控制|是|||||用户帐户控制|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] （.rsmobile）|用户帐户控制||||||用户帐户控制|  
|用于移动设备的 Power BI 应用（iOS、Windows 10、Android）(.rsmobile)|用户帐户控制||||||用户帐户控制|  
  
> [!NOTE]  
> 1.  上表标识了启用这些客户端工具所需的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本；但是，这些工具可以访问在任何版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上托管的数据。  
> 2.  [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] 是创建移动报表的单一点。 连接到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务器来访问数据源并创建报表。 然后将其发布到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务器以供组织中其他人访问（在服务器上或在移动设备上）。 你还可以单独与本地数据源使用 [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)]  
> 3.  无论使用本地的  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 和/或云中的 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 作为报表传递解决方案，都只需要一个移动应用便可访问移动设备上的仪表板和移动报表。 可从 Windows、iOS 或 Android 应用商店下载 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 应用。  

## <a name="next-steps"></a>后续步骤

[SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[SQL Server 2016 的产品规格](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)  
[安装 SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md) 

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
