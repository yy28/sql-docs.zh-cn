---
title: "创建、 删除或修改角色 (Management Studio) |Microsoft 文档"
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
- roles [Reporting Services], creating
- deleting roles
- removing roles
- roles [Reporting Services], definitions
- modifying roles
- roles [Reporting Services], deleting
- roles [Reporting Services], modifying
ms.assetid: 3d1d56e6-a283-44a7-8417-36cb4d2c74d1
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 42f66d05b179ee5f00c3322a2eb2943439936bcb
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="role-definitions---create-delete-or-modify"></a>角色定义的创建、 删除或修改
  Reporting Services 提供了定义对报表服务器的访问级别的预定义角色。 需要访问报表服务器的每个用户或组都通过说明可以执行的任务的角色来进行访问。 这些角色是对作为整体的报表服务器进行定义的。 不能对报表服务器的特定部分改变角色定义，也不能指定根据不同情况以不同的方式使用角色。  
  
 若要创建、修改或删除角色，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 只能删除未使用的角色。  
  
 若要将所创建的角色分配给用户或组，请使用报表管理器。 有关详细信息，请参阅[授予用户对报表服务器的访问权限（报表管理器）](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)。  
  
> [!NOTE]  
>  如果报表服务器配置为 SharePoint 集成模式，并且已连接到与该报表服务器集成的 SharePoint 站点，则可以查看和修改控制对报表服务器内容和操作的访问权限的权限级别。  
  
### <a name="to-create-a-role-definition"></a>创建角色定义  
  
1.  在对象资源管理器中，展开报表服务器节点。  
  
2.  展开“安全性”文件夹。  
  
3.  若要创建项目级角色定义，请右键单击“角色”，再指向“新建角色”。  
  
     或者，若要创建系统级角色定义，请右键单击“系统角色”，再指向“新建系统角色”。  
  
4.  为角色键入唯一名称。 名称必须至少包含一个字符。 它也可以包括空格和特定的一些符号，但不能包括以下字符：; ? : @ & = + , $ / * < > | " 或 /。  
  
5.  根据需要，可以键入说明。 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，此说明仅在此页上可见。 通过报表管理器查看此项的用户可以在该工具中看到此说明。  
  
6.  选择此角色的成员可以执行的任务。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-or-modify-a-role-definition"></a>删除或修改角色定义  
  
1.  在对象资源管理器中，展开报表服务器节点。  
  
2.  展开“安全性”文件夹。  
  
3.  若要删除或修改项目级角色定义，请展开“角色”文件夹。 执行下列操作之一：  
  
    1.  若要删除角色定义，请右键单击该项，再单击“删除”。 此时，将显示 **“删除对象”** 对话框。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  若要修改角色定义，请右键单击该项，再单击“属性”。 将显示 **“用户角色属性”** 对话框的“常规”页。  
  
         选择此角色的成员可以执行的任务，再单击 **“确定”**。  
  
4.  若要删除或修改系统级角色定义，请展开“系统角色”文件夹。 执行下列操作之一：  
  
    1.  若要删除系统角色定义，请右键单击该项，再单击“删除”。 此时，将显示 **“删除对象”** 对话框。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  若要修改系统角色定义，请右键单击该项，再单击“属性”。 将显示 **“系统角色属性”** 对话框的“常规”页。  
  
         选择此角色的成员可以执行的任务，再单击 **“确定”** 以应用更改。  
  
## <a name="see-also"></a>另请参阅  
 [在 Management Studio 中连接到报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [创建和管理角色分配](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [SQL Server Management Studio 中的 Reporting Services (SSRS)](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  

