---
title: 激活报表服务器文件同步功能在 SharePoint 管理中心 |Microsoft Docs
ms.prod: reporting-services-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 03/06/2017
ms.openlocfilehash: b56960b23370de3803f475c02aaee3b98ae491e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232911"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-central-administration"></a>在 SharePoint 管理中心中激活报表服务器文件同步功能

[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器文件同步功能利用 SharePoint 事件处理程序将报表服务器目录与文档库中的项进行同步。 当用户经常直接将已发布的报表项上载到 SharePoint 文档库时，此功能很有用。 如果文件同步功能未激活，内容仍将同步，但不是会频繁地。  
  
在安装了用于 SharePoint 产品的 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 外接程序之后，可以在 SharePoint 站点管理中激活该文件同步功能。  
  
可对于每个站点（但不在网站集级别）手动激活和停用此功能。  
  
## <a name="prerequisites"></a>先决条件  
 必须安装用于 SharePoint 的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序。 如果未安装外接程序，文件同步功能不会显示在站点功能列表中。  
  
 若要验证是否已安装，请在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows **“控制面板”** 中查看已安装应用程序的列表。 如果 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序已安装，请按照本主题中的说明激活报表服务器文件同步功能。  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>在站点上激活或停用 Reporting Services 文件同步功能  
  
1.  从你的站点的主页，单击**站点操作**菜单，然后单击**站点设置**。  
  
2.  在中**站点操作**，单击**管理站点功能**。  
  
3.  在列表中找到 **“报表服务器文件同步”** 。  
  
4.  单击 **“激活”**。  
  
> [!NOTE]  
>  若要停用报表服务器文件同步功能，可以使用相同的过程，但单击“停用”。  
  
## <a name="see-also"></a>请参阅  
 [报表部件故障排除&#40;报表生成器和 SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [在 SharePoint 中激活报表服务器和 Power View 集成功能](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [安装或卸载 Reporting Services 外接程序的 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [安装或卸载 Reporting Services 外接程序的 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
