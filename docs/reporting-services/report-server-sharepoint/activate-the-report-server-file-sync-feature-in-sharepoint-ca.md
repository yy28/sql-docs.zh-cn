---
title: "激活报表服务器 File Sync Feature in SharePoint CA |Microsoft 文档"
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
ms.assetid: 32d1988d-07e7-41c2-b636-e65ecfae4677
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d9f1b75bc40693248526282a6565db340930601b
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-ca"></a>激活报表服务器 File Sync Feature in SharePoint CA
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器文件同步功能利用 SharePoint 事件处理程序将报表服务器目录与文档库中的项进行同步。 当用户经常直接将已发布的报表项上载到 SharePoint 文档库时，此功能很有用。 如果文件同步功能未激活，则内容仍将（但不会频繁地）保持同步。  
  
 在安装了用于 SharePoint 产品的 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 外接程序之后，可以在 SharePoint 站点管理中激活该文件同步功能。  
  
 可对于每个站点（但不在网站集级别）手动激活和停用此功能。  
  
## <a name="prerequisites"></a>先决条件  
 必须安装用于 SharePoint 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序。 如果未安装该外接程序，则文件同步功能在站点功能列表上将不可见。  
  
 若要验证是否已安装，请在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows **“控制面板”**中查看已安装应用程序的列表。 如果 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序已安装，请按照本主题中的说明激活报表服务器文件同步功能。  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>在站点上激活或停用 Reporting Services 文件同步功能  
  
1.  从您站点的主页中，单击 **“站点操作”** 菜单，然后单击 **“站点设置”**。  
  
2.  在 **“站点操作”** 中，单击 **“管理站点功能”**。  
  
3.  在列表中找到 **“报表服务器文件同步”** 。  
  
4.  单击 **“激活”**。  
  
> [!NOTE]  
>  若要停用报表服务器文件同步功能，可以使用相同的过程，但单击“停用”。  
  
## <a name="see-also"></a>另请参阅  
 [报表部件故障排除（报表生成器和 SSRS）](http://msdn.microsoft.com/en-us/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [在 SharePoint 中激活报表服务器和 Power View 集成功能](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
 [安装或卸载用于 SharePoint 的 Reporting Services 外接程序](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [安装或卸载用于 SharePoint 的 Reporting Services 外接程序](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
