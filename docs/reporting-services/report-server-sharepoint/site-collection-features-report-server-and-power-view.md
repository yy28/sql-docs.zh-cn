---
title: "激活报表服务器和 Power View Integration Features in SharePoint |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7f64a54-c555-4d31-bf99-3abe57dc8626
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: bca4115307f7bf9dab5ffc9d2ab02ababb209d65
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="site-collection-features---report-server-and-power-view"></a>网站集功能的报表服务器和 Power View
  默认情况下，在安装用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 网站集功能。 在某些情况下，您将需要手动激活这些功能。  
  
 如果在安装 SharePoint 产品后安装了用于 SharePoint 2010 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序，则仅对根网站集激活报表服务器集成功能和 Power View 集成功能。 对于其他网站集，您将需要手动激活这些功能。 例如，如果具有 **http://[我的服务器名称]/sites/[网站集名称]** 的网站集，将需要手动激活 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 网站集功能。  
  
 没有根网站集时， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序将记录一条类似于以下内容的消息：  
  
 “SharePoint Web 应用程序 80 没有根网站集”  
  
 该消息可以在名为“RS_SP_#.log”的外接程序安装日志中找到，其中 # 为递增数字。 该日志文件位于当前用户的 Temp 文件夹中，例如 C:\Users\\[用户名]\AppData\Local\Temp。 有关该外接程序日志记录选项的详细信息，请参阅 [安装或卸载用于 SharePoint 的 Reporting Services 外接程序](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。  
  
 本主题内容：  
  
-   [若要激活报表服务器和 Power View 集成网站集功能：](#bkmk_features)  
  
-   [若要激活或停用 Reporting Services 管理中心网站集功能：](#bkmk_centraladmin)  
  
##  <a name="bkmk_features"></a> 若要激活报表服务器和 Power View 集成网站集功能：  
  
1.  打开浏览器，找到要激活 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能的网站。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [安装或卸载用于 SharePoint 的 Reporting Services 外接程序](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
