---
title: 系统级任务 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- system-level tasks [Reporting Services]
ms.assetid: 7023b388-40b2-4590-b227-115cf380a1e7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0f7ca906c8689c1bf8f40e79875acff5b7ab7c70
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570298"
---
# <a name="tasks-and-permissions---system-level-tasks"></a>任务和权限 - 系统级任务
  系统级任务是与应用于整个报表服务器站点的操作相关的权限的集合。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 还包括应用于特定项的项级任务。 有关详细信息，请参阅 [项级任务](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md)。 有关任务和权限总体情况的详细信息，请参阅 [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md)。  
  
> [!NOTE]  
>  如果以编程方式使用这些任务，则必须使用支持系统级任务的方法。 有关详细信息，请参阅 <xref:ReportService2010.ReportingService2010.ListTasks%2A> 和 <xref:ReportService2010.ReportingService2010.ListRoles%2A>。  
  
## <a name="permissions-in-system-level-tasks"></a>系统级任务中的权限  
 下表给出了各个系统任务的权限集合。 所列出的权限仅供参考，目的是为每个任务的可用功能提供更准确的说明。  
  
|任务|权限|  
|----------|-----------------|  
|执行报表定义|执行报表定义（权限和任务名称相同）|  
|生成事件|生成事件|  
|管理作业|读取系统属性<br /><br /> 更新系统属性|  
|管理报表服务器属性|读取系统属性<br /><br /> 更新系统属性|  
|管理角色|创建角色<br /><br /> 删除角色<br /><br /> 读取角色属性<br /><br /> 更新角色属性|  
|管理共享计划|创建计划|  
|管理报表服务器安全性|读取系统安全策略<br /><br /> 更新系统安全策略|  
|查看报表服务器属性|读取系统属性|  
|查看共享计划|读取计划|  
  
## <a name="see-also"></a>另请参阅  
 [授予对本机模式报表服务器的权限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
