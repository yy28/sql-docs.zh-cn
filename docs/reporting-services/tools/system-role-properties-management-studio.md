---
title: "系统角色属性 (Management Studio) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.systemroleproperties.f1
ms.assetid: 0210fc2a-74fb-41dd-8e39-4830047ec417
caps.latest.revision: 30
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68038228fd6fb7b2af8dd6f1bb5ae50b7f63daac
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="system-role-properties-management-studio"></a>系统角色属性 (Management Studio)
  使用“系统角色”页可以查看当前为报表服务器定义的系统角色定义。 系统角色定义包含一组任务的命名集合，这些任务相对于整个站点（而不是单项）执行。 角色定义将分配给用户或组，以据此创建角色分配。 角色定义中的任务指定用户或组可以执行的任务。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]具有两个预定义的系统角色定义：**系统管理员**和**系统用户**。 您可以通过更改任务列表来修改这些角色定义，也可以创建支持其他任务组合的新系统角色。 对角色定义进行编辑将影响包括角色定义的所有角色分配。  
  
> [!NOTE]  
>  系统角色分配仅适用于在本机模式下运行的报表服务器。 如果针对报表服务器配置了 SharePoint 集成，则此页不可用。  
  
## <a name="options"></a>选项  
 **名称**  
 指定系统角色定义的名称。  
  
 **Description**  
 显示系统角色定义的说明。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，该说明仅在此页上可见。 通过报表管理器查看此项的用户在浏览文件夹层次结构时可能会看到此说明。  
  
 **任务**  
 列出可以为此角色定义选择的所有系统级任务。 可以在预定义任务列表中添加或删除项，以定义用户通过此角色访问给定项的方式。 不能创建新任务，也不能修改现有任务。  
  
 **Description**  
 提供每个任务的有关信息。 不能修改任务说明。  
  
## <a name="see-also"></a>另请参阅  
 [Management Studio F1 帮助中的报表服务器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [系统级任务](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md)   
 [任务和权限](../../reporting-services/security/tasks-and-permissions.md)   
 [预定义的角色](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  

