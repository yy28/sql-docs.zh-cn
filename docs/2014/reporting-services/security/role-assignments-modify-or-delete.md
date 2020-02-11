---
title: 修改或删除角色分配（报表管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
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
manager: kfile
ms.openlocfilehash: 14d0a9f95ea3abccd2d50f469fe068459baa9364
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101961"
---
# <a name="modify-or-delete-a-role-assignment-report-manager"></a>修改或删除角色分配（报表管理器）
  角色分配将组或用户帐户映射到包含可执行任务的预定义的角色定义。 角色分配确定用户可针对文件夹、报表、模型或其他内容类型执行的操作类型。 若要创建、修改或删除角色分配，请使用报表管理器。 在为特定用户或组创建了角色分配之后，您还可以通过选择其他角色来修改它。 如果要撤消对报表报务器的权限，可从报表服务器删除角色分配。  
  
 根据您的目标，其他方法可能会更合适。 例如自定义或创建新的角色定义，或者在 Active Directory 中修改组帐户的成员身份。  
  
 例如，假定有一组需要完全管理内容的用户，但他们不应具有与“内容管理员”关联的所有权限。 在这种情况下，您可以创建一个名为“部门内容管理员”的新角色定义，其中包括“内容管理员”中除 **“设置项的安全策略”** 以外的所有任务。  
  
 同样，如果您是系统管理员或网络管理员，并且对于您来说管理 Active Directory 组帐户比在报表管理器中管理角色分配更加容易，则您可以通过为组帐户创建一个角色分配来减少管理角色分配的开销，并且在用户不需要再访问报表时调整组成员身份。  
  
 如果您确定修改或删除角色分配是最佳做法，那么，请记住要同时检查系统角色分配和项角色分配。 每种类型的角色分配都是通过报表管理器中不同的页面配置的。  
  
### <a name="to-modify-or-delete-a-system-role-assignment"></a>修改或删除系统角色分配  
  
1.  启动 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
2.  单击 **“网站设置”**。  
  
3.  单击 **“安全性”** 。 将按帐户名列出当前为服务器或扩展部署定义的所有系统级角色分配。  
  
4.  查找要修改或删除的角色分配。  
  
5.  若要为特定用户或组添加或删除角色，请单击 **“编辑”**。  
  
6.  若要删除角色分配，请单击该用户或组名旁边的复选框，再单击 **“删除”**。  
  
### <a name="to-modify-or-delete-an-item-role-assignment"></a>修改或删除项角色分配  
  
1.  启动 **“报表管理器”** 并找出您要为其编辑或删除角色分配的项。  
  
2.  悬停在该项之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击“安全性”****。  
  
4.  查找要修改或删除的角色分配。  
  
5.  若要为特定用户或组添加或删除角色，请单击 **“编辑”**。  
  
6.  若要删除角色分配，请单击该用户或组名旁边的复选框，再单击 **“删除”**。  
  
## <a name="see-also"></a>另请参阅  
 （create-and-manage-role-assignments.md）   
 [角色分配](role-assignments.md)   
 ["站点设置" 页 &#40;报表管理器&#41;](../site-settings-page-report-manager.md)   
 [新系统角色分配： "编辑系统角色分配" 页 &#40;报表管理器&#41;](../new-system-role-assignments-edit-system-role-assignments-page-report-manager.md)  
  
  
