---
title: "Reporting Services 网站集功能 |Microsoft 文档"
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
ms.openlocfilehash: 7c86f9ecdbbf4955ba224e40c245fc412742fc30
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="reporting-services-site-collection-features"></a>Reporting Services 网站集功能

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Reporting Services SharePoint 模式提供了三个 SharePoint 网站集功能。 功能支持常规的 Reporting Services SharePoint 模式 reporting 环境中， [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]，SQL Server 2016 Reporting Services 外接程序，和 SharePoint 管理中心中的 Reporting Services 的管理操作的一个功能。

> [!NOTE]
> 与 SharePoint 的 reporting Services 集成 SQL Server 2016 之后将不再可用。
  
## <a name="site-collection-features"></a>网站集功能

 下表介绍 Reporting Services 网站集功能。  
  
|功能|Description|  
|-------------|-----------------|  
|**报表服务器管理中心功能**|启用用于管理与 Reporting Services 报表服务器集成功能。 此功能仅安装和用于 SharePoint 管理中心网站集中。<br /><br /> 在安装了用于 SharePoint 产品的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 外接程序之后，报表服务器集成功能将自动在 SharePoint 管理中心网站集中激活。 在某些情况下，你需要手动激活功能。 若要激活报表服务器功能，请在 SharePoint 管理中心的站点设置页中使用的 Reporting Services 页。<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Reporting Services 版本和更高版本的外接程序的 SharePoint 产品激活的所有现有的网站集的报表服务器集成功能安装外接程序时。 此外，此功能是自动活动对于新站点集合。|  
|**报表服务器集成功能**|启用丰富的报表使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]Reporting Services<br /><br /> 默认情况下此功能处于活动状态。|  
|**Power View 集成功能**|对 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿和 Analysis Services 表格数据库启用交互式数据浏览和直观的展示。<br /><br /> 该功能可通过下列数据源的上下文菜单访问：<br /><br /> **.rdlx**<br /><br /> **.rsds**<br /><br /> **.bism** 连接文件<br /><br /> <br /><br /> 如果 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 未出现在上下文菜单中，请确认 **“Power View 集成功能”** 已激活。<br /><br /> 默认情况下此功能是被停用的。|  

## <a name="next-steps"></a>后续步骤

[在 SharePoint 中激活报表服务器和 Power View 集成功能](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Reporting Services 网站设置和网站功能（SharePoint 模式）](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[在 SharePoint 管理中心中激活报表服务器文件同步功能](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)

