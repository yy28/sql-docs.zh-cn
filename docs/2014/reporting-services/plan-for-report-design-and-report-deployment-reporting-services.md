---
title: 规划报表设计和报表部署 (Reporting Services 2014) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1c1e265e-52a2-4de3-96fd-ca4abae01c02
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4347854a56e0d6cb021a3958203d94c28cb96d22
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188492"
---
# <a name="plan-for-report-design-and-report-deployment-reporting-services-2014"></a>报表设计和报表部署的规划 (Reporting Services 2014)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供了创作和部署报表的多个方法。 使用本主题帮助计划协同工作的报表创作环境和报表服务器。 本主题概述了 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 组件对报表定义的支持。 报表定义是用报表定义语言 (RDL) 或客户端报表定义语言 (RDLC) 编写的 XML 文件。 每个报表定义都符合位于该文件开头的特定架构版本的要求。  
  
 RDL 文件是在 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 项目的报表设计器或报表生成器 3.0 中创作的。 RDLC 文件是使用包括在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中的 ReportViewer 控件创作的。  
  
 本主题内容：  
  
-   [RDL 架构版本](#bkmk_rdl_schema_versions)  
  
-   [报表服务器和 RDL 架构支持](#bkmk_report_server_rdl_schema_support)  
  
-   [报表创作和部署支持](#bkmk_report_authoring_and_deployment)  
  
-   [ReportViewer 控件](#bkmk_reportviewer)  
  
##  <a name="bkmk_rdl_schema_versions"></a> RDL 架构版本  
 下表列出了可用的每个架构版本及其缩写，这些缩写要在本主题的其余部分通篇使用：  
  
|缩写|架构版本|  
|------------------|--------------------|  
|2010 RDL|https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition|  
|2008 RDL|https://schemas.microsoft.com/sqlserver/reporting/2008/01/reportdefinition|  
|2005 RDL<br /><br /> 2005 RDLC|https://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition|  
|2000 RDL|https://schemas.microsoft.com/sqlserver/reporting/2003/10/reportdefinition|  
  
 有关 RDL 和 RDL 架构的详细信息，请参阅以下内容：  
  
-   [Microsoft SQL Server XML 架构](https://go.microsoft.com/fwlink/?LinkId=31850)  
  
-   [报表定义语言规范](https://go.microsoft.com/fwlink/?linkid=116865)  
  
-   [报表定义语言 (SSRS)](reports/report-definition-language-ssrs.md)  
  
 有关 ReportViewer 控件的详细信息，请参阅 [ReportViewer 控件 (Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx)。  
  
##  <a name="bkmk_report_server_rdl_schema_support"></a> 报表服务器和 RDL 架构支持  
 可以使用以下方法将报表定义文件部署到 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 报表服务器：  
  
-   **报表设计器：** 报表设计器中的部署报表[!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)]。  
  
-   **报表生成器：** 通过报表生成器将报表保存到报表服务器。  
  
-   **报表管理器：** 将报表上载到本机模式报表服务器从报表管理器。  
  
-   **SharePoint:** 将报表上载到 SharePoint 模式报表服务器使用配置的 SharePoint 站点。  
  
-   **以编程方式：** 使用报表服务器的 SOAP API 接口以编程方式发布报表。 有关详细信息，请参阅 [Report Server Web Service](report-server-web-service/report-server-web-service.md)。  
  
 下表按报表服务器的版本列出了支持的 rdl 架构版本。  
  
|报表服务器版本|RDL 架构版本|  
|---------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> 或<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> 或<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|2010 RDL<br /><br /> 2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]|2005 RDL<br /><br /> 2000 RDL|  
  
 如果您将报表定义上载到报表服务器或者升级包含现有报表的报表服务器，报表服务器将保留原格式的报表定义。 **首次使用时**，报表服务器会将报表服务器数据库中的报表升级到二进制格式，并保留这种格式以便以后查看。 报表定义 (.rdl) 本身不升级。  
  
 可以从报表服务器提取报表定义文件 (.rdl) 的只读副本。 在本机模式报表服务器上，浏览到报表管理器，选择该报表并单击 **“下载”**。 在 SharePoint 模式部署中，浏览到文档库，选择该报表并单击 **“下载副本”**。  
  
 若要升级报表定义，必须在报表创作环境中打开报表，然后保存它。  
  
 有关报表升级以及支持的架构版本的详细信息，请参阅 [升级报表](install-windows/upgrade-reports.md)。  
  
##  <a name="bkmk_report_authoring_and_deployment"></a> 报表创作和部署支持  
 报表创作环境为 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 项目中的报表设计器以及报表生成器。 报表创作环境对报表升级、报表设计、在本地模式下预览报表、在报表服务器上预览报表以及报表部署提供各种支持。  
  
 下表汇总了对不同架构版本的报表定义的创作和部署支持：  
  
|创作环境|创作的 RDL 版本|部署 RDL 版本|部署到的报表服务器的版本|  
|---------------------------|--------------------------|------------------------|--------------------------------------|  
|SQL Server 2014 Data Tools 中的报表设计器 - Microsoft 下载中心上的 Business Intelligence for Microsoft Visual Studio 2012。<br /><br /> 或<br /><br /> SQL Server 2012 Data Tools 中的报表设计器 - Microsoft 下载中心上的 Business Intelligence for Microsoft Visual Studio 2012。<br /><br /> 或<br /><br /> 包含在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]Data Tools 中的报表设计器。|作者 2010 RDL。 在打开现有的 RDL 时：<br /><br /> 2000 RDL, 升级到 2010 RDL<br /><br /> 2005 RDL, 升级到 2010 RDL<br /><br /> 2008 RDL，升级到 2010 RDL|2008 RDL<br /><br /> 2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Business Intelligence Development Studio 中的报表设计器|作者 2010 RDL。 在打开现有的 RDL 时：<br /><br /> 2000 RDL, 升级到 2010 RDL<br /><br /> 2005 RDL, 升级到 2010 RDL<br /><br /> 2008 RDL，升级到 2010 RDL|2008 RDL<br /><br /> 2010 RDL|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Business Intelligence Development Studio 中的报表设计器|作者 2008 RDL。 在打开现有的 RDL 时：<br /><br /> 2000 RDL, 升级到 2008 RDL<br /><br /> 2005 RDL, 升级到 2008 RDL|2008 RDL|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|  
|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 报表生成器|作者 2010 RDL。 在打开现有的 RDL 时：<br /><br /> 2000 RDL, 升级到 2010 RDL<br /><br /> 2005 RDL, 升级到 2010 RDL<br /><br /> 2008 RDL，升级到 2010 RDL|2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|  
|Visual Studio RDLC 报表设计器|2005 RDLC|不可用|不可用|  
  
 有关 [!INCLUDE[ss_dtbi_vs2013](../includes/ss-dtbi-vs2013-md.md)]的详细信息，请参阅以下内容：  
  
-   [SQL Server Data Tools 中的部署和版本支持 (SSRS)](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  
  
-   [Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)。  
  
##  <a name="bkmk_reportviewer"></a> ReportViewer 控件  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ReportViewer 控件可在本地预览模式或远程模式下显示 .rdlc 报表，该控件还可以显示在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器上托管的 .rdl 文件。 下表提供 ReportViewer 控件为进行本地处理 (.rdlc) 支持的 RDL 版本的列表。 [报表服务器和 RDL 架构支持](#bkmk_report_server_rdl_schema_support)一节中总结了服务器端 RDL 支持。  
  
|产品中的 ReportViewer 控件|用于本地预览的 RDL 版本|  
|-------------------------------------|--------------------------------------|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2013<br /><br /> 或<br /><br /> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2012<br /><br /> 或<br /><br /> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]|2008 RDL|  
|[!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)]<br /><br /> 或<br /><br /> [!INCLUDE[vsOrcas](../includes/vsorcas-md.md)]|2005 RDL|  
  
 有关详细信息，请参见以下内容：  
  
-   [将 RDLC 文件转换为 RDL 文件](https://msdn.microsoft.com/library/ms252109.aspx)  
  
-   [ReportViewer 控件 (Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx)  
  
-   [添加并配置 ReportViewer 控件](https://msdn.microsoft.com/library/ms252104.aspx)  
  
## <a name="see-also"></a>请参阅  
 [报表、报表部件和报表定义（报表生成器和 SSRS）](report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Reporting Services 工具](tools/reporting-services-tools.md)   
 [报表定义语言 (SSRS)](reports/report-definition-language-ssrs.md)  
  
  
