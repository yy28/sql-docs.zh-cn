---
title: 授予对本机模式报表服务器的权限 | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- authorization [Reporting Services]
- server security [Reporting Services]
- role-based security [Reporting Services]
- items [Reporting Services], security
- permissions [Reporting Services], native mode
- published reports [Reporting Services], security
- reports [Reporting Services], security
- report items [Reporting Services], security
- role-based security [Reporting Services], about role-based security
- security [Reporting Services], role-based
ms.assetid: 260dc2e9-546c-4f04-9fa1-977e23c9d68c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: be6b0825244dee9f80f88a1b211eee5881d2a96a
ms.sourcegitcommit: 9bdecafd1aefd388137ff27dfef532a8cb0980be
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2020
ms.locfileid: "77147366"
---
# <a name="grant-permissions-on-a-native-mode-report-server"></a>授予对本机模式报表服务器的权限
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用基于角色的授权和身份验证子系统来确定哪些用户可以在报表服务器上执行操作和访问项。 基于角色的授权将角色分为用户或组可以执行的操作组。 身份验证基于内置的 Windows 身份验证或您提供的自定义身份验证模块。 您对这两种身份验证类型都可以使用预定义或自定义角色。
  
## <a name="use-roles-to-grant-report-server-access"></a>使用角色授予报表服务器访问权限
 所有用户都在定义特定访问级别的角色上下文中与报表服务器进行交互。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了预定义的角色，您可以为用户和组分配这些角色，从而让其可以立即访问报表服务器。 预定义角色的示例有“内容管理员”、“发布者”和“浏览者”    。 每个角色定义一个相关任务的集合。 例如，“发布者”  具有添加报表和创建用于存储这些报表的文件夹的权限。
  
 角色分配通常从父节点继承，但是您可以通过为特定项创建新的角色分配来打破权限继承。 某个用户作为一个报表的“内容管理员”角色成员的同时也可以是另一个报表的“浏览者”角色的成员   。
  
 允许访问报表服务器项和操作：
  
1. 检查预定义角色，以确定是否可以按原样使用它们。 如果需要调整任务或额外定义角色，请在向用户分配特定角色之前执行这些操作。 有关每个角色的详细信息，请参阅[预定义角色](../../reporting-services/security/role-definitions-predefined-roles.md)。
  
1. 明确需要访问报表服务器的用户和组以及访问级别。 将大多数用户分配到“浏览器”角色或“报表生成器”角色   。 将少数用户分配到“发布者”角色  。 仅将少数用户分配到“内容管理员”角色  。
  
1. 使用 Web 门户为需要访问权限的每个用户或组分配主文件夹中的角色。 主文件夹是报表服务器文件夹层次结构的顶层文件夹。
  
1. 在站点级别，在 Web 门户的“站点设置”页上，使用预定义角色“系统用户”和“系统管理员”，为每个用户和组创建系统级的角色分配    。
  
1. 根据需要为特定文件夹、报表和其他项创建额外的角色分配。 应避免创建大量角色分配。 如果创建过多，则很难跟踪每个用户的不同权限级别。
  
> [!NOTE]  
>  如果已将报表服务器配置为在 SharePoint 集成模式下运行，则必须设置对 SharePoint 站点的权限以授予对报表服务器项的访问权限。 有关详细信息，请参阅[授予对 SharePoint 站点上报表服务器项的权限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)。
> 
> 自 SQL Server 2016 之后，不再提供 Reporting Services 与 SharePoint 的集成这一功能。
  
## <a name="who-sets-permissions"></a>由谁设置权限
 最初，只有属于本地管理员组成员的用户才可以访问报表服务器。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装时将分配两个默认的角色，它们可向本地管理员组成员授予项级和系统级的访问权限。 本地管理员可以使用这些内置角色分配向其他用户授予对报表服务器的访问权限并管理报表服务器项。 不能删除内置角色分配。 本地管理员始终具有完全管理报表服务器实例的权限。
 
 需要进行其他配置才能在运行 Windows Vista 或 Windows Server 2008 的本地计算机上管理报表服务器实例。 有关详细信息，请参阅[为本地管理配置本机模式报表服务器 &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。
  
## <a name="how-permissions-are-stored"></a>如何存储权限
 角色分配和定义都存储在报表服务器数据库中。 如果使用各种客户端工具或编程接口，则所有访问都受限于为整个报表服务器实例定义的权限。 如果在扩展部署中配置多个报表服务器，则对一个实例定义的角色分配存储在共享数据库中，并由同一扩展部署中的所有其他实例使用。 因为角色分配与它们所保护的项一起存储，所以可以将数据库移到另一个报表服务器实例，而不会丢失已定义的权限。
  
## <a name="tasks-and-tools-for-managing-permissions"></a>管理权限的任务和工具
 使用以下工具可以管理角色定义和分配。
  
|工具|任务|  
|----------|-----------|  
|Management Studio：用于查看、修改、创建和删除角色定义|[创建、删除或修改角色 &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)|  
|Web 门户：用于将用户和组分配到角色|[授予用户对报表服务器的访问权限](../../reporting-services/security/grant-user-access-to-a-report-server.md)<br /><br /> [修改或删除角色分配](../../reporting-services/security/role-assignments-modify-or-delete.md)|  
  
## <a name="see-also"></a>另请参阅
 - [预定义角色](../../reporting-services/security/role-definitions-predefined-roles.md)  
 - [在 SharePoint 站点上授予对报表服务器项的权限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 - [针对报表服务器的身份验证](../../reporting-services/security/authentication-with-the-report-server.md)  
 - [创建和管理角色分配](../../reporting-services/security/create-and-manage-role-assignments.md)  
 - [Reporting Services 安全性和保护](../../reporting-services/security/reporting-services-security-and-protection.md)  
 - [报表服务器内容管理（SSRS 本机模式）；](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
