---
title: 新建系统角色分配：编辑系统角色分配页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 62a22ab9-1eb4-4ce5-8dd7-06b5ed2d9a2a
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7c1354228c1afbebe519a94d16973d024b84caac
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032388"
---
# <a name="new-system-role-assignments-edit-system-role-assignments-page-report-manager"></a>新建系统角色分配：编辑系统角色分配页 （报表管理器）
  使用“新建系统角色分配”页或“编辑系统角色分配”页可以定义报表服务器的安全性。 所有安全性都是通过将特定用户或组映射到这些用户或组可以执行的任务的角色分配来定义的。 任务列表表现为您在进行角色分配时选择的角色定义。  
  
 在系统级，您创建或修改的角色分配应用于整个报表服务器。 例如，创建共享计划的权限是在系统级指定的，因为共享计划在整个系统中使用。  
  
 默认情况下，Reporting Services 提供两个预定义的系统级角色：  
  
-   系统用户包含允许用户查看报表服务器属性和共享计划的任务，以及允许用户执行报表定义的任务，此类任务允许用户查看已经发布到报表服务器的点击链接型报表。 大部分用户都应当获得此角色分配。  
  
-   “系统管理员”角色包括用来创建和管理共享计划、设置服务器属性和为其他用户创建系统级角色分配的任务。 只有极少用户才需要此级别的权限。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-new-system-role-assignments-or-edit-system-role-assignments-page"></a>打开“新建系统角色分配”或“编辑系统角色分配”页  
  
1.  打开报表管理器。  
  
2.  在页面顶部的右角，单击 **“站点设置”**。 这会打开该站点的“常规属性”页。  
  
3.  选择 **“安全”** 选项卡。必须拥有“内容管理员”和“系统管理员”权限才能访问此页。  
  
4.  要创建新的角色分配，在工具栏中单击 **“新建角色分配”** 。 要编辑现有角色分配，请在“安全属性”页上单击组或用户旁边的 **“编辑”** 。  
  
## <a name="options"></a>选项  
 **组或用户**  
 键入域中的组或用户帐户的名称。 如果报表服务器在本地帐户下运行，则必须指定本地组或用户。 如果报表服务器在域帐户下运行，则必须指定域组或域用户。 按以下格式输入帐户：\<域 >\\< 帐户\>。  
  
> [!NOTE]  
>  此框仅可用于“新建角色分配”页上。  
  
 **Roles**  
 提供可以分配给其他用户的系统级角色的列表。 可以为单个角色分配指定多个角色。  
  
 报表管理器不显示每个角色中的任务，也不提供用来添加或修改任务的方法。 您必须按照角色的定义使用角色。 若要创建、修改或删除角色，请使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 有关详细信息，请参阅 [创建、删除或修改角色 (Management Studio)](security/role-definitions-create-delete-or-modify.md)。  
  
 请注意，如果使用的是具有高级服务的 [!INCLUDE[ssExpressEd2005](../includes/ssexpressed2005-md.md)] ，则必须使用所提供的默认角色。  
  
 **说明**  
 显示有关角色的其他信息。 对于预定义角色（如系统用户或系统管理员），说明概述每个角色支持的任务。  
  
 **删除角色分配**  
 单击以删除用户或组的现有角色分配。 您不能删除剩余的最后一个角色分配（每个项必须至少有一个角色分配）。  
  
> [!NOTE]  
>  此按钮仅可用于“编辑角色分配”页上。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [角色分配](security/role-assignments.md)   
 [角色定义](security/role-definitions.md)  
  
  
