---
description: 角色定义
title: 角色定义 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- roles [Reporting Services], security
- security [Reporting Services], role definitions
- role-based security [Reporting Services], role definitions
ms.assetid: d1b8dbf0-4462-402e-92dd-0e4835002b6e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d8dbfe6d890c84bee9a66141971a554c410d47dd
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987377"
---
# <a name="role-definitions"></a>角色定义
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，*角色定义*是一组任务的命名集合，这些任务定义了可在报表服务器上执行的操作。 角色定义提供了报表服务器用于增强安全性的规则。 当用户尝试执行任务（如发布报表）时，报表服务器将检查用户的角色分配以确定该任务是否包含在其角色定义中。 如果试图执行的任务包括在角色定义中，则提交请求。  
  
## <a name="using-roles-to-authorize-access-to-a-report-server"></a>使用角色授予对报表服务器的访问权限  
 角色只有在角色分配中使用时才有效。 有关角色如何提供安全性的详细信息，请参阅 [角色分配](../../reporting-services/security/role-assignments.md)。  
  
## <a name="types-of-role-definitions"></a>角色定义的类型  
 角色定义既可以是项级定义也可以是系统级定义。 “项级角色定义”** 说明了与在报表服务器上存储和管理的项（如报表、文件夹和模型）相关的任务。 可以包含在项级角色定义中的任务如：管理报表、查看文件夹和管理单独的订阅。 “系统角色定义” ** 包含应用于整个站点的任务。 可以包含在系统角色中的任务如：查看报表服务器属性。  
  
## <a name="predefined-roles"></a>预定义角色  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含与不同级别的用户交互所对应的预定义角色。 下面的列表包含可以使用的预定义角色：  
  
-   为访问报表服务器内容创建角色分配时可以使用以下项级角色定义：内容管理员、发布者、浏览者、报表生成者和我的报表。  
  
-   授予对站点操作的访问权限时可以使用以下系统级角色定义：系统管理员和系统用户。  
  
 有关详细信息，请参阅 [预定义角色](../../reporting-services/security/role-definitions-predefined-roles.md)。  
  
## <a name="creating-a-role-definition"></a>创建角色定义  
 若要创建角色，请使用 Management Studio 指定名称及其所包含的任务。 必须为项和系统任务创建不同的角色定义。 角色可以包含项级任务或系统级任务，但不能同时包含这两种任务。 创建角色定义时，需要提供名称并为角色定义选择一组任务。 若要创建角色定义，您必须具有相应的权限。 “设置各项的安全性”任务可以提供这些权限。 默认情况下，分配了预定义的 **“内容管理员”** 角色的管理员和用户可以执行此任务。  
  
 角色必须拥有唯一的名称。 角色定义中至少必须包含一个任务才会有效。 有关详细信息，请参阅 [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md)。  
  
 若要创建角色定义，请使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 有关详细信息，请参阅 [创建、删除或修改角色 (Management Studio)](../../reporting-services/security/role-definitions-create-delete-or-modify.md)。  
  
 在创建角色定义后，可以通过在角色分配中选择该角色定义来使用它。 有关详细信息，请参阅 [授予用户对报表服务器的访问权限（报表管理器）](./grant-user-access-to-a-report-server.md)。  
  
## <a name="customize-or-delete-a-role-definition"></a>修改或删除角色定义  
 可以修改预定义角色，也可以用自定义角色替换它们。 若要修改角色，请向角色定义中添加任务或从角色定义中删除任务。 不能对角色重命名。 您所进行的任何更改都会立即应用到包含该角色定义的所有角色分配中。  
  
 如果不再使用该角色定义，可以删除它。 只要启用了“我的报表”功能，就不能删除为此功能选择的角色定义。 在删除用于“我的报表”功能的角色定义之前，首先必须禁用该功能，或为该功能另选一个角色定义以供使用。  
  
## <a name="see-also"></a>另请参阅  
 [任务和权限](../../reporting-services/security/tasks-and-permissions.md)   
 [授予对本机模式报表服务器的权限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [创建、删除或修改角色 (Management Studio)](../../reporting-services/security/role-definitions-create-delete-or-modify.md)   
 [授予用户对报表服务器的访问权限（报表管理器）](./grant-user-access-to-a-report-server.md)   
 [修改或删除角色分配（报表管理器）](../../reporting-services/security/role-assignments-modify-or-delete.md)   
 [在 SharePoint 站点上为报表服务器项设置权限（SharePoint 集成模式下的 Reporting Services）](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
  
