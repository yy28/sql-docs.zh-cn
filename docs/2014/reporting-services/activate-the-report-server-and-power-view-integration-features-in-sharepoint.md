---
title: 激活报表服务器和 SharePoint 中的 Power View 集成功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c7f64a54-c555-4d31-bf99-3abe57dc8626
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e30ae6ea0e7fa314748c4da265650273c0a7d56e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66110029"
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>在 SharePoint 中激活报表服务器和 Power View 集成功能
  默认情况下，在安装用于 SharePoint 产品的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]外接程序后，通常会激活 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 网站集功能。 在某些情况下，您将需要手动激活这些功能。  
  
 如果在安装 SharePoint 产品后安装了用于 SharePoint 2010 产品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序，则仅对根网站集激活报表服务器集成功能和 Power View 集成功能。 对于其他网站集，您将需要手动激活这些功能。 例如，如果具有 **http://[我的服务器名称]/sites/[网站集名称]** 的网站集，将需要手动激活 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 网站集功能。  
  
 没有根网站集时， [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序将记录一条类似于以下内容的消息：  
  
 “SharePoint Web 应用程序 80 没有根网站集”  
  
 该消息将名为"RS_SP_ #.log"其中 # 为递增数字在外接程序安装日志中找到。 该日志文件位于当前用户的 Temp 文件夹中，例如 C:\Users\\[用户名]\AppData\Local\Temp。有关日志记录选项的外接程序的详细信息，请参阅[安装或卸载 Reporting Services 外接 for SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。  
  
 本主题内容：  
  
-   [若要激活报表服务器和 Power View 集成网站集功能：](#bkmk_features)  
  
-   [若要激活或停用 Reporting Services 管理中心网站集功能：](#bkmk_centraladmin)  
  
##  <a name="bkmk_features"></a> 若要激活报表服务器和 Power View 集成网站集功能：  
  
1.  打开浏览器，找到要激活 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能的网站。  
  
2.  单击 **“网站操作”**。  
  
3.  单击 **“网站设置”**。  
  
4.  在网站集管理组中单击 **“网站集功能”** 。  
  
5.  在列表中找到 **“报表服务器集成功能”** 或 **“Power View 集成功能”** 。  
  
6.  单击 **“激活”**。  
  
 若要停用这些功能，您可以使用相同的过程，但单击 **“停用”** 而非 **“激活”**。  
  
##  <a name="bkmk_centraladmin"></a> 若要激活或停用 Reporting Services 管理中心网站集功能：  
  
1.  打开浏览器找到 SharePoint 管理中心。  
  
2.  单击 **“网站操作”**。  
  
3.  单击 **“网站设置”**。  
  
4.  在网站集管理组中单击 **“网站集功能”** 。  
  
5.  在列表中找到 **“报表服务器管理中心功能”** 。  
  
6.  单击 **“激活”**。  
  
 若要停用这些功能，您可以使用相同的过程，但单击 **“停用”** 而非 **“激活”**。  
  
## <a name="next-steps"></a>后续步骤  
 激活此功能后，可以继续进行服务器集成。  
  
## <a name="see-also"></a>请参阅  
 [安装或卸载 Reporting Services 外接程序的 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
