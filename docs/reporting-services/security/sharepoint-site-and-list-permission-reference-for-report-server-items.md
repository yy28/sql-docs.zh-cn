---
title: 报表服务器项的 SharePoint 站点和列表权限参考 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
- permission sets [Reporting Services]
ms.assetid: 1fcb27bd-4c4a-43f4-bfff-e42a59c87c49
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ee1a5dcf3d475937ae87a1f3c5282d484b2193a9
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570687"
---
# <a name="sharepoint-site-and-list-permission-reference-for-report-server-items"></a>报表服务器项的 SharePoint 站点和列表权限参考
  本主题提供了 SharePoint 中的权限参考，对于在 SharePoint 集成模式下运行的报表服务器，可使用这些权限来授予对报表服务器操作的访问权限。 如果要创建自定义权限级别，本主题可帮助您选择要使用何种权限。  
  
 SharePoint 提供了三十三种可用于控制对内容和操作的访问的权限。 其中有些但并非所有权限均可应用于涉及 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器的文档和操作。 可以通过本文中的权限参考表查找支持特定报表任务的权限。  
  
 每个表的前两列均列出了 SharePoint 权限及其说明。 表中有三列用于说明在预定义权限级别下如何使用权限。 预定义的权限级别包括：  
  
|权限级别|缩写|  
|----------------------|------------------|  
|完全控制|**F**|  
|参与|**C**|  
|访问者|**V**|  
  
 不会影响报表服务器的权限未在表中列出。 所有个性化权限均未列出在该参考文章中。 尽管可以将报表服务器项包括在个性化网站中，但报表服务器不会直接处理个性化请求或操作。  
  
||  
|-|  
| [!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式 | SharePoint 2010 和 SharePoint 2013。|  
  
## <a name="list-permissions"></a>列表权限  
 对包含报表服务器项的库设置的权限将确定用户如何访问这些项。  
  
|权限|描述|F|C|V|报表服务器操作|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|管理列表|创建和删除列表，添加或删除列表中的栏，添加或删除列表的公共视图。|X|||在从创作工具执行发布操作期间，在 SharePoint 库中创建文件夹。 管理报表历史记录也需要此权限。|  
|添加项|向列表中添加项目，向文档库中添加文档，添加 Web 讨论评论。|X|X||将报表、报表模型、共享数据源和资源（外部图像文件）添加到 SharePoint 库中。 创建共享数据源。 从共享数据源生成报表模型。 启动报表生成器并创建新报表，或将模型加载到报表生成器中。|  
|编辑项目|编辑列表中的项目、文档库中的文档、文档中的 Web 讨论评论以及自定义文档库中的 Web 部件页。<br /><br /> 创建订阅并编辑您创建的订阅。|X|X||查看文档以前的版本，包括报表历史记录快照。 为报表和其他文档编辑项属性。 设置报表处理选项。 设置报表参数。 编辑数据源属性。 创建报表历史记录快照。 在报表生成器中打开报表模型或基于模型的报表，并保存对文件所做的更改。 将链接型报表分配给模型中的实体。 用新的报表定义、共享数据源、报表模型或资源替换其旧版本（替换文件，保留元数据）。 管理报表或模型中引用的依赖项。 自定义与特定报表相关的报表查看器 Web 部件。<br /><br /> 创建、更改和删除使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 传递扩展插件将报表传递到目标位置的订阅。 只有订阅所有者和拥有“管理通知”权限的用户可以执行这些操作。|  
|删除项目|从列表中删除项目、从文档库中删除文档，以及删除文档中的 Web 讨论评论。|X|X||从库中删除报表、报表模型、共享数据源和其他文档。|  
|查看项|查看列表中的项目、文档库中的文档和 Web 讨论评论。|X|X|X|打开报表、报表模型和其他文档，并在报表服务器上对其进行处理。|  
|打开项|使用服务器端文件处理程序查看文档的源。|X|X|X|查看共享数据源的列表。 下载报表定义或报表模型的源文件副本。 查看将报表模型用作数据源的点击链接型报表。|  
|查看版本|查看列表项或文档以前的版本。|X|X|X|查看文档和报表快照以前的版本。|  
|删除版本|删除列表项或文档以前的版本。|X|X||删除文档和报表快照以前的版本。|  
  
> [!NOTE]  
>  其他列表权限包括“覆盖签出”、“批准项”和“查看应用程序页面”。 报表服务器不会评估这些权限。 报表服务器不会处理这些操作。  
  
## <a name="site-permissions"></a>网站权限  
 网站权限决定对与存储在特定库中的项不直接相关的报表服务器操作的访问。 例如，此类操作包括创建和管理共享计划（可由多个库中的项使用）以及配置报表查看器 Web 部件（可在整个网站内使用）。  
  
|权限|描述|F|C|V|报表服务器操作|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|管理权限|创建和更改网站上的权限级别，并为用户和组分配权限。|X|||可以更改针对所有报表服务器项和操作的权限。 可以设置模型项安全性。|  
|管理网站|执行网站的所有管理任务并管理内容。|X|||创建、更改和删除共享计划。|  
|添加和自定义网页|添加、更改或删除 HTML 页或 Web 部件页，以及使用与 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]兼容的编辑器编辑网站。|X|||添加或删除报表查看器 Web 部件。|  
|浏览用户信息|查看有关网站用户的信息。|X|X|X|浏览不同网站、库和文件夹中的报表以及其他项目。 将报表以及其他项目发布到库中。|  
|枚举权限|枚举对网站、列表、文件夹、文档或列表项的权限。|X|||读取所有报表服务器项的权限。 查看使用包含模型项安全设置的报表模型的点击链接型报表。|  
|管理警报|管理网站中所有用户的通知。|X|||创建、更改和删除网站上的任何订阅。|  
|使用远程接口|使用 SOAP、Web DAV 或 SharePoint Designer 接口访问网站。|X|X|X|用于调用报表服务器的 URL 代理端点。|  
|打开|打开网站、列表或文件夹以访问相应容器中的项。|X|X|X|读取计划和项属性。|  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 中的角色和任务与 SharePoint 组和权限的比较](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [在 SharePoint 站点上授予对报表服务器项的权限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
