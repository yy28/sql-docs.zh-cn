---
title: "Reporting Services 角色任务与SharePoint 组权限对比 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- security [Reporting Services], tasks
- roles [Reporting Services], predefined
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], predefined roles
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 429f1dbb-183a-4097-bd1b-693da9fe7a36
caps.latest.revision: "19"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b1ac3cd31061a749a035c9f4feb6ceef8bdebcd3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="reporting-services-roles-tasks-vs-sharepoint-groups-permissions"></a>Reporting Services 角色任务与SharePoint 组权限对比
  本主题将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式下基于角色和任务的授权功能与 SharePoint 产品中的安全功能进行比较。 本主题将比较角色、任务、SharePoint 组、权限级别和权限的术语及特征。  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式 &#124; SharePoint 2010 和 SharePoint 2013<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式|  
  
 **本主题内容：**  
  
-   [比较权限工具和术语](#bkmk_compare_tools_terms)  
  
-   [比较本机模式角色与 SharePoint 组](#bkmk_compare_roles_groups)  
  
-   [比较本机模式任务和 SharePoint 权限](#bkmk_compare_tasks_permissions)  
  
##  <a name="bkmk_compare_tools_terms"></a> 比较权限工具和术语  
 **本机模式：**[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式权限对象（角色和任务）在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中创建并在报表管理器中为各用户配置。  
  
 **SharePoint 模式：** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式使用 SharePoint 权限功能。 SharePoint 组和权限从以下“站点设置”  页进行管理。  
  
 下表比较 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式与 SharePoint 之间权限相关的对象和概念。  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式|SharePoint|  
|---------------------------------------------|----------------|  
|**角色：** 例如“内容管理员”。|**组：** 例如默认的“查看者”组。|  
|---|**权限级别组：** 例如“查看者”组的“仅查看”。|  
|**任务：** 例如“管理报表”。|**权限：** 例如，在“仅查看”组中，有“查看项”、“查看版本”和“查看应用程序页”权限相关的列表。|  
  
 有关 SharePoint 权限的详细信息，请参阅 [权限级别和权限](http://office.microsoft.com/windows-sharepoint-services-help/permission-levels-and-permissions-HA010100149.aspx) 以及 [在 SharePoint 2013 中确定权限级别和组](http://technet.microsoft.com/library/cc262690.aspx)。  
  
##  <a name="bkmk_compare_roles_groups"></a> 比较本机模式角色与 SharePoint 组  
 下表将在本机模式下的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的预定义角色定义与标准 SharePoint 组进行比较。 如果 SharePoint 组与您需要的特定角色不匹配，可以在 SharePoint 中创建自定义组并分配权限级别。  
  
 **注意**：可用的默认 SharePoint 组取决于用于创建 SharePoint 站点的站点模板。  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 角色|SharePoint 组|  
|--------------------------------------|-----------------------|  
|**浏览者**<br /><br /> 视图| 使用“访问者”组授予查看报表的权限。  “访问者”组拥有“读取”级权限，通过这些权限，组成员能够查看页面、列表项和文档。|  
|**内容管理员**<br /><br /> 拥有对所有项和项级操作的全部权限，包括设置安全性的权限。| 使用“所有者”组授予管理 SharePoint 站点上的报表服务器项的完全控制权限。  “所有者”组拥有“完全控制”权限，通过这些权限，组成员能够更改网站内容、页面或功能。 “完全控制”访问权限应仅限于站点管理员。|  
|**我的报表**|没有等同的组。  在 SharePoint 模式下运行的报表服务器不支持“我的报表”。 如果希望使用等同功能，可以使用 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 中的“我的站点”功能。|  
|**发布服务器**<br /><br /> 添加、更新、查看、删除报表、报表模型、共享数据源和资源。| 使用“成员”组授予在 SharePoint 站点上添加项、编辑项以及更新对依赖项的引用的权限。  “成员”组拥有“参与讨论”级权限，通过这些权限，组成员能够查看页面、添加和更新项以及提交更改以待批准。|  
|**报表生成器**<br /><br /> 在报表生成器中查看报表、自行管理单个订阅以及打开报表。|没有与“报表生成器”报表定义相对应的现成预定义权限级别或 SharePoint 组。  默认情况下，属于“成员”组或“所有者”组的用户拥有使用报表生成器的权限。  如果希望更多用户能够使用报表生成器，应创建自定义安全设置以提供类似于报表生成器角色所提供的权限级别。 有关详细信息，请参阅 [在 SharePoint 站点上为报表服务器项设置权限（SharePoint 集成模式下的 Reporting Services）](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)。|  
|-| 使用“查看者”组授予查看呈现的报表的权限。  “查看者”组无法下载或查看报表项的内容。<br /><br /> 注意：从 SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 开始，“查看者”组不具有创建订阅的权限。|  
| “系统用户”和“系统管理员” |这些角色对于在 SharePoint 模式下运行的报表服务器并不是必需的。  “系统用户”和“系统管理员”  对应于 SharePoint 场或 Web 应用程序级权限。 报表服务器不提供任何要求该级别授权的功能。|  
  
##  <a name="bkmk_compare_tasks_permissions"></a> 比较本机模式任务和 SharePoint 权限  
 下表将比较 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式任务与 SharePoint 权限。  “类型”列指示本机模式任务与系统角色或标准角色和项是否相关。 系统角色管理系统级别的权限，例如共享计划。  
  
|本机模式任务|角色类型|等效 SharePoint 权限|  
|----------------------|---------------|--------------------------------------|  
|使用报表|项|编辑项、查看项。|  
|创建链接报表|项|不提供支持。|  
|管理所有订阅|项|管理警报。|  
|管理数据源|项|添加项、编辑项、删除项、查看项。|  
|管理文件夹|项|添加项、编辑项、删除项、查看项。|  
|管理单独的订阅|项|编辑项目<br /><br /> 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]之前，所需的权限级别为“创建警报”。|  
|管理模型|项|添加项、编辑项、删除项、查看项。|  
|管理报表历史记录|项|编辑项、查看版本、删除版本。|  
|管理报表|项|添加项、编辑项、删除项、查看项。|  
|管理资源|项|添加项、编辑项、删除项、查看项。|  
|设置各项的安全性|项|管理权限|  
|查看数据源|项|查看项。|  
|查看文件夹|项|查看项。|  
|查看模型|项|查看项。|  
|查看报表|项|查看项。|  
|查看资源|项|查看项。|  
||||  
|执行报表定义|系统|查看项。|  
|生成事件|系统|管理网站。|  
|管理作业|系统|无（不支持）。|  
|管理报表服务器属性|系统|无（不适用）。 报表服务器并不控制用户是否拥有在管理中心中查看集成设置的权限。|  
|管理角色|系统|管理权限。|  
|管理共享计划|系统|管理网站、打开。|  
|管理报表服务器安全性|系统|无（不适用）。 报表服务器并不在 SharePoint 集成模式下运行的服务器上使用系统级角色分配。|  
|查看报表服务器属性|系统|无（不适用）。 报表服务器并不控制用户是否拥有在管理中心中查看集成设置的权限。|  
|查看共享计划|系统|打开项。|  
  
## <a name="see-also"></a>另请参阅  
 [在 SharePoint 站点上为报表服务器项设置权限（SharePoint 集成模式下的 Reporting Services）](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [在 SharePoint Web 应用程序中设置报表服务器操作的权限](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [在 SharePoint 站点上授予对报表服务器项的权限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [角色定义](../../reporting-services/security/role-definitions.md)   
 [预定义角色](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  
