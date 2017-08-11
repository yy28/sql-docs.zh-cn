---
title: "修改或删除角色分配 （报表管理器） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1a0db8452d082dddf6f5ffc39c1a9bd5802bf114
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="role-assignments---modify-or-delete"></a>角色分配的修改或删除
  角色分配将组或用户帐户映射到包含可执行任务的预定义的角色定义。 角色分配确定用户可针对文件夹、报表、模型或其他内容类型执行的操作类型。 若要创建、修改或删除角色分配，请使用报表管理器。 在为特定用户或组创建了角色分配之后，您还可以通过选择其他角色来修改它。 如果要撤消对报表报务器的权限，可从报表服务器删除角色分配。  
  
 根据您的目标，其他方法可能会更合适。 例如自定义或创建新的角色定义，或者在 Active Directory 中修改组帐户的成员身份。  
  
 例如，假定有一组需要完全管理内容的用户，但他们不应具有与“内容管理员”关联的所有权限。 在这种情况下，您可以创建一个名为“部门内容管理员”的新角色定义，其中包括“内容管理员”中除 **“设置项的安全策略”**以外的所有任务。  
  
 同样，如果您是系统管理员或网络管理员，并且对于您来说管理 Active Directory 组帐户比在报表管理器中管理角色分配更加容易，则您可以通过为组帐户创建一个角色分配来减少管理角色分配的开销，并且在用户不需要再访问报表时调整组成员身份。  
  
 如果您确定修改或删除角色分配是最佳做法，那么，请记住要同时检查系统角色分配和项角色分配。 每种类型的角色分配都是通过报表管理器中不同的页面配置的。  
  
### <a name="to-modify-or-delete-a-system-role-assignment"></a>修改或删除系统角色分配  
  
1.  启动[报表管理器（SSRS 本机模式）](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  单击 **“网站设置”**。  
  
3.  单击 **“安全性”**。 将按帐户名列出当前为服务器或扩展部署定义的所有系统级角色分配。  
  
4.  查找要修改或删除的角色分配。  
  
5.  若要为特定用户或组添加或删除角色，请单击 **“编辑”**。  
  
6.  若要删除角色分配，请单击该用户或组名旁边的复选框，再单击 **“删除”**。  
  
### <a name="to-modify-or-delete-an-item-role-assignment"></a>修改或删除项角色分配  
  
1.  启动 **“报表管理器”** 并找出您要为其编辑或删除角色分配的项。  
  
2.  悬停在该项之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击“安全性”。  
  
4.  查找要修改或删除的角色分配。  
  
5.  若要为特定用户或组添加或删除角色，请单击 **“编辑”**。  
  
6.  若要删除角色分配，请单击该用户或组名旁边的复选框，再单击 **“删除”**。  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理角色分配](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [角色分配](../../reporting-services/security/role-assignments.md)   
 [站点设置页面 &#40;报表管理器 &#41;](http://msdn.microsoft.com/library/4d67a01c-eae4-49ba-a6e8-8e983c0248f5)   
 [新建系统角色分配： 编辑系统角色分配页 &#40;报表管理器 &#41;](http://msdn.microsoft.com/library/62a22ab9-1eb4-4ce5-8dd7-06b5ed2d9a2a)  
  
  
