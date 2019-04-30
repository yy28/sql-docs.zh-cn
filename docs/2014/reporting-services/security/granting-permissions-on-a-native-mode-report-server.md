---
title: 授予对本机模式报表服务器的权限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
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
manager: kfile
ms.openlocfilehash: 1188f0d5cb68a86b6e3f3305ec9b5a40e51a8d3a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242463"
---
# <a name="granting-permissions-on-a-native-mode-report-server"></a>授予对本机模式报表服务器的权限
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用基于角色的授权和身份验证子系统来确定哪些用户可以在报表服务器上执行操作和访问项。 基于角色的授权将角色分为用户或组可以执行的操作组。 身份验证基于内置的 Windows 身份验证或您提供的自定义身份验证模块。 您对这两种身份验证类型都可以使用预定义或自定义角色。  
  
## <a name="using-roles-to-grant-report-server-access"></a>使用角色授予报表服务器访问权限  
 所有用户都在定义特定访问级别的角色上下文中与报表服务器进行交互。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了预定义的角色，您可以为用户和组分配这些角色，从而让其可以立即访问报表服务器。 预定义角色例如有“内容管理员”、“发布者”和“浏览者”。 每个角色定义一个相关任务的集合。 例如，“发布者”  具有添加报表和创建用于存储这些报表的文件夹的权限。  
  
 角色分配通常从父节点继承，但是您可以通过为特定项创建新的角色分配来打破权限继承。 某个用户作为一个报表的“内容管理员”  角色成员的同时也可以是另一个报表的“浏览者”  角色的成员。  
  
 若要授予对报表服务器项和操作的访问权限，请遵循下列原则：  
  
1.  检查预定义角色，以确定是否可以按原样使用它们。 如果需要调整任务或额外定义角色，应该在开始向用户分配特定角色之前执行这些操作。 有关每个角色的详细信息，请参阅 [预定义角色](role-definitions-predefined-roles.md)。  
  
2.  明确需要访问报表服务器的用户和组以及访问级别。 应该为大多数用户分配 **“浏览者”** 角色或 **“报表生成者”** 角色。 应该为少量用户分配 **“发布者”** 角色。 应该只为极少数用户分配 **“内容管理员”** 角色。  
  
3.  对主文件夹（这是报表服务器文件夹层次结构的顶级文件夹），使用报表管理器为需要访问权限的每个用户或组分配角色。  
  
4.  在站点级，使用预定义的角色“系统用户”和“系统管理员”在报表管理器的“站点设置”页为每个用户和组创建系统级角色分配。  
  
5.  根据需要为特定文件夹、报表和其他项创建额外的角色分配。 应避免创建大量角色分配。 如果创建过多的角色分配，将很难跟踪每个用户的不同权限级别。  
  
> [!NOTE]  
>  如果已将报表服务器配置为在 SharePoint 集成模式下运行，则必须设置对 SharePoint 站点的权限以授予对报表服务器项的访问权限。 有关详细信息，请参阅 [在 SharePoint 站点上授予对报表服务器项的权限](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)。  
  
## <a name="who-sets-permissions"></a>由谁设置权限  
 最初，只有属于本地管理员组成员的用户才可以访问报表服务器。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装时将分配两个默认的角色，它们可向本地管理员组成员授予项级和系统级的访问权限。 这些内置角色分配允许本地 Administrators 组中的管理员向其他用户授予对报表服务器的访问权限并管理报表服务器项。 不能删除内置角色分配。 本地管理员始终具有完全管理报表服务器实例的权限。  
  
 由于对报表服务器的完全权限包括项级权限和系统级权限，因此本地管理员分配有以下角色：  
  
 需要进行其他配置才能在运行 Windows Vista 或 Windows Server 2008 的本地计算机上管理报表服务器实例。 有关详细信息，请参阅 [为本地管理配置本机模式报表服务器 (SSRS)](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
## <a name="how-permissions-are-stored"></a>如何存储权限  
 角色分配和定义都存储在报表服务器数据库中。 如果使用的是多种客户端工具或编程接口，则所有访问都受限于为整个报表服务器实例定义的权限。 如果在扩展部署中配置了多个报表服务器，则对一个实例定义的角色分配存储在共享数据库中，并由同一扩展部署中的所有其他实例使用。 因为角色分配与它们所保护的项一起存储，所以可以将数据库移到另一个报表服务器实例，而不会丢失已定义的权限。  
  
## <a name="tasks-and-tools-for-managing-permissions"></a>管理权限的任务和工具  
 使用以下工具可以管理角色定义和分配。  
  
|Tool|“任务”|  
|----------|-----------|  
|Management Studio - 用于查看、修改、创建和删除角色定义。|[创建、删除或修改角色 (Management Studio)](role-definitions-create-delete-or-modify.md)|  
|报表管理器 - 用于为用户和组分配角色。|[授予用户对报表服务器的访问权限（报表管理器）](grant-user-access-to-a-report-server.md)<br /><br /> [修改或删除角色分配（报表管理器）](role-assignments-modify-or-delete.md)|  
  
## <a name="see-also"></a>请参阅  
 [预定义角色](role-definitions-predefined-roles.md)   
 [在 SharePoint 站点上授予对报表服务器项的权限](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [针对报表服务器的身份验证](authentication-with-the-report-server.md)   
 (create-and-manage-role-assignments.md)   
 [Reporting Services 安全性和保护](reporting-services-security-and-protection.md)   
 [报表服务器内容管理（SSRS 本机模式）](../report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
