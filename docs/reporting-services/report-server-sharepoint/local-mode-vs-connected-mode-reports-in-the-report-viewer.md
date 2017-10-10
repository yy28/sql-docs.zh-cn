---
title: "本地模式和在报表查看器的连接的模式报表对比 |Microsoft 文档"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 5f8342550dc105fb6d3544e1d8bd65fcd660ff64
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="local-mode-vs-connected-mode-reports-in-the-report-viewer"></a>本地模式和在报表查看器的连接的模式报表对比

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表可配置为在 *“本地模式”* 或 *“连接模式”*下运行，以利用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器。 您而是可以在数据扩展插件支持本地模式报表时，使用报表查看器直接从 SharePoint 呈现报表。 这种方法称为“本地模式” 。 在之前的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]版本中，SharePoint 场需连接到在 SharePoint 模式下配置的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器，以便报表查看器控件可以呈现报表。 这种方法称为“远程模式”  或“连接模式” 。  

> [!NOTE]
> 与 SharePoint 的 reporting Services 集成 SQL Server 2016 之后将不再可用。

 在*本地模式*没有任何[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]报表服务器。 必须安装 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序，但无需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器。 在本地模式中，用户可以查看报表，但无法使用订阅和数据警报之类的服务器端功能。  

## <a name="local-mode-vs-connected-mode-and-supported-extensions"></a>本地模式与连接模式对比以及支持的扩展插件

 **本地模式：** 当你具有支持本地模式的数据扩展插件时，报表查看器会直接从 SharePoint 呈现报表。 在*本地模式*没有任何[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]报表服务器。 必须安装 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序，但无需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器。 在本地模式下，用户可以查看报表，但 **无法** 使用订阅和数据警报之类的服务器端功能。  
  
 **连接模式**也称为 *远程模式* ，在 SharePoint 模式下需使用连接至 SharePoint 场的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器，以便报表服务器控件可以呈现报表。  
  
 下表列出了支持本地模式报表的数据处理扩展插件：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access 2010 报表扩展插件。 有关 Access Services 的详细信息，请参阅 [将 Access Services 与 SQL Reporting Services 配合使用：安装 SQL Server 2008 R2 Reporting Services 外接程序 (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=192686)。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 列表数据扩展插件。 有关 SharePoint 列表数据扩展插件的详细信息，请参阅 [Reporting Services 支持的数据源 (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
 还可以开发自定义数据处理扩展插件，以支持本地模式。 有关详细信息，请参阅 [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)。  
  
 本地模式支持呈现具有嵌入数据源或来自 .rsds 文件的共享数据源的报表。 但是，您不能管理报表或其关联的数据源。 如果您尝试进行管理，系统将会显示错误消息，因为在本地模式下不支持这样做。 仅在连接模式下支持在 SharePoint 站点中管理数据源。  
  
> [!NOTE]  
>  与以前的版本一样，您不能在 .rsds 文件中嵌入用户名和密码。  
  
## <a name="configure-local-mode-and-access-services-with-sharepoint-2013"></a>使用 SharePoint 2013 配置本地模式和访问服务

 您可以配置 SharePoint 2013 场支持现有的 Access 2010 Web 数据库和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本地模式。 有关详细信息，请参阅 [为 SharePoint Server 2013 中的 Web 数据库安装和配置 Access Services 2010](http://technet.microsoft.com/library/ee748653\(office.15\).aspx)。  
  
 不可能为 SharePoint 2013 创建新的 Access Web 数据库。 Access 2013 使用在 Access 中内置的新型数据库“Access Web 应用程序”  ，然后将其用作 Web 浏览器中的 SharePoint 应用程序并与他人共享。  
  
 有关详细信息，请参阅以下内容。  
  
-   [Access 2013 的新增功能](http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx) (http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx)。  
  
-   [Access 应用基本任务](http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500) (http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500)。  
  
## <a name="configure-local-mode-reporting-with-sharepoint-2010"></a>配置本地模式使用 SharePoint 2010 reporting

 本地模式要求 ASP.NET 会话状态。 安装 Access 服务将启用 ASP.Net 会话状态。 您也可以使用 PowerShell 来启用。  
  
1.  打开 SharePoint 2010 Management Shell。  
  
2.  键入下列命令：  
  
    ```  
    - Enable-SPSessionStateService  
    ```  
  
3.  在系统提示后，键入数据库的名称。  
  
4.  执行 IIS 重置。  
  
 有关详细信息，请参阅将 [Access Services 与 SQL Reporting Services 配合使用：安装 SQL Server 2008 R2 Reporting Services 外接程序 (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=192686) 和 [Enable-SPSessionStateService](http://technet.microsoft.com/library/ff607857\(v=office.15\).aspx)。  
  
## <a name="connected-mode"></a>“连接模式”

 有关在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 连接模式下使用 ADS 扩展插件的最新信息，请参阅 [SharePoint 站点中的 Access Services 报表显示数据扩展插件“ADS”中的错误](http://social.technet.microsoft.com/wiki/contents/articles/25298.access-services-report-in-sharepoint-site-shows-error-in-data-extension-ads.aspx)。  
  
## <a name="see-also"></a>另请参阅

 [支持的 Reporting Services 数据源](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
