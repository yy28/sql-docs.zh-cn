---
title: "将 Windows SharePoint Services 中的内置安全性用于报表服务器项 | Microsoft Docs"
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
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 9577e88d-c22b-4934-936f-e0f1400cedf5
caps.latest.revision: "14"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: be121a1676947f3e878c660aecc15f1ea82e0e11
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="use-built-in-security-in-windows-sharepoint-services-for-report-server-items"></a>将 Windows SharePoint Services 中的内置安全性用于报表服务器项
  SharePoint 提供了内置安全功能，您可以使用这些功能从 SharePoint 站点和库访问报表服务器项。 如果已为用户分配了站点和列表权限，则在配置了 SharePoint 和报表服务器之间的集成设置后，这些用户即可拥有访问报表服务器项和操作的权限。  
  
## <a name="securable-items"></a>安全对象  
 对站点或库定义的权限可以用来授予对报表服务器项的访问权限。 但是，如果要确保各项的安全，您可以对以下内容类型设置权限：  
  
|文件类型|Description|  
|---------------|-----------------|  
|.rdl|用来定义报表布局和数据检索命令的报表定义文件。 在处理报表时报表定义使用数据源连接信息来检索数据。 如果报表定义是在报表生成器中创建的特别报告，则该报表将与报表模型 (.smdl) 文件（设置了所呈现报表中的数据浏览的范围）成对使用。|  
|.smdl|用来描述数据结构以及它们之间如何关联的报表模型文件。 报表模型文件用来创建和运行报表生成器报表。|  
|.rsds|用来指定有关外部数据源连接信息的共享数据源文件。 报表定义 (.rdl) 和报表模型 (.smdl) 文件将使用共享数据源文件。 报表模型始终使用 .rsds 文件来获取有关基础数据源的连接信息。 报表定义可以使用 .rsds 文件，或者使用在报表的数据源属性中定义的连接信息。|  
|.rsc|定义报表项或数据区域的布局和结构的报表部件文件。 此文件用于将报表部件发布到服务器，以便其他报表作者可从报表部件库中重用该项。|  
|.rsd|定义查询语法和数据集属性的共享数据集文件。 共享数据集可在报表外部共享、存储、处理和缓存。|  
  
 计划、订阅和报表历史记录不是安全对象。 可以对站点或库设置权限以确定用户是否可以创建或使用计划、订阅和报表历史记录，但无法直接对这些项进行安全设置。  
  
 若要对单个项进行安全设置，请在库中选择该项，单击向下箭头并选择 **“管理权限”**。 在 **“操作”** 菜单上，选择 **“编辑权限”**。  
  
## <a name="using-built-in-groups-and-permission-levels-to-access-report-server-items"></a>使用内置组和权限级别来访问报表服务器项  
 如果使用权限继承和标准 SharePoint 组，则在对报表服务器和 SharePoint 实例配置集成设置后，即可访问大多数报表服务器操作。  
  
 SharePoint 提供标准组，这些标准组将映射到用来确定如何访问 SharePoint 站点上的文档和页面的预定义权限级别。 如果使用的是标准组和默认权限级别，并且将站点配置为继承权限，则可能要以下列方式使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能：  
  
|**SharePoint 组**|**权限级别**|**摘要**|**报表服务器访问**|  
|---------------------------|--------------------------|-----------------|------------------------------|  
|**所有者**|完全控制|所有者拥有创建、管理以及设置报表服务器项和操作安全性的完全权限。|设置对整个站点的库中存储的所有报表服务器项的访问权限。 设置报表模型内的权限（也称为模型项安全性）。 自定义报表查看器 Web 部件。 向库中添加报表和其他项。 为报表和其他文档编辑项属性。 删除报表和其他项。 查看报表，包括将报表模型用于数据浏览的报表。 设置报表的参数。 设置报表的处理选项。 生成报表模型。 在报表生成器中创建报表。 创建和管理共享数据源。 创建、更改和删除任何用户所拥有的订阅。 创建和管理在整个站点范围内使用的共享计划。 创建和管理文档版本，包括报表历史记录。 下载报表定义或报表模型的源文件。 替换报表定义、报表模型、共享数据源或资源（保留项属性和权限）。|  
|**成员**|参与|成员可以创建新项并将报表和模型项从设计工具发布到 SharePoint 库。|向库中添加报表和其他项。 为报表和其他文档编辑项属性。 删除报表和其他项。 查看报表，包括将报表模型用于数据浏览的报表。 查看文档的先前版本，包括报表历史记录快照（还要求用户拥有打开已创建相应报表历史记录的报表的权限）。 设置报表的参数。 设置报表的处理选项。 生成报表模型。 在报表生成器中创建报表。 创建和管理共享数据源。 创建、更改和删除该用户所拥有的订阅。 将共享计划与订阅配合使用。 创建和管理文档版本，包括报表历史记录。 下载报表定义或报表模型的源文件。 替换报表定义、报表模型、共享数据源或资源（保留项属性和权限）。|  
|**访问者** 和 **查看者**|读取|“访问者”可以查看报表|查看报表，包括将报表模型用于数据浏览的报表。|  
  
 如果没有使用内置组和权限级别，则必须包括特定的权限才能访问 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能。 有关详细信息，请参阅 [在 SharePoint Web 应用程序中设置报表服务器操作的权限](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)。  
  
## <a name="see-also"></a>另请参阅  
 [在 SharePoint 站点上授予对报表服务器项的权限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Reporting Services 中的角色和任务与 SharePoint 组和权限的比较](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [在 SharePoint Web 应用程序中设置报表服务器操作的权限](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [在 SharePoint 站点上授予对报表服务器项的权限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
