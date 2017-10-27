---
title: "激活报表服务器和 SharePoint 中的 Power View 集成功能 |Microsoft 文档"
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: e97378914a59fab938fc3e4c7926847effcffc94
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>激活报表服务器和 SharePoint 中的 Power View 集成功能

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Reporting Services 网站集功能激活默认情况下，在安装之后[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] SharePoint 产品的外接程序。 在某些情况下，你需要手动激活这些功能。  

> [!NOTE]
> 与 SharePoint 的 reporting Services 集成 SQL Server 2016 之后将不再可用。

 如果在安装 SharePoint 产品后安装 Reporting Services 外接程序用于 SharePoint 2010 产品，然后的报表服务器集成功能和 Power View 集成功能将仅激活对根网站集。 对于其他网站集，你需要手动激活这些功能。 例如，如果你具有的站点集合**http://[my 服务器名称] /sites/ [站点集合名称]**需要手动激活 Reporting Services 网站集功能。  
  
 当没有任何根网站集时，Reporting Services 外接程序会记录类似于以下的消息。  
  
 “SharePoint Web 应用程序 80 没有根网站集”  
  
 找到在外接程序安装日志中，名为"RS_SP_ #.log"其中 # 是递增的数字。 在当前用户 Temp 文件夹，例如 C:\Users 中找到日志文件，则\\[用户名] \AppData\Local\Temp。有关该外接程序日志记录选项的详细信息，请参阅 [安装或卸载用于 SharePoint 的 Reporting Services 外接程序](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>激活报表服务器和 Power View 集成网站集功能
  
1.  打开浏览器指向其中所需的 Reporting Services 功能活动的站点。  
  
2.  单击 **“网站操作”**。  
  
3.  单击 **“网站设置”**。  
  
4.  在网站集管理组中单击 **“网站集功能”** 。  
  
5.  在列表中找到 **“报表服务器集成功能”** 或 **“Power View 集成功能”** 。  
  
6.  单击 **“激活”**。  
  
 若要停用这些功能，您可以使用相同的过程，但单击 **“停用”** 而非 **“激活”**。  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>激活或停用 Reporting Services 管理中心网站集功能
  
1.  打开浏览器找到 SharePoint 管理中心。  
  
2.  单击 **“网站操作”**。  
  
3.  单击 **“网站设置”**。  
  
4.  在网站集管理组中单击 **“网站集功能”** 。  
  
5.  在列表中找到 **“报表服务器管理中心功能”** 。  
  
6.  单击 **“激活”**。  
  
 若要停用这些功能，您可以使用相同的过程，但单击 **“停用”** 而非 **“激活”**。  
  
## <a name="next-steps"></a>后续步骤

激活此功能后，可以继续进行服务器集成。

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)

