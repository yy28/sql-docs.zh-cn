---
title: 项的 "安全性" 属性页（报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 351b8503-354f-4b1b-a7ac-f1245d978da0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5ad98fe533caefa937d969754fa1278354e5c6e1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66102173"
---
# <a name="security-properties-page-items-report-manager"></a>项的“安全性”属性页（报表管理器）
  使用“安全属性”页可以查看或修改安全设置，以确定对文件夹、报表、模型、资源和共享数据源的访问。 此页可用于您有权保护的项。  
  
 对项的访问是通过指定某个组或用户可以执行的任务的角色分配来定义的。 角色分配包含一个用户名或组名，以及指定一组任务的一个或多个角色定义。  
  
 安全设置是从根文件夹以及依次向下的各子文件夹和这些文件夹中的项继承而来。 除非明确中断继承的安全性，否则子文件夹和项将继承父项的安全上下文。 如果为位于层次结构中间的某个文件夹重新定义安全策略，其所有子项（包括子文件夹）将采用新的安全设置。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-security-page-for-an-item"></a>打开项的“安全性”页  
  
1.  打开报表管理器，找到要配置安全设置的项。  
  
2.  悬停在该项之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，执行以下步骤之一：  
  
    -   单击 **“安全”**。 这会打开该项的“安全属性”页。  
  
    -   单击 **“管理”** 以打开该项的“常规属性”页。 然后，选择 **“安全性”** 选项卡。  
  
 **编辑项安全设置**  
 单击此选项可更改为当前项定义安全性的方式。 如果编辑文件夹的安全性，则更改将应用于当前文件夹及其所有子文件夹的内容。  
  
 此按钮对于主文件夹不可用。  
  
 编辑项安全性时可以使用以下按钮。  
  
 **删除**  
 选中要删除的组名或用户名旁边的复选框，再单击 **“删除”**。 如果角色分配是剩余的唯一角色分配，或者如果它是定义报表服务器的安全基线的内置角色分配（如“Built-in\Administrators”），则不能删除该角色分配。 删除角色分配不会删除组或用户帐户或角色定义。  
  
 **新建角色分配**  
 单击此选项可打开“新建角色分配”页，该页用于为当前项创建其他角色分配。 有关详细信息，请参阅 "[新建角色分配：编辑角色分配" 页 &#40;报表管理器&#41;](../../2014/reporting-services/new-role-assignment-edit-role-assignment-page-report-manager.md)。  
  
 **恢复到父级安全设置**  
 单击此选项可将安全设置重置到其直接父文件夹的安全设置。 如果贯穿报表服务器文件夹层次结构的继承是完整的，则使用顶层文件夹（即主文件夹）的安全设置。  
  
 **组或用户**  
 列出属于当前项的现有角色分配的组和用户。 当前文件夹的现有角色分配是为此列中显示的组和用户定义的。 单击组名或用户名可以查看或编辑角色分配的详细信息。  
  
 **角色**  
 列出属于现有角色分配的一个或多个角色定义。 如果为一个组帐户或用户帐户分配了多个角色，则该组或用户可以执行属于这些角色的所有任务。 若要查看与角色关联的任务，请使用 SQL Server Management Studio 来查看每个角色定义中的任务。  
  
## <a name="see-also"></a>另请参阅  
 [报表管理器 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [预定义角色](security/role-definitions-predefined-roles.md)   
 [授予对本机模式报表服务器的权限](security/granting-permissions-on-a-native-mode-report-server.md)   
 [角色分配](security/role-assignments.md)   
 [角色定义](security/role-definitions.md)  
  
  
