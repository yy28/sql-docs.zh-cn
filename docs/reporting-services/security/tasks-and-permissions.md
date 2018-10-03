---
title: 任务和权限 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], tasks
- role-based security [Reporting Services], permissions
- security [Reporting Services], tasks
- security [Reporting Services], permissions
- role-based security [Reporting Services], tasks
- predefined tasks [Reporting Services]
- tasks [Reporting Services]
ms.assetid: d7ff90b5-b976-4270-b9ad-9d7b801d8263
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4793fef2ab0460c5adce81aa418130681ccdabfc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709325"
---
# <a name="tasks-and-permissions"></a>任务和权限
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，“任务”  是指用户或管理员可以执行的操作。 任务是预定义的。 您不能创建自定义任务，也不能以编程方式或通过工具修改所提供的任务。 总共有二十五个任务。 这些任务组成了基于角色的安全性中可用的完整操作集。 部分任务示例包括：“查看报表”、“管理报表”和“管理报表服务器属性”。  
  
 每个任务由一组权限构成，这些权限也是预定义的。 例如，“管理文件夹”任务包含创建和删除文件夹以及查看和更新文件夹属性等权限。 对每个任务的权限进行了说明，以便更为准确地描述每个任务。 不能直接对权限进行交互操作或者在角色分配中指定权限。 用户的权限是通过角色定义中包括的任务间接授予的。  
  
 只有当任务是角色的一部分并且该角色包含在角色分配中时，才能执行该任务。 因此，如果角色中不包括“查看模型”任务，或者角色分配中不包括该角色，则用户就不能查看报表模型。 下图显示了如何将权限组合到任务中，以及如何将任务组合到角色中以将角色用于特定的角色分配。  
  
 ![权限和任务关系图](../../reporting-services/security/media/report-securityobjects.gif "权限和任务关系图")  
权限和任务关系图  
  
## <a name="system-and-item-level-tasks"></a>系统级任务和项级任务  
 任务分为两类：系统级任务和项级任务。 一个角色只能包含单个类别中的任务。 下表对每一类别的任务进行了说明。  
  
|类别|描述|  
|--------------|-----------------|  
|[项级任务](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md)|对报表服务器管理的项（例如文件夹、报表、报表模型和资源）执行的操作。<br /><br /> 项级任务的作用域为报表服务器文件夹命名空间。 通过报表服务器上的文件夹或通过 URL 访问的项都受到包含项级任务的角色分配的保护。|  
|[系统级任务](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md)|在系统级执行的操作，例如，管理可用于多个项的作业或共享计划。 系统级任务的作用域扩展到报表服务器文件夹命名空间之外。|  
  
## <a name="see-also"></a>另请参阅  
 [角色定义](../../reporting-services/security/role-definitions.md)   
 [预定义角色](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [授予对本机模式报表服务器的权限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
