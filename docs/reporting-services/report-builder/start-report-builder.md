---
title: "启动报表生成器 |Microsoft 文档"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
caps.latest.revision: 56
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e99d13a8e80a0ed2a5e584dcc0e20591507f8c92
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---

# <a name="start-report-builder"></a>启动报表生成器

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]独立的报表创作环境。 使用它，可以创建分页报表并将其发布到在本机或 SharePoint 集成模式下安装的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。  
  
 从 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] Web 门户或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中以 SharePoint 集成模式首次启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 时，系统会提示你从 Microsoft 下载中心下载。 
 
![report-builder-get-report-builder](../../reporting-services/report-builder/media/report-builder-get-report-builder.png) 
 
 你或管理员还可以 [从 Microsoft 下载中心将报表生成器安装到你的计算机上](http://go.microsoft.com/fwlink/?LinkID=219138)。 有关详细信息，请参阅 [安装报表生成器](../../reporting-services/install-windows/install-report-builder.md) 中的“使用系统管理器服务器安装报表生成器”。
 
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]当你安装 SQL Server Reporting Services; 时未安装你需要单独下载和安装它。  
  
 从 Web 门户或 SharePoint 站点启动 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 时，如果打开了较早版本的 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] ，请与你的管理员联系，管理员可以更新 Web 门户或 SharePoint 站点上的版本。  
  
## <a name="to-start-includessrbnoversionincludesssrbnoversion-mdmd-from-the-includessrsnoversionincludesssrsnoversion-mdmd-web-portal"></a>从 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] Web 门户启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
1.  在 Web 浏览器的地址栏中，键入报表服务器的 URL。 默认情况下，URL 是 http://\<*servername*> / 报表。  
  
2.  在 Web 门户的上栏中，选择“新建” > “分页报表”。  
  
     ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png "PBI_SSMRP_NewMenu")  
  
     第一次，将提示你 [安装报表生成器](../../reporting-services/install-windows/install-report-builder.md)。 
  
     之后将打开 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] ，然后就可以从报表服务器中创建分页报表或打开报表。  
  
## <a name="to-start-includessrbnoversionincludesssrbnoversion-mdmd-in-sharepoint-integrated-mode"></a>在 SharePoint 集成模式下启动 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]  
  
1.  导航到包含所需库的 SharePoint 站点。  
  
2.  打开库。  
  
3.  单击 **“文档”**。  
  
4.  在 **“新建文档”** 菜单上，单击 **“报表生成器报表”**。  
  
     第一次时，此操作将启动 SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 向导。 有关详细信息，请参阅 [Install Report Builder](../../reporting-services/install-windows/install-report-builder.md) 。  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 将打开，随后你可以在报表服务器中创建分页报表或打开报表。  
  
     **注意** 如果  “新建文档”菜单未列出 “报表生成器报表”、 “报表生成器模型”或 “报表数据源”，则需要将其内容类型添加到 SharePoint 库中。 有关详细信息，请参阅 [向 SharePoint 库添加 Reporting Services 内容类型](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)。  

## <a name="next-steps"></a>后续步骤

[SQL Server 2016 中的报表生成器](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
[设置报表生成器的默认选项](../../reporting-services/report-builder/set-default-options-for-report-builder.md)  

更多问题？ [尝试的 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)

