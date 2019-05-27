---
title: 不推荐使用 SQL Server 2014 中的 SQL Server Reporting Services 中的功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d5cbef64cbed910018e7d2f8dae1844074aaa3f5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109344"
---
# <a name="deprecated-features-in-sql-server-reporting-services-in-sql-server-2014"></a>SQL Server 2014 的 SQL Server Reporting Services 中不推荐使用的功能
  本主题介绍不推荐使用的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能。 在不推荐使用这些功能的版本中仍提供这些功能，但是计划在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的未来版本中删除它们。 在新的应用程序中不应使用这些不推荐使用的功能。  
  
 本主题内容：  
  
-   [SQL Server 2014 Reporting Services 中弃用的功能](#bkmk_2014)  
  
-   [SQL Server 2012 SP1 Reporting Services 不推荐使用的功能](#bkmk_2012sp1)  
  
-   [SQL Server 2012 Reporting Services 中弃用的功能](#bkmk_2012)  
  
-   [SQL Server 2008 R2 Reporting Services 不推荐使用的功能](#bkmk_kj)  
  
##  <a name="bkmk_2014"></a> SQL Server 2014 Reporting Services 不推荐使用的功能  
  
### <a name="features-not-supported-in-the-next-version-of-sql-server"></a>SQL Server 的下一版本中不支持的功能  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的 **下一个** 版本将不再支持以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能。 请不要在新的开发工作中使用这些功能，并尽快修改当前还在使用这些功能的应用程序。  
  
#### <a name="html-rendering-extension-device-information-settings"></a>HTML 呈现扩展插件的设备信息设置  
 不推荐使用 HTML 呈现扩展插件的以下设备信息设置。  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   缩放  
  
 有关 HTML 呈现扩展插件的详细信息，请参阅 [HTML Device Information Settings](html-device-information-settings.md)  
  
#### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Microsoft Word 和 Microsoft Excel 1997-2003 呈现  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] BIFF8 呈现扩展插件将 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表呈现为 [!INCLUDE[msCoName](../includes/msconame-md.md)] Word 和 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 1997-2003 二进制交换文件格式。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 包括在呈现的扩展插件[!INCLUDE[msCoName](../includes/msconame-md.md)]Office 2007-2010 开放 XML 格式。  
  
#### <a name="report-definition-language-rdl-2005-and-earlier"></a>报表定义语言 (RDL) 2005 和更早版本  
 不推荐使用报表定义语言 (RDL) 2005 和更早版本。 有关 RDL 的详细信息，请参阅[报表定义语言&#40;SSRS&#41;](reports/report-definition-language-ssrs.md)。  
  
 有关升级报表的详细信息，请参阅 [Upgrade Reports](install-windows/upgrade-reports.md)。  
  
#### <a name="sql-server-2005-and-earlier-custom-report-items"></a>SQL Server 2005 和更早版本的自定义报表项  
 不推荐使用为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 和更早版本编译的自定义报表项 (CRI)。  
  
#### <a name="reporting-services-snapshots-2005-and-earlier"></a>Reporting Services 快照 2005 和更早版本  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 使用快照呈现[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005年及更早版本已弃用。  
  
#### <a name="report-models"></a>报表模型  
 语义建模语言 (SMDL) 报表模型已不推荐使用。 尽管您可以继续使用现有报表模型作为数据源[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]报告应考虑更新你的报表以便删除对报表模型及其依赖关系。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不包含用于创建或更新报表模型的工具。 有关详细信息，请参阅[SQL Server 2014 中的 SQL Server Reporting Services 中的重大更改](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)。  
  
#### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Web 服务端点中不推荐使用的方法  
 在 <xref:ReportService2010.ReportingService2010> Web 服务端点中不推荐使用以下操作：  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
#### <a name="sharepoint-web-parts"></a>SharePoint Web 部件  
 不推荐使用安装 cab 文件 **RSWebParts.cab** 和可以从该 cab 文件解压缩的 SharePoint Web 部件。 不推荐使用的 Web 部件是报表资源管理器 (**SPExplorer.dwp**) 和报表查看器 (**SPViewer.dwp**)。  
  
 有关不推荐使用的 Web 部件的详细信息，请参阅 [使用 SharePoint Web 部件查看和浏览本机模式下的报表 (SSRS)](https://msdn.microsoft.com/library/ms159772.aspx)  
  
### <a name="features-not-supported-in-a-future-version-of-sql-server"></a>SQL Server 未来版本中不支持的功能  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的下一版本仍支持以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能，但以后的版本将删除这些功能。 具体是哪一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本现在还未确定。  
  
 没有在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中不推荐使用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。  
  
##  <a name="bkmk_2012sp1"></a> SQL Server 2012 SP1 Reporting Services 不推荐使用的功能  
 本节介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中不推荐使用的 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]功能。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的下一版本仍支持以下 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]功能，但以后的版本将删除这些功能。 具体是哪一 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 版本现在还未确定。  
  
### <a name="sharepoint-web-parts"></a>SharePoint Web 部件  
 不推荐使用安装 cab 文件 **RSWebParts.cab** 和可以从该 cab 文件解压缩的 SharePoint Web 部件。 不推荐使用的 Web 部件是报表资源管理器 (**SPExplorer.dwp**) 和报表查看器 (**SPViewer.dwp**)。  
  
 有关不推荐使用的 Web 部件的详细信息，请参阅 [使用 SharePoint Web 部件查看和浏览本机模式下的报表 (SSRS)](https://msdn.microsoft.com/library/ms159772.aspx)  
  
##  <a name="bkmk_2012"></a> SQL Server 2012 Reporting Services 不推荐使用的功能  
 本节介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中不推荐使用的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]功能。  
  
### <a name="html-rendering-extension-device-information-settings"></a>HTML 呈现扩展插件的设备信息设置  
 不推荐使用 HTML 呈现扩展插件的以下设备信息设置。  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   缩放  
  
 有关 HTML 呈现扩展插件的详细信息，请参阅 [HTML Device Information Settings](html-device-information-settings.md)  
  
### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Microsoft Word 和 Microsoft Excel 1997-2003 呈现  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] BIFF8 呈现扩展插件将 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表呈现为 [!INCLUDE[msCoName](../includes/msconame-md.md)] Word 和 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 1997-2003 二进制交换文件格式。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 包括在呈现的扩展插件[!INCLUDE[msCoName](../includes/msconame-md.md)]Office 2007-2010 开放 XML 格式。  
  
### <a name="report-definition-language-rdl-2005-and-earlier"></a>报表定义语言 (RDL) 2005 和更早版本  
 不推荐使用报表定义语言 (RDL) 2005 和更早版本。 有关 RDL 的详细信息，请参阅[报表定义语言&#40;SSRS&#41;](reports/report-definition-language-ssrs.md)。  
  
 有关升级报表的详细信息，请参阅 [Upgrade Reports](install-windows/upgrade-reports.md)。  
  
### <a name="sql-server-2005-and-earlier-custom-report-items"></a>SQL Server 2005 和更早版本的自定义报表项  
 不推荐使用为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 和更早版本编译的自定义报表项 (CRI)。  
  
### <a name="reporting-services-snapshots-2005-and-earlier"></a>Reporting Services 快照 2005 和更早版本  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 使用快照呈现[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005年及更早版本已弃用。  
  
### <a name="report-models"></a>报表模型  
 语义建模语言 (SMDL) 报表模型已不推荐使用。 尽管您可以继续使用现有报表模型作为数据源[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]报告应考虑更新你的报表以便删除对报表模型及其依赖关系。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不包含用于创建或更新报表模型的工具。 有关详细信息，请参阅[SQL Server 2014 中的 SQL Server Reporting Services 中的重大更改](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)。  
  
### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Web 服务端点中不推荐使用的方法  
 在 <xref:ReportService2010.ReportingService2010> Web 服务端点中不推荐使用以下操作：  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
##  <a name="bkmk_kj"></a> SQL Server 2008 R2 Reporting Services 不推荐使用的功能  
  
> [!NOTE]  
>  因为 SQL Server 2008 R2 是 SQL Server 2008 的次版本升级，所以，我们建议您也查看 SQL Server 2008 部分的内容。  
  
### <a name="report-server-web-service-endpoints"></a>报表服务器 Web 服务端点  
 在此版本中，Web 服务 <xref:ReportService2005.ReportingService2005> 和 <xref:ReportService2006.ReportingService2006> 已不推荐使用。 这些端点已替换为一个新端点：<xref:ReportService2010.ReportingService2010>。  
  
 新端点包含不推荐使用的端点中可用的所有功能和 SQL Server 2008 R2 中引入的新功能。  
  
## <a name="see-also"></a>请参阅  
 [新增功能&#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [后向兼容性](../getting-started/backward-compatibility.md)   
 [SQL Server 2014 中的 SQL Server Reporting Services 的行为更改](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [SQL Server 2014 的 SQL Server Reporting Services 中已停止使用的功能](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  
