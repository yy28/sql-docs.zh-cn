---
title: 在何处查找用于 SharePoint 产品的 Reporting Services 外接程序 | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- rsSharePoint
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 11/16/2015
ms.openlocfilehash: adee6ee7d0d769d8e87e228c475b224a3e78675b
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637875"
---
# <a name="where-to-find-the-reporting-services-add-in-for-sharepoint-products"></a>在何处查找用于 SharePoint 产品的 Reporting Services 外接程序

用于 SharePoint 产品和技术 (rsSharePoint.msi) 的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) 外接程序可通过 Web 进行下载，它提供用于将报表服务器与 SharePoint 的部署进行集成的功能。  
  
> [!IMPORTANT]  
>  有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序、Report Server 和 SharePoint 的支持组合的列表，请参阅有关详细信息，请参阅[支持的 SharePoint 和 Reporting Services 服务器和外接程序的组合&#40;SQL Server 2014&#41;](supported-combinations-of-sharepoint-and-reporting-services-server.md)。  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 用于 SharePoint 产品的 Reporting Services 外接程序  
 若要下载并安装该外接程序，请访问 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 下载中心：  
  
-   [用于 Microsoft SharePoint 的 Microsoft® SQL Server 2014 Reporting Services 外接程序](https://www.microsoft.com/download/details.aspx?id=53162)  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 安装向导中还提供了该外接程序的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 版本：  
  
-   在安装向导的 **“功能选择”** 页上，选择 **“用于 SharePoint 产品的 Reporting Services 外接程序”** 。  
  
-   从命令提示符安装中，使用 **RS_SHPWFE** 选项安装该外接程序。 有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 命令提示符安装的详细信息，请参阅[Reporting Services SharePoint 模式和本机模式的命令提示符安装](install-reporting-services-at-the-command-prompt.md)。  
  
##  <a name="bkmk_sql11sp1"></a> [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 用于 SharePoint 产品的 Reporting Services 外接程序  
 该外接程序和报表服务器的 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 版本添加了对 SharePoint Server 2013 的支持。  
  
 若要下载并安装该外接程序，请访问 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 下载中心：  
  
-   SP1 加载项：  [用于 Microsoft® SharePoint® 的 Microsoft® SQL Server® 2012 SP1 Reporting Services 加载项](https://www.microsoft.com/download/details.aspx?id=35583)(https://www.microsoft.com/download/details.aspx?id=35583)。  
  
-   **SP1：**  [Microsoft® SQL Server® 2012 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=35575) (https://www.microsoft.com/download/details.aspx?id=35575)。  
  
##  <a name="bkmk_sql11"></a> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 用于 SharePoint 2010 产品的 Reporting Services 外接程序  
 从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本开始，此外接程序可以作为 SQL Server 安装向导的一部分在“功能选择”页中进行安装。 如果你希望单独下载和安装此外接程序，则可以通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 下载中心的 [用于 Microsoft® SharePoint® 技术 2010 的 Microsoft® SQL Server® 2012 Reporting Services 外接程序](https://go.microsoft.com/fwlink/?LinkID=207242) 页获得此文件的最新版本。  
  
##  <a name="bkmk_sql2008r2"></a>用于 SharePoint 2010 产品的 SQL Server 2008 R2 Reporting Services 外接程序  
 用于 Microsoft SharePoint 2010 产品的 Microsoft SQL Server 2008 R2 Reporting Services 外接程序由 SharePoint 2010 产品准备工具 (**PreRequisiteInstaller.exe**) 进行安装。 如果您希望单独下载和安装此外接程序，则可以通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 下载中心的 [SQL Server 2008 R2 Reporting Services Add-in for Microsoft SharePoint Technologies 2010](https://www.microsoft.com/download/details.aspx?id=622)（用于 Microsoft SharePoint 技术 2010 的 SQL Server 2008 R2 Reporting Services 外接程序）获得此文件的最新版本。  
  
> [!TIP]  
>  如果将其用于 SQL Server 2008 Service Pack 1 (SP1)（带有累积更新 #8 或更高版本），请查看 [将 SQL Server 2008 SP2 报表服务器与 SharePoint 2010 集成](https://technet.microsoft.com/library/ff946055%28SQL.100%29.aspx)中的“SharePoint 2010 集成的已知问题”部分。  
  
##  <a name="bkmk_sql2008sp2"></a>SQL Server 2008 SP2 Reporting Services 用于 SharePoint 2007 产品和技术的外接程序  
 Microsoft SQL Server 2008 SP2 Reporting Services 外接程序是 2008 外接程序的更新版本，它增加了对于将 2008 R2 报表服务器与 SharePoint 2007 产品相集成的支持。  
  
 您可以通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 下载中心的 [Microsoft SQL Server 2008 SP2 Reporting Services Add-in for Microsoft SharePoint Technologies](https://www.microsoft.com/download/details.aspx?id=793)（用于 Microsoft SharePoint 技术的 Microsoft SQL Server 2008 SP2 Reporting Services 外接程序）获得此文件的最新版本。  
  
##  <a name="bkmk_sql2008"></a>SQL Server 2008 Reporting Services 用于 SharePoint 2007 产品和技术的外接程序  
 用于 Microsoft SharePoint 技术的 Microsoft SQL Server 2008 Reporting Services 外接程序提供用于在 Microsoft Windows SharePoint Services 3.0 或 Microsoft Office SharePoint Server 2007 部署中运行报表服务器的功能。  
  
 您可以通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 下载中心的 [Microsoft SQL Server 2008 Reporting Services Add-in for Microsoft SharePoint Technologies](https://www.microsoft.com/download/details.aspx?id=622)（用于 Microsoft SharePoint 技术的 Microsoft SQL Server 2008 Reporting Services 外接程序）获得此文件的最新版本。  
  
## <a name="see-also"></a>另请参阅  
 [安装或卸载用于 sharepoint &#40;sharepoint 2010 和 sharepoint 2013&#41;的 Reporting Services 外接程序](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [将报表服务器内容类型添加到 SharePoint &#40;集成模式下&#41;的库 Reporting Services](../add-reporting-services-content-types-to-a-sharepoint-library.md)   
 [当卸载 Reporting Services 外接程序之后，您无法在非默认区域中浏览 SharePoint 页](https://support.microsoft.com/kb/2009212)  
  
  
