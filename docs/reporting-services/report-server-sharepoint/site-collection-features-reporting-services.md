---
title: "Reporting Services 网站集功能 |Microsoft 文档"
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
ms.assetid: e05ae162-a4b2-489d-9853-d6b09414e632
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b68204ab4c9a008db7c43d2c568d1c3ccedbcb7a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---

# <a name="site-collection-features---reporting-services"></a>网站集功能-Reporting Services

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式提供了三个 SharePoint 网站集功能。 功能支持常规[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式 reporting 环境中， [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]，SQL Server 2016 Reporting Services 外接程序，和的管理操作的一个功能[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在 SharePoint 管理中心。  
  
## <a name="site-collection-features"></a>网站集功能  
 下表对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 网站集功能进行了说明。  
  
|功能|Description|  
|-------------|-----------------|  
|**报表服务器管理中心功能**|启用用于管理与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器的集成的功能。 此功能仅安装和用于 SharePoint 管理中心网站集中。<br /><br /> 在安装了用于 SharePoint 产品的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 外接程序之后，报表服务器集成功能将自动在 SharePoint 管理中心网站集中激活。 在某些情况下，您将需要手动激活该功能。 若要激活报表服务器功能，请在 SharePoint 管理中心的“站点设置”页中使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 页。<br /><br /> 用于 SharePoint 产品的外接程序的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本和更高版本将在安装外接程序时为所有现有的网站集激活报表服务器集成功能。 此外，对于新的网站集，此功能将自动激活。|  
|**报表服务器集成功能**|使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]<br /><br /> 默认情况下此功能处于活动状态。|  
|**Power View 集成功能**|对 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿和 Analysis Services 表格数据库启用交互式数据浏览和直观的展示。<br /><br /> 该功能可通过下列数据源的上下文菜单访问：<br /><br /> **.rdlx**<br /><br /> **.rsds**<br /><br /> **.bism** 连接文件<br /><br /> <br /><br /> 如果 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 未出现在上下文菜单中，请确认 **“Power View 集成功能”** 已激活。<br /><br /> 默认情况下此功能是被停用的。|  

## <a name="next-steps"></a>后续步骤

[在 SharePoint 中激活报表服务器和 Power View 集成功能](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Reporting Services 网站设置和网站功能（SharePoint 模式）](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[在 SharePoint 管理中心中激活报表服务器文件同步功能](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

更多问题？ [尝试的 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
