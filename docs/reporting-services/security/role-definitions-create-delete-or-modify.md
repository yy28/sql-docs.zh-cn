---
title: 创建、删除或修改角色 (Management Studio) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- deleting roles
- removing roles
- roles [Reporting Services], definitions
- modifying roles
- roles [Reporting Services], deleting
- roles [Reporting Services], modifying
ms.assetid: 3d1d56e6-a283-44a7-8417-36cb4d2c74d1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d482eaf3186a5304d89a03fbeac526925b6268f8
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449604"
---
# <a name="role-definitions---create-delete-or-modify"></a>角色定义 - 创建、删除或修改

Reporting Services 提供了定义对报表服务器的访问级别的预定义角色。 每个需要访问报表服务器的用户或组都被分配了一个定义允许任务的角色。 这些角色是对作为整体的报表服务器进行定义的。 就如何在报表服务器的所有区域定义和使用角色方面，必须保持一致。

若要创建、修改或删除角色，可以使用 [!INCLUDE[SQL Server Management Studio](../../includes/ssmanstudiofull-md.md)]。 只能删除未使用的角色。

 若要将所创建的角色分配给用户或组，请使用 SSRS Web 门户。 有关详细信息，请参阅[授予用户对报表服务器的访问权限](../../reporting-services/security/grant-user-access-to-a-report-server.md)。

> [!NOTE]  
>如果报表服务器配置为 SharePoint 集成模式，并且已连接到与该报表服务器集成的 SharePoint 站点，则可以查看和修改控制对报表服务器内容和操作的访问权限的权限级别。

## <a name="to-create-a-role-definition"></a>创建角色定义

1. 在对象资源管理器中，展开报表服务器节点。

2. 展开“安全性”文件夹。

3. 要创建项目级角色定义，请右键单击“角色” > “新建角色”。

    或者，如果要创建项目级角色定义，请右键单击“系统角色” > “新建系统角色”。

4. 为角色键入唯一名称。 名称必须至少包含一个字符。 它也可以包括空格和特定的一些符号，但不能包括以下字符：`[; : \ / @ & = + , $ / * < > | "]`。

5. 根据需要，可以键入说明。 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，此说明仅在此页上可见。 通过 Web 门户查看此项的用户可以在该工具中看到此说明。

6. 选择此角色的成员可以执行的任务。

7. 选择“确定”。

### <a name="to-delete-or-modify-a-role-definition"></a>删除或修改角色定义  

1. 在对象资源管理器中，展开报表服务器节点。

2. 展开“安全性”文件夹。

3. 若要删除或修改项目级角色定义，请展开“角色”文件夹，然后执行下列操作之一：

    1. 要删除角色定义，请右键单击该项 > “删除”。 将显示“删除目录项”对话框。 选择“确定”删除角色。
  
    2. 要修改角色定义，请右键单击该项 > “属性”。 将显示 **“用户角色属性”** 对话框的“常规”页。

         选择此角色的成员可以执行的任务，然后选择“确定”。
  
4. 要删除或修改系统级角色定义，请展开“系统角色”文件夹。 执行下列操作之一：

- 要删除系统角色定义，请右键单击该项，然后选择“删除”。 将显示“删除目录项”对话框。 选择“确定”删除角色。

- 要修改系统角色定义，请右键单击该项，然后选择“属性”。 将显示 **“系统角色属性”** 对话框的“常规”页。 选择此角色的成员可以执行的任务，然后选择“确定”以应用更改。

## <a name="see-also"></a>另请参阅

 [在 Management Studio 中连接到报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)  
 [创建和管理角色分配](../../reporting-services/security/create-and-manage-role-assignments.md)  
 [SQL Server Management Studio 中的 Reporting Services (SSRS)](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)
