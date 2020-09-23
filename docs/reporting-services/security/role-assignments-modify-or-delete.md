---
description: 修改或删除角色分配（SSRS Web 门户）
title: 修改或删除角色分配（SSRS Web 门户）| Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: defe3952f9fd3c5c4eb4453c2071820cb44a3fb8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480649"
---
# <a name="role-assignments---modify-or-delete"></a>角色分配 - 修改或删除

角色分配将组或用户帐户映射到预定义的角色，该角色定义可以执行的任务。 角色分配确定用户可针对文件夹、报表、模型或其他内容类型执行的任务类型。 若要创建、修改或删除角色分配，请使用 SSRS Web 门户。 在为特定用户或组创建了角色分配之后，您还可以通过选择其他角色来修改它。 如果要撤消对报表报务器的权限，可从报表服务器删除角色分配。  

根据您的目标，其他方法可能会更合适。 例如自定义或创建新的角色定义，或者在 Active Directory 中修改组帐户的成员身份。  

例如，假定有一组需要管理内容的用户，但他们不应具有与“内容管理员”关联的所有权限。 可以创建一个名为“部门内容管理员”的新角色定义。 它可以包含内容管理员中的所有任务，除了设置各项安全策略****。

同样，如果你是系统或网络管理员，在 Web 门户中管理 Active Directory 组帐户可能比管理角色分配更容易。 通过为组帐户创建单个角色分配，可以减少管理角色分配的开销。 然后，当用户不再需要访问报表时，可以修改组成员身份。
  
 如果确定修改或删除角色分配是最佳做法，那么，请记住要同时检查系统角色和项角色分配。 每种类型的角色分配都是通过 Web 门户中不同的页面配置的。
  
## <a name="to-modify-or-delete-a-system-role-assignment"></a>修改或删除系统角色分配
  
1. 访问[报表服务器的 Web 门户（SSRS 本机模式）](../../reporting-services/web-portal-ssrs-native-mode.md)。

2. 选择“站点设置” > “安全性”。 将按帐户名列出当前为服务器或扩展部署定义的所有系统级角色分配。

3. 查找要修改或删除的角色分配。

4. 若要为特定用户或组添加或删除角色，请选择“编辑”****。

5. 若要删除角色分配，请选择该用户或组名旁边的复选框，然后选择“删除”****。

### <a name="to-modify-or-delete-an-item-role-assignment"></a>修改或删除项角色分配

1. 访问 Web 门户并找出要为其编辑或删除角色分配的项。

2. 悬停在该项之上，然后选择下拉箭头。

3. 在下拉菜单中，选择“安全性”****。

4. 查找要修改或删除的角色分配。

5. 若要为特定用户或组添加或删除角色，请选择“编辑”****。

6. 若要删除角色分配，请选择该用户或组名旁边的复选框，然后选择“删除”****。

## <a name="see-also"></a>另请参阅

[创建和管理角色分配](../../reporting-services/security/create-and-manage-role-assignments.md)  
[角色分配](../../reporting-services/security/role-assignments.md)  
