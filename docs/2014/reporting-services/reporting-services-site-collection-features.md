---
title: Reporting Services 网站集功能 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e05ae162-a4b2-489d-9853-d6b09414e632
caps.latest.revision: 5
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 88dd168355249d5b1f2dfd645ad7f42505597cde
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024737"
---
# <a name="reporting-services-site-collection-features"></a>Reporting Services 网站集功能
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式提供了三个 SharePoint 网站集功能。 功能支持常规[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]SharePoint 模式 reporting 环境中，[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]的一项功能[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]的外接程序[!INCLUDE[SPS2010](../includes/sps2010-md.md)]Enterprise Edition 和的管理操作[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中SharePoint 管理中心。  
  
## <a name="site-collection-features"></a>网站集功能  
 下表对 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 网站集功能进行了说明。  
  
|功能|Description|  
|-------------|-----------------|  
|**报表服务器管理中心功能**|启用用于管理与 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器的集成的功能。 此功能仅安装和用于 SharePoint 管理中心网站集中。<br /><br /> 在安装之后自动在 SharePoint 管理中心网站集合中激活报表服务器集成功能[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] SharePoint 产品的外接程序。 在某些情况下，您将需要手动激活该功能。 若要激活报表服务器功能，请在 SharePoint 管理中心的“站点设置”页中使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 页。<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]版本和更高版本的外接程序的 SharePoint 产品将激活所有现有网站集中的报表服务器集成功能时安装外接程序。 此外，对于新的网站集，此功能将自动激活。|  
|**报表服务器集成功能**|启用丰富的报表使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> 默认情况下此功能处于活动状态。|  
|**Power View 集成功能**|对 PowerPivot 工作簿和 Analysis Services 表格数据库启用交互式数据浏览和直观的展示。<br /><br /> 该功能可通过下列数据源的上下文菜单访问：<br /><br /> .rdlx<br /><br /> .rsds<br /><br /> .bism 连接文件<br /><br /> <br /><br /> 如果 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 未出现在上下文菜单中，请确认 **“Power View 集成功能”** 已激活。<br /><br /> 默认情况下此功能是被停用的。|  
  
## <a name="see-also"></a>请参阅  
 [激活报表服务器和 Power View Integration Features in SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Reporting Services 网站设置和网站功能&#40;SharePoint 模式&#41;](../../2014/reporting-services/reporting-services-site-settings-and-site-features-sharepoint-mode.md)   
 [在 SharePoint 管理中心中激活报表服务器文件同步功能](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)  
  
  