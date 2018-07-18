---
title: 在 SharePoint 站点上授予对报表服务器项的权限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 0eb2f34a-3643-4b03-81c2-5741ba7ebefd
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2c106d3d086366146c0ed32dca78533238e81ed2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37183844"
---
# <a name="granting-permissions-on-report-server-items-on-a-sharepoint-site"></a>在 SharePoint 站点上授予对报表服务器项的权限
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 提供了内置安全功能。使用这些功能，你可以授予对从 SharePoint 站点和库访问的报表服务器项的访问权限。 如果已为用户分配权限，则在 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 和报表服务器之间配置集成设置后，这些用户就会立即拥有访问报表服务器项和操作的权限。 您可以使用现有权限上载报表定义和其他文档、查看报表、创建订阅以及管理项。  
  
 如果您尚未分配权限，或者您对 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]中的安全功能并不熟悉，请遵循以下指南：  
  
1.  在 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]的产品文档中，阅读有关标准 SharePoint 组的默认安全设置的内容，以了解如何管理权限和用户访问。  
  
2.  查看专门影响报表服务器项和操作访问的权限列表。 有关详细信息，请参阅[将为报表服务器项的 Windows SharePoint Services 中的内置安全性](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)。  
  
3.  将用户帐户和组帐户分配到预定义的 SharePoint 组。  
  
4.  可以选择创建新的权限级别和组，或修改现有权限级别和组以根据特定需要改变服务器访问权限。  
  
 若要将 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 安全功能用于报表服务器项，必须有一台在 SharePoint 集成模式下运行的报表服务器。  
  
## <a name="about-permissions-permission-levels-and-sharepoint-groups"></a>关于权限、权限级别和 SharePoint 组  
 下表提供了 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]中的安全功能简介。 有关详细信息，请参阅您的 SharePoint 站点上的“Windows SharePoint 帮助和操作指南”。  
  
-   安全对象包括站点、列表、库、文件夹和文档。  
  
-   权限是对执行特定任务的授权。 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 提供了 33 种预定义的权限，并且您可以将这些权限合并为一个权限级别。  
  
-   权限级别是针对某安全对象（如站点、库、列表、文件夹、项或文档）、可以授予用户或 SharePoint 组的一组权限。 它相当于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的角色定义。 有五个预定义的权限级别。 您可以对其进行自定义或根据需要创建新的权限级别。  
  
-   SharePoint 组是可在 SharePoint 站点上创建的用户组，用于管理对该站点的权限并为站点成员提供电子邮件分发列表。 SharePoint 组由 Windows 用户帐户和组帐户组成；如果您使用窗体身份验证，则 SharePoint 组由用户登录名组成。 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 提供了三个组。 您可以对其进行自定义或根据需要创建新的权限级别。  
  
-   权限继承允许子站点、列表和库以及项继承父站点的安全设置。 您可以使用继承的权限访问存储在 SharePoint 库中的报表服务器项。 使用权限继承和预定义的 SharePoint 组有助于简化部署，并且可以立即访问大多数报表服务器操作。  
  
## <a name="who-sets-permissions"></a>由谁设置权限  
 安装 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]、运行 SharePoint 配置向导和创建门户网站的管理员是默认的门户网站所有者。 站点所有者可以在管理中心为场或独立 SharePoint Web 应用程序设置权限，并且可以在顶级站点为每个 SharePoint Web 应用程序设置权限。 该所有者还可以指定其他站点所有者。  
  
 在 SharePoint Web 应用程序的顶级站点，网站集管理员可以为整个站点层次结构中的多个站点设置权限。 单个站点所有者可以执行与子站点相关的同样的任务。  
  
 服务器管理员或网站集管理员可设置确定其他站点所有者是否可以设置权限的选项。 根据您拥有的权限级别，您可能无法创建或自定义 SharePoint 组或权限级别。  
  
## <a name="using-predefined-sharepoint-groups-and-permission-levels"></a>使用预定义的 SharePoint 组和权限级别  
 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 产品文档建议你使用标准 SharePoint 组（即“Site name 所有者”、“Site name 成员”和“Site name 访问者”）并在站点级分配权限。 为其分配权限的多数用户都应是 Site name 访问者或 Site name 成员组的成员。 对父站点的权限可在整个站点层次结构中得到继承。 您可以对需要其他限制的特定项中断权限继承。  
  
 下列 SharePoint 组拥有以下预定义的权限级别：  
  
-   “所有者”  组拥有“完全控制”权限，通过这些权限，组成员可以更改站点内容、页面或功能。 “完全控制”访问权限应仅限于站点管理员。  
  
-    “成员”组拥有“参与讨论”级别权限，此权限允许组成员查看页面、编辑项、提交更改以待审批、添加项以及从列表中删除项。  
  
-    “访问者”组拥有“读取”级权限，通过这些权限，组成员能够查看页面、列表项和文档。  
  
 SharePoint 组拥有的权限级别可提供对许多报表服务器操作的快速访问。 如果您发现内置安全设置未提供所需访问级别，可创建自定义组或权限级别。  
  
 报表服务器操作支持的默认安全功能的详细信息，请参阅[将为报表服务器项的 Windows SharePoint Services 中的内置安全性](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)。  
  
 若要使用内置安全功能，您必须将 Windows 用户帐户或组帐户分配到 SharePoint 组。 除服务器管理员和门户网站所有者外（他们在安装软件时自动获得对 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 的访问权限），所有其他用户都必须获得授权才能访问服务器。  
  
## <a name="in-this-section"></a>本节内容  
 [将 Windows SharePoint Services 中的内置安全性用于报表服务器项](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
 说明如何使用预定义的 SharePoint 组和权限级别来访问报表服务器项。  
  
 [报表服务器项的 SharePoint 站点和列表权限参考](sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
 提供可用于访问报表服务器操作的所有 SharePoint 产品权限的参考。  
  
 [在 SharePoint Web 应用程序中设置报表服务器操作的权限](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)  
 说明特别报告功能的权限要求并提供使功能可用的建议方法。  
  
 [Reporting Services 中的角色和任务与 SharePoint 组和权限的比较](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
 简要介绍了 SharePoint 组与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的预定义角色定义之间的比较。  
  
 [SharePoint 站点上为报表服务器项设置权限&#40;Reporting Services SharePoint 集成模式下&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
 提供有关创建有权启动报表生成器和设置模型项安全性的新 SharePoint 组的说明。 此主题还包含有关为任意报表服务器项或操作设置自定义权限的通用原则。  
  
## <a name="see-also"></a>请参阅  
 [SharePoint 站点上为报表服务器项设置权限&#40;Reporting Services SharePoint 集成模式下&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Reporting Services 安全性和保护](reporting-services-security-and-protection.md)  
  
  
