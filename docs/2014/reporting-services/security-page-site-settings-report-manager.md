---
title: “安全性”页（站点设置， 报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: acc9a905-90f8-4544-aec6-b2ab3a1b0015
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6a64dd80608d7b1d60718e5753d77fb37687234a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183107"
---
# <a name="security-page-site-settings-report-manager"></a>“安全性”页（站点设置， 报表管理器）
  使用“安全性”页可以查看用来控制报表服务器站点访问权限的系统角色分配。 系统角色分配存在于报表服务器命名空间或文件夹层次结构范围之外。 系统角色分配是全局性的，不能随具体项的变化而变化。 通过系统角色分配支持的操作包括创建和使用共享计划、使用报表生成器以及为某些服务器功能设置默认值。  
  
 在安装报表服务器时将创建默认的系统角色分配。 此系统角色分配授予本地系统管理员管理报表服务器环境的权限。 即使删除系统角色分配，本地系统管理员也可以随时设置本地报表服务器的安全性。  
  
 所有其他需要访问报表生成器或共享计划的用户都必须获得系统角色分配。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-security-page-for-site-settings"></a>打开站点设置的“安全性”页  
  
1.  打开报表管理器。  
  
2.  单击页面顶部的 **“站点设置”**。 这会打开该站点的“常规属性”页。  
  
3.  选择 **“安全”** 选项卡。  
  
## <a name="options"></a>选项  
 **删除**  
 单击此选项可删除现有的角色分配。 在单击 **“删除”** 之前，请选中要删除的组名或用户名旁的复选框。 如果只剩下一个角色分配，则不能删除它。 删除角色分配不会删除组或用户帐户或角色定义。  
  
 **新建角色分配**  
 单击此选项可打开“新建系统角色分配”页，通过该页可以为报表服务器站点创建其他系统角色分配。 有关详细信息，请参阅[新建系统角色分配： 编辑系统角色分配页&#40;报表管理器&#41;](../../2014/reporting-services/new-system-role-assignments-edit-system-role-assignments-page-report-manager.md)。  
  
 **编辑**  
 单击此选项可打开“编辑系统角色分配”页，通过该页可以为报表服务器站点编辑各个系统角色分配。 有关详细信息，请参阅[新建系统角色分配： 编辑系统角色分配页&#40;报表管理器&#41;](../../2014/reporting-services/new-system-role-assignments-edit-system-role-assignments-page-report-manager.md)。  
  
 **组或用户**  
 列出属于现有角色分配的组和用户。 当前文件夹的现有角色分配是为此列中显示的组和用户定义的。 单击组名或用户名旁边的 **“编辑”** 可以查看或编辑角色分配的详细信息。  
  
 **Roles**  
 列出属于现有角色分配的一个或多个角色定义。 如果给一个组或用户帐户分配了多个角色，那么该组或用户帐户可以执行属于所有这些角色的全部任务。 若要查看的每个角色支持的任务集，请使用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 不能在报表管理器中查看、创建、修改或删除角色。 有关说明，请参阅[创建、 删除或修改角色&#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [授予对本机模式报表服务器的权限](security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
