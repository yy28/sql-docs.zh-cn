---
title: 新建角色分配：编辑角色分配页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 3319ced0-4b86-42af-b18d-da41a625113c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fc4dd805faffb9fcf172f372f48d497a037fd16c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188395"
---
# <a name="new-role-assignment-edit-role-assignment-page-report-manager"></a>新建角色分配：编辑角色分配页 （报表管理器）
  使用“新建角色分配”或“编辑角色分配”页可以授予对报表服务器项和操作的权限。 需要访问报表服务器的每个用户都必须拥有用来定义访问级别的角色分配。 可以针对根节点或者针对特定的报表、模型、文件夹、资源或共享数据源创建角色分配。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安全性可以通过您应用到项的角色分配来强制执行。 角色分配将某个组或用户匹配到某个角色定义，每个角色定义标识该组或用户可以执行的与某一特定项相关的任务。  
  
 项级的角色分配的影响面可以更广。 虽然它们可以与单个报表或文件夹关联，但还可以在文件夹层次结构中的更高级别定义它们，并且树视图中更低位置的文件夹和项可以继承它们。 有关详细信息，请参阅 [授予用户对报表服务器的访问权限（报表管理器）](security/grant-user-access-to-a-report-server.md)。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-new-role-assignment-or-edit-role-assignment-page"></a>打开“新建角色分配”或“编辑角色分配”页  
  
1.  打开“报表管理器”，并找出您要为其添加新角色分配或编辑角色分配的项。  
  
2.  悬停在该项之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“安全性”**。 这会打开该项的“安全属性”页。  
  
4.  如果您要添加新的角色分配，则在工具栏中单击 **“新建角色分配”**。 如果您要编辑角色分配，请单击要编辑的组或用户名旁边的 **“编辑”** 。  
  
    > [!NOTE]  
    >  如果某项当前从父项继承安全性，则在工具栏中单击 **“编辑项安全设置”** 可以更改安全设置。  
  
## <a name="options"></a>选项  
 **组或用户名称**  
 键入要为其创建角色分配的组或用户帐户的名称。 组名或用户名必须是有效的 Windows 域帐户。 按以下格式输入帐户：\<域 >\\< 帐户\>。  
  
> [!NOTE]  
>  此框仅可用于“新建角色分配”页上。  
  
 **角色**  
 显示报表服务器中定义的可用于定义项安全性的所有角色。 创建或更改报表或文件夹的角色分配时，选择一个或多个角色，直到组合任务集能够说明应允许用户执行的操作。 若要查看每个角色支持的任务集，请使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 不能在报表管理器中查看、创建、修改或删除角色。 有关说明，请参阅[创建、 删除或修改角色&#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)。  
  
 **说明**  
 显示有关角色的其他信息。 对于预定义角色例如**浏览器**或**Content Manager**，此说明汇总了每个角色支持的任务。  
  
 **删除角色分配**  
 单击以删除用户或组的现有角色分配。 您不能删除剩余的最后一个角色分配（每个项必须至少有一个角色分配）。  
  
> [!NOTE]  
>  此按钮仅可用于“编辑角色分配”页上。  
  
## <a name="see-also"></a>请参阅  
 [创建、删除或修改角色 (Management Studio)](security/role-definitions-create-delete-or-modify.md)   
 [授予对本机模式报表服务器的权限](security/granting-permissions-on-a-native-mode-report-server.md)   
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [角色分配](security/role-assignments.md)   
 [授予用户对报表服务器的访问权限（报表管理器）](security/grant-user-access-to-a-report-server.md)  
  
  
