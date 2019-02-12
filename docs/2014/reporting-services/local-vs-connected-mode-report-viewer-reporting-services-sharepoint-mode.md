---
title: 报表查看器中的本地模式和连接模式报表对比 (SharePoint 模式下的 Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a230a9bb-6046-401f-b5e5-53ff6edf2264
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9393d4c4cdd3e3655a5088d8b1dd2bcfb33285a5
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039614"
---
# <a name="local-mode-vs-connected-mode-reports-in-the-report-viewer-reporting-services-in-sharepoint-mode"></a>报表查看器中的本地模式和连接模式报表对比（SharePoint 模式下的 Reporting Services）
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表可配置为在 *“本地模式”* 或 *“连接模式”* 下运行，以利用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器。 您而是可以在数据扩展插件支持本地模式报表时，使用报表查看器直接从 SharePoint 呈现报表。 这种方法称为“本地模式” 。 在之前的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]版本中，SharePoint 场需连接到在 SharePoint 模式下配置的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器，以便报表查看器控件可以呈现报表。 这种方法称为“远程模式”  或“连接模式” 。  
  
 “本地模式”中没有 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器。 必须安装 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序，但无需 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器。 在本地模式中，用户可以查看报表，但无法使用订阅和数据警报之类的服务器端功能。  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式|  
  
 **本主题内容：**  
  
-   [本地模式与连接模式对比以及支持的扩展插件](#bkmk_local_vs_connected)  
  
-   [使用 SharePoint 2013 配置本地模式和 Access Services](#bkmk_local_mode_sharepoint2013)  
  
-   [使用 SharePoint 2010 配置本地模式报告](#bkmk_local_mode_sharepoint2010)  
  
##  <a name="bkmk_local_vs_connected"></a> 本地模式与连接模式对比以及支持的扩展插件  
 **本地模式：** 当你具有支持本地模式的数据扩展插件时，报表查看器会直接从 SharePoint 呈现报表。 “本地模式”中没有 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器。 必须安装 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序，但无需 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器。 在本地模式下，用户可以查看报表，但 **无法** 使用订阅和数据警报之类的服务器端功能。  
  
 **连接模式**也称为 *远程模式* ，在 SharePoint 模式下需使用连接至 SharePoint 场的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器，以便报表服务器控件可以呈现报表。  
  
 下表列出了支持本地模式报表的数据处理扩展插件：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Access 2010 报表扩展插件。 有关 Access services 的详细信息，请参阅[使用 Access Services 和 SQL Reporting Services:安装 SQL Server 2008 R2 Reporting Services 外接程序 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=192686)。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 列表数据扩展插件。 有关 SharePoint 列表数据扩展插件的详细信息，请参阅 [Reporting Services 支持的数据源 (SSRS)](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
 还可以开发自定义数据处理扩展插件，以支持本地模式。 有关详细信息，请参阅 [Implementing a Data Processing Extension](extensions/data-processing/implementing-a-data-processing-extension.md)。  
  
 本地模式支持呈现具有嵌入数据源或来自 .rsds 文件的共享数据源的报表。 但是，您不能管理报表或其关联的数据源。 如果您尝试进行管理，系统将会显示错误消息，因为在本地模式下不支持这样做。 仅在连接模式下支持在 SharePoint 站点中管理数据源。  
  
> [!NOTE]  
>  与以前的版本一样，您不能在 .rsds 文件中嵌入用户名和密码。  
  
##  <a name="bkmk_local_mode_sharepoint2013"></a> 使用 SharePoint 2013 配置本地模式和 Access Services  
 您可以配置 SharePoint 2013 场支持现有的 Access 2010 Web 数据库和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 本地模式。 有关详细信息，请参阅 [为 SharePoint Server 2013 中的 Web 数据库安装和配置 Access Services 2010](https://technet.microsoft.com/library/ee748653\(office.15\).aspx)。  
  
 不可能为 SharePoint 2013 创建新的 Access Web 数据库。 Access 2013 使用在 Access 中内置的新型数据库“Access Web 应用程序”  ，然后将其用作 Web 浏览器中的 SharePoint 应用程序并与他人共享。  
  
 有关详细信息，请参阅以下内容。  
  
-   [Access 2013 中的新增功能](http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx) (http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx)。  
  
-   [Access 应用的基本任务](http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500)(http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500)。  
  
##  <a name="bkmk_local_mode_sharepoint2010"></a> 使用 SharePoint 2010 配置本地模式报告  
 本地模式要求 ASP.NET 会话状态。 安装 Access 服务将启用 ASP.Net 会话状态。 您也可以使用 PowerShell 来启用。  
  
1.  打开 SharePoint 2010 Management Shell。  
  
2.  键入下列命令：  
  
    ```  
    - Enable-SPSessionStateService  
    ```  
  
3.  在系统提示后，键入数据库的名称。  
  
4.  执行 IIS 重置。  
  
 有关详细信息，请参阅[使用 Access Services 和 SQL Reporting Services:安装 SQL Server 2008 R2 Reporting Services 外接程序 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=192686)并[Enable-spsessionstateservice](https://technet.microsoft.com/library/ff607857\(v=office.15\).aspx)。  
  
## <a name="connected-mode"></a>“连接模式”  
 有关在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 连接模式下使用 ADS 扩展插件的最新信息，请参阅 [SharePoint 站点中的 Access Services 报表显示数据扩展插件“ADS”中的错误](https://social.technet.microsoft.com/wiki/contents/articles/25298.access-services-report-in-sharepoint-site-shows-error-in-data-extension-ads.aspx)。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 支持的数据源 (SSRS)](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
