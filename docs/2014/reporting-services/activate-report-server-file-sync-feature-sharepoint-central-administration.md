---
title: 激活报表服务器文件同步功能，在 SharePoint 管理中心 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 32d1988d-07e7-41c2-b636-e65ecfae4677
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 83ffe3e16bad4fdc1c60a818dd7f07bd47e00cb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137472"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-central-administration"></a>在 SharePoint 管理中心中激活报表服务器文件同步功能
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器文件同步功能利用 SharePoint 事件处理程序将报表服务器目录与文档库中的项进行同步。 当用户经常直接将已发布的报表项上载到 SharePoint 文档库时，此功能很有用。 如果文件同步功能未激活，则内容仍将（但不会频繁地）保持同步。  
  
 在安装之后可以在 SharePoint 站点管理激活文件同步功能[!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]SharePoint 产品的外接程序。  
  
 可对于每个站点（但不在网站集级别）手动激活和停用此功能。  
  
## <a name="prerequisites"></a>必要條件  
 必须安装用于 SharePoint 的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序。 如果未安装该外接程序，则文件同步功能在站点功能列表上将不可见。  
  
 若要验证安装，查看已安装应用程序的列表[!INCLUDE[msCoName](../includes/msconame-md.md)]Windows**控制面板**。 如果[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]安装外接程序，请按照本主题中的说明来激活报表服务器文件同步功能。  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>在站点上激活或停用 Reporting Services 文件同步功能  
  
1.  从您站点的主页中，单击 **“站点操作”** 菜单，然后单击 **“站点设置”**。  
  
2.  在 **“站点操作”** 中，单击 **“管理站点功能”**。  
  
3.  在列表中找到 **“报表服务器文件同步”** 。  
  
4.  单击 **“激活”**。  
  
> [!NOTE]  
>  若要停用报表服务器文件同步功能，可以使用相同的过程，但单击“停用”。  
  
## <a name="see-also"></a>请参阅  
 [解决报表部件&#40;报表生成器和 SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [激活报表服务器和 Power View Integration Features in SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [安装或卸载 Reporting Services 外接程序为 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [安装或卸载 Reporting Services 外接程序为 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  